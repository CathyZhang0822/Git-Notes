# Environment variables
1. 在bash `printenv`，显示所有环境变量
2. `echo $<variable name>` 会显示value
ie:
```
(env) ➜  app git:(master) ✗ echo $FLASK_ENV
development
```
3. 设置一个环境变量：   
`export FLASK_APP=hello.py`
