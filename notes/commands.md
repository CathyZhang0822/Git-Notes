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

4. Set variables
```
auth="abc xxx"
$auth
bash: abc: command not found
echo $auth
abc xxx
```
注意不加echo的话被当成command来处理！
