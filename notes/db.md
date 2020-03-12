### Flask db migration
1. Install `Flask-Migrate`: `pip install Flask-Migrate`   
2. locate Flask application: `export FLASK_APP=app.py` (把app.py换成自己的相关app) 
在 `app.py`里面要定义这些东西：
```python
from flask import Flask
from flask.ext.sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

app = Flask(__name__)
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = True
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://localhost/devdb'

db = SQLAlchemy(app)
migrate = Migrate(app, db)
```
(以下三个命令需要在`app.py`所在的folder里，不然会有file doesn't exist error，暂时还没有办法解决)
3. `Flask db init`   
_________ 以上是第一次做的__________   
4. `Flask db migrate`
会坐`versions`里面产生一个file，这个file是Alembic自动产生出来的，有时候需要adjust
还可以加一句话：`flask db migrate -m "Initial migration."`   
5. `flask db upgrade`

### db.session.commit() 与 db.session.flush()
`session.flush()` communicates a series of operations to the database (insert, update, delete). The database maintains them as pending operations in a transaction. The changes aren't persisted permanently to disk, or visible to other transactions until the database receives a COMMIT for the current transaction (which is what `session.commit()` does).   

如果只用`session.flush()`的话，别人是无法看到的。`flush`只是保存**自己session**的变化，我们可以理解每一个窗口就是一个session

# Relationships
## One-to-Many
The most common relationships are one-to-many relationships.   
1. First you need to supply a primary ky of each model
2. Then you need to define one foreign key which refers to the Primary Ky of the other model.
3. then you can define a relationship with a backref that allows direct access to the related model. (但是现在还不确定这个relation要定义在哪个Model里面，目前我觉得定义在任何一个里面都行)
```python
class Person(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    addresses = db.relationship('Address', backref='person', lazy=True)

class Address(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    email = db.Column(db.String(120), nullable=False)
    person_id = db.Column(db.Integer, db.ForeignKey('person.id'),
        nullable=False)
```
### relationship & backref
通过上面的 `db.relationship()`, `Person`有了一个可以访问的`addresses` -> `person1.addresses`。 它返回的可能是一个query，需要做`person1.addresses.all()`. 也可能是一个object, (这取决于`lazy`的设定，下面会讲)   

似乎明白了了一下foreign key 和 relationship的区别： foreign key是要 `addresss1.person_id`. 只能单向并且只能访问 `id`.   
而relationship 可以双向，可以直接返回objects，可以返回query。

### lazy
https://docs.sqlalchemy.org/en/13/orm/relationship_api.html#sqlalchemy.orm.relationship.params.lazy   
True - a synonym for ‘select’  
False - a synonym for ‘joined’   
None - a synonym for ‘noload’   
还有经常用的事dynamic，返回一个 Query object。

## One-to-One
one-to-one 和 one-to-many很像，只需要加一个限制：`uselist=False`

## Many-to-Many
If you want to use many-to-many relationships you will need to define a helper table that is used for the relationship. For this helper table it is strongly recommended to not use a model but an actual table: 
```
tags = db.Table('tags',
    db.Column('tag_id', db.Integer, db.ForeignKey('tag.id'), primary_key=True),
    db.Column('page_id', db.Integer, db.ForeignKey('page.id'), primary_key=True)
)

class Page(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    tags = db.relationship('Tag', secondary=tags, lazy='subquery',
        backref=db.backref('pages', lazy=True))

class Tag(db.Model):
    id = db.Column(db.Integer, primary_key=True)
```
需要额外的一个table!

## Lazy loading vs Eager loading
https://stackoverflow.com/questions/31366236/lazy-loading-vs-eager-loading   
**When to use eager loading** 

In "one side" of one-to-many relations that you sure are used every where with main entity. like User property of an Article. Category property of a Product.   
Generally When relations are not too much and eager loading will be good practice to reduce further queries on server.

**When to use lazy loading**

Almost on every "collection side" of one-to-many relations. like Articles of User or Products of a Category
You exactly know that you will not need a property instantly.   
Note: like Transcendent said there may be disposal problem with lazy loading.

