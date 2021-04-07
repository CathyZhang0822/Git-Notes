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
https://dashboard.heroku.com/apps/yuelin/deploy/github
和Github integrate到一起了

### Test locally
`heroku local`

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

**`heroku run bash` !!!!!!!!!!!!!!!**

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

4. Get/Set/Delete Env variables 
```
heroku config:get GITHUB_USERNAME
```
```
heroku config:set FLASK_APP=<your flask app path> 
```
```
heroku config:unset GITHUB_USERNAME
Unsetting GITHUB_USERNAME and restarting myapp... done, v13
```
check configs:
```
heroku config
=== yuelin Config Vars
FLASK_APP: __init__.py
```

4. Create Procfile
In my personal_site app case: （我下面这个好像不对，port有问题）
```
web: flask run
```
别人用gunicorn的例子：
`__init__`是创建APP的
```
web: gunicorn -w 4 -b "0.0.0.0:$PORT" __init__:app
```
# Connect to Postgresql database
### 1. 添加addon   
``
heroku addons:create heroku-postgresql:hobby-dev
``
hobby-dev 是那个免费的Plan
### 2. Check addons
```
heroku ps:info
heroku addons
heroku confg
```
三连来查看   
### 3.  Connecting to Python   
`pip install psycopg2-binary`

```python
import os
import psycopg2

DATABASE_URL = os.environ['DATABASE_URL']

conn = psycopg2.connect(DATABASE_URL, sslmode='require')
```
### 4. Prduction DB migration/update
1. 先到heroku app的bash `heroku run bash`   
2. cd 到app的根目录 `cd app`   
3. `flask db upgrade` 一般情况下我们在local run `flask db migrate`，然后把migration file push上去   
### 5. 进入到heroku的db 
`heroku pg:psql`   

