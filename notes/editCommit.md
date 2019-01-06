# 对 commits 进行操作

关于对commits的操作有很多，要一直积累总结

## 对已经push的commits进行delete 
把last 2 commits显示出来

`git rebase -i HEAD~2`
显示出这样：
```pick d6f81a8 create the project in intellij and add gitignore
 pick 05aed2e add storage manager library
 
 # Rebase a79b4a4..05aed2e onto a79b4a4 (2 commands)
 #
 # Commands:
 # p, pick = use commit
 # r, reword = use commit, but edit the commit message
 # e, edit = use commit, but stop for amending
 # s, squash = use commit, but meld into previous commit
 # f, fixup = like "squash", but discard this commit's log message
 # x, exec = run command (the rest of the line) using shell
 # d, drop = remove commit
 ```
 然后添加你想完成的命令，比如 `delete d6f81a8 create the project in intellij and add gitignore` ,保存退出
 此时对local的commits完成了修改，再 `git push origin master -f`修改remote commits
 
 ## 对已经push的commits进行squash
 比如我想把几个commits合并成一个commit
 
 举个例子：
 把last 5 commits显示出来：
 `git rebase -i HEAD~5`
 
我想把'git pull' 和'update pull.md' 这两个commits 合并，所以把'update pull.md'的这个commit的 **pick** 改成 **squash**：

<img width="304" alt="screen shot 2019-01-04 at 6 27 14 pm" src="https://user-images.githubusercontent.com/36396754/50731462-d82a0d80-1119-11e9-9936-9d344c97128c.png">
保存后退出:

`git log --pretty=oneline --abbrev-commit`

查看local commits，会显示跟remote commits不同
再把local的commit change push到remote上去：

`git push origin master -f`

前后commits history对比：

之前：

<img width="958" alt="screen shot 2019-01-04 at 6 30 06 pm" src="https://user-images.githubusercontent.com/36396754/50731519-c184b600-111b-11e9-86ed-0c4d497beec2.png">

之后：

<img width="961" alt="screen shot 2019-01-04 at 6 31 13 pm" src="https://user-images.githubusercontent.com/36396754/50731521-cba6b480-111b-11e9-9944-d4be21c94714.png">

我们可以主要到通过 `git pull`产生的 **merge commit** 也被自动合并


