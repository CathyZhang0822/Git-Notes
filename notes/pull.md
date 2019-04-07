# git fetch   

credits: https://blog.csdn.net/Sevk/article/details/6040420

1. git fetch：相当于是从远程获取最新版本到本地，不会自动merge  
```
git fetch origin master
git log -p master..origin/master
git merge origin/master
```
以上命令的含义：  
首先从远程的origin的master主分支下载最新的版本到origin/master分支上  
然后比较本地的master分支和origin/master分支的差别  
最后进行合并  

上述过程其实可以用以下更清晰的方式来进行：  
```
git fetch origin master:tmp
git diff tmp 
git merge tmp
```
从远程获取最新的版本到本地的test分支上之后再进行比较合并



# git pull 命令
git pull命令完整格式比较长，先从最简单的origin + master来开始记录

举个列子：我在github直接对这个repo进行了修改，有了新commits A,B,C. 我还在本地对代码进行了修改，有了新commits E,F,G.
类似于这种情况：

<img width="431" alt="screen shot 2019-01-04 at 4 19 16 pm" src="https://user-images.githubusercontent.com/36396754/50717513-90818400-103c-11e9-88a4-f4e8b3e17053.png">

运行 `git pull`，先fetch后merge：

<img width="302" alt="screen shot 2019-01-04 at 4 19 24 pm" src="https://user-images.githubusercontent.com/36396754/50717538-d1799880-103c-11e9-941c-73e49b7b1f9e.png">

此时 H commit就是自动产生的一个'merge' commit.

中途可能会产生conflict 需要解决

#1
