## How do I alias commands in git?
Basically you just need to add lines to ~/.gitconfig
```
[alias]
    st = status
    ci = commit -v
```
Or you can use the git config alias command:    

`$ git config --global alias.st status `
Use single quote:   
`$ git config --global alias.ci 'commit -v'`
