# 有关 gitignore

## Ignore files that have already been tracked/commited/pushed

1. Add the files you want to ignore to your .gitignore file

2. To unstage and remove paths only from the index, not the file system, run:

`git rm -r --cached`

3. Run:

`git add .`

4. Run:

`git commit -m "Removed sensitive files`