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
