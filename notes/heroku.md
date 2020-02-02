### 创建了一个project,想把它们push 到 `github`和 `heroku`上
#### 连接到github
链接github
```
git init
git add -A
git commit -m "first commit"
git remote add origin https://github.com/YuelinZhang0822/personal_site 
```
查看remote
```
(base) ➜  personal_site git:(master) git remote
origin
```
#### 连接到heroku
创建heroku app
```
heroku create yuelin (yuelin is app-name)
```
查看apps:
```
(base) ➜  personal_site git:(master) heroku apps
=== zyl960822-@tamu.edu Apps
app1
app2...
yuelin
```
链接heroku:
```
heroku git:remote -a yuelin (your_app_name)
```
#### 查看remotes:
```
(base) ➜  personal_site git:(master) git remote
heroku
origin
```
详细版本：  
```
(base) ➜  personal_site git:(master) git remote -v
heroku	https://git.heroku.com/yuelin.git (fetch)
heroku	https://git.heroku.com/yuelin.git (push)
origin	git@github.com:YuelinZhang0822/personal_site.git (fetch)
origin	git@github.com:YuelinZhang0822/personal_site.git (push)
```

#### 更改remotes
Instead of removing and re-adding, you can do this:   
```
git remote set-url origin git://new.url.here
```
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

4. Create Procfile
In my personal_site app case:
```
web: gunicorn -w 4 -b "0.0.0.0:$PORT" __init__.py:app
```

