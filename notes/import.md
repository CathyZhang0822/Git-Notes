#### 快刀斩乱麻
```
repo/
   __init__.py
   sub1/
      __init__.py
      sub1a/
         __init.py
         mod1.py
   sub2/
      __init__.py
      mod2.py
```
很多时候我们会在同一个app里面import来import去的，最简单的方法就是把`repo`所在的parent folder加到`PYTHONPATH`里面去。   
The simplest solution is to put the directory containing repo in your PYTHONPATH, and then just use absolute-path imports, e.g. `import repo.sub2.mod2` and so on.
ie:
```
export PYTHONPATH=/Users/yuelinzhang/Desktop/CS/:$PYTHONPATH
```
或者更加general
```
export PYTHONPATH=$(cd .. && pwd):$PYTHONPATH
```
