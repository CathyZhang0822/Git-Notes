
# 几种撤销场景
场景1.1：**unstaged(code change):** 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令
```$ git checkout -- file```   
场景1.2：**unstaged file/folder:** 当你误创建了一些file/folders，想要舍弃，这时候`git checkout`就无法做到了，这时候需要
用`git clean`   
```$ git clean -f```   
To remove directories, run `git clean -f -d` or`git clean -fd`   
To remove ignored files, run `git clean -f -X` or `git clean -fX`   
To remove ignored and non-ignored files, run `git clean -f -x` or `git clean -fx`

场景2.1：**staged code change:** 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令
```$ git reset HEAD file```
就回到了场景1，第二步按场景1操作。(git reset默认是mixed)   
场景2.2：**staged file** 当你add了一个file，但是想撤回staged file。这时用 ```git reset filename.txt```

场景3：已经commit，想要撤销本次提交，git reset --hard,不过前提是没有推送到远程仓库。

场景4：不小心删除了一个file，这个删除操作一般是自动stage
1. `git restore --unstaged <file>`
2. `git restore <file>`
以上方法第二天就不管用了
Assuming you're wanting to undo the effects of `git rm <file> or rm <file>` followed by `git add -A` or something similar:
```
# this restores the file status in the index
git reset -- <file>
# then check out a copy from the index
git checkout -- <file>
```
作者：胜天半子bibi酱
链接：https://juejin.im/post/5abef8356fb9a028df22bd78

# git reset soft,hard,mixed之区别深解  
链接：https://www.cnblogs.com/kidsitcn/p/4513297.html

先来看几个关键的术语： （在markdown格式里面换行，在上一行末尾敲打两个空格）  
**HEAD**  
这是当前分支版本顶端的别名，也就是在当前分支你最近的一个提交  

**Index**  
index也被称为staging area，是指一整套即将被下一个提交的文件集合。他也是将成为HEAD的父亲的那个commit  

**Working Copy**  
working copy代表你正在工作的那个文件  

**1.soft**  
--soft参数告诉Git重置HEAD到另外一个commit，但也到此为止。如果你指定--soft参数，Git将停止在那里而什么也不会根本变化。这意味着index,working copy都不会做任何变化，所有的在original HEAD和你重置到的那个commit之间的所有变更集都放在stage(index)区域中。

**2.hard**  

--hard参数将会blow out everything.它将重置HEAD返回到另外一个commit(取决于~12的参数），重置index以便反映HEAD的变化，并且重置working copy也使得其完全匹配起来。这是一个比较危险的动作，具有破坏性，数据因此可能会丢失！如果真是发生了数据丢失又希望找回来，那么只有使用：git reflog命令了。makes everything match the commit you have reset to.你的所有本地修改将丢失。如果我们希望彻底丢掉本地修改但是又不希望更改branch所指向的commit，则执行git reset --hard = git reset --hard HEAD. i.e. don't change the branch but get rid of all local changes.另外一个场景是简单地移动branch从一个到另一个commit而保持index/work区域同步。这将确实令你丢失你的工作，因为它将修改你的work tree！

**3.mixed(default）**

--mixed是reset的默认参数，也就是当你不指定任何参数时的参数。它将重置HEAD到另外一个commit,并且重置index以便和HEAD相匹配，但是也到此为止。working copy不会被更改。所有该branch上从original HEAD（commit）到你重置到的那个commit之间的所有变更将作为local modifications保存在working area中，（被标示为local modification or untracked via git status)，但是并未staged的状态，你可以重新检视然后再做修改和commit

