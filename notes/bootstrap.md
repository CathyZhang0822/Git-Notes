## 如何导入bootstrap？如何控制version？
### 1. Flask-Bootstrap
在Flask app的setupfile里面import
```python
from flask_bootstrap import Bootstrap
app = Flask(__name__)
bootstrap = Bootstrap(app)
```
然后在自己的html file里面extend:
```html
{% extends "bootstrap/base.html" %}
....
```
但是注意，这个installed的bootstrap是Bootstrap 3.3.7。所以develop的时候要看这个doc: https://getbootstrap.com/docs/3.3/
但是现在bootstrap已经发展到4.x了   

### 2. Starter Template (版本控制灵活，推荐)
https://getbootstrap.com/docs/4.4/getting-started/introduction/
把这个starter template，设置成一个`base.html`. 让自己的其他Html extend它就好了。但是要自己加相应的`block`。
