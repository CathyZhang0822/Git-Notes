设置好Postgres 之后： You now have a PostgreSQL server running on your Mac with these default settings:   


| name | value | 
| ---- | -------------- |
|Host|	localhost |   
|Port|	5432 |
|User|	your system user name|
|Database|	same as user|
|Password|	none |
|Connection URL|	postgresql://localhost |

### Flask   
When using the Flask-SQLAlchemy extension you can add to your application code:
```python
from flask import Flask
from flask.ext.sqlalchemy import SQLAlchemy
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://localhost/[YOUR_DATABASE_NAME]'
db = SQLAlchemy(app)
```

### Django
In your settings.py, add an entry to your DATABASES setting:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql_psycopg2",
        "NAME": "[YOUR_DATABASE_NAME]",
        "USER": "[YOUR_USER_NAME]",
        "PASSWORD": "",
        "HOST": "localhost",
        "PORT": "",
    }
}
```
