# Github 学习笔记
汇总一下经常用的的commands，省了每次都去stack overflow了

| # | 笔记 | Description |
| ---- | -------------- | ----------------- |
| | **Git，github 等等** | |
| 1 | [在readme里面添加图片](./notes/addImg.md)|不仅仅是readme，是所有.md文件 |
| 2 | [Locally && Remotely更改 commits history](./notes/editCommit.md)| 1. 删除已经push的commits 2.删除没有push的commits（TODO）|
| 3 | [git pull/git fecth](./notes/pull.md)| `git pull` is shorthand for `git fetch` followed by `git merge FETCH_HEAD`|
| 4 | [Ignore files that have already be pushed](./notes/ignoreFile.md)|对于没有tracked/committed/pushed files, 我们只需要在.gitignore 里面添加就好了。但是对于已经tracked files, 应该怎么做呢？|
| 5 | [Git撤销操作](./notes/gitCheckOutFile.md) |撤销 unstaged/staged/commited/pushed changes|
| 6 | [Git Branches遇到各种senario](./notes/gitBranch.md) |1. 在一个branch里新建的file也出现在了其他branch|
| 7 | [Phabricator Stacked Diff Workflow](./notes/Stacked_Diffs.md) |Create stacked diffs|
| 8 | [Change upstream](./notes/changeUpstream.md)| Change upstream, rebase child branch to master|
| 9 | [把local连接到github和heroku](./notes/heroku.md)| 创建remotes, 链接remotes|
| | **Python, framework, 以及相关数据库** | |
| 1 | [Connect Postgres server to Flask](./notes/postgres.md)| 在Flask里面使用PostgresSQL  |
| 2 | [Flask db migration](./notes/db.md)| Flask db migration相关命令 |
| 3 | [PYTHONPATH](./notes/import.md) | 梳理一下import路径问题 |
| 4 | [Postgres Commands](./notes/postgress_commands.md)| 常见postgres commands|
| 5 | [Heroku Setup](./notes/herokuapp.md)| 1. 常见的heroku commands <br> 2.Heroku app setup step by step|
| | **Frontend** | |
| 1 | [Template inheritance](./notes/templates.md)| flask html里面的`block`, `extend`, `super`.. 等代表什么呢？|
| 2 | [Bootstrap](./notes/bootstrap.md) | 1. 如何导入bootstrap? |
| 3 | [Images](./notes/images.md) | 1. 前端如何serve pictures？|
