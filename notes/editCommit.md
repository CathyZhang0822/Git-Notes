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
