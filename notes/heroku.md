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

