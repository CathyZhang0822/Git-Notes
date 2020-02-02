# Heroku Commands
### Check apps
1. `heroku apps`   
```
(base) ➜  personal_site git:(master) heroku apps
=== zyl960822-@tamu.edu Apps
agile-eyrie-72035
calm-taiga-39676
career-closet
cryptic-journey-72189
mighty-fortress-23421
yuelin
```
2. `heroku apps:info`
```
(base) ➜  personal_site git:(master) heroku apps:info
=== yuelin
Auto Cert Mgmt: false
Dynos:
Git URL:        https://git.heroku.com/yuelin.git
Owner:          zyl960822-@tamu.edu
Region:         us
Repo Size:      0 B
Slug Size:      0 B
Stack:          heroku-18
Web URL:        https://yuelin.herokuapp.com/
```
### Deploying code
`git push heroku master`

### Viewing logs
`heroku logs --tail`

### SSH Tunneling
1. Check running dyno:
`heroku ps`

2. Restart a web
`heroku restart web.1`

3. SSH
`heroku ps:exec`
or specify a dyno:
`heroku ps:exec --dyno=web.2`

# Setup a Heroku app step by step
1. Create an empty Heroku app and add it to remote
```
heroku login
heroku create
heroku apps
git remote -v
```

2. Create a virtual env, develop your local app.
简历virtual env一定要在创建自己的local app之前！！！
```
python3 -m venv env
source env/bin/activate
deactivate
```
会发现所用的python和Pip 是env里面特定的
```
(env) (base) ➜  personal_site git:(master) ✗ which pip
/Users/yuelinzhang/Desktop/CS/personal_site/env/bin/pip
(env) (base) ➜  personal_site git:(master) ✗ which python
/Users/yuelinzhang/Desktop/CS/personal_site/env/bin/python
```

3. Add `requirments.txt`
一个简单的办法， 在root folder:
`$ pip freeze > requirements.txt`

4. Set Env variables 
```
heroku config:set FLASK_APP=<your flask app path> 
```
check configs:
```
heroku config
=== yuelin Config Vars
FLASK_APP: __init__.py
```

4. Create Procfile
In my personal_site app case:
```
web: flask run
```
别人用gunicorn的例子：
```
web: gunicorn -w 4 -b "0.0.0.0:$PORT" __init__.py:app
```
