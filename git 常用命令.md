# <center>git 常用命令</center>
---
### 1. 查看状态
```git status```

### 2. 移除文件
* ```git rm ```
* ```git rm --cached xxx```我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。
* ```git rm log/\*.log```git rm 命令后面可以列出文件或者目录的名字，也可以使用 glob 模式。
* > 注意到星号 * 之前的反斜杠 \， 因为 Git 有它自己的文件模式扩展匹配方式，所以我们不用 shell 来帮忙展开。 此命令删除 log/ 目录下扩展名为 .log 的所有文件
* ```git rm \*~```该命令会删除所有名字以 ~ 结尾的文件

### 3.重命名（移动文件）
* ```git mv file_from file_to```

### 4.查看历史
* ```git log```
* ```git log -p -2``` 查看最近两次的提交
* ```$ git log --stat```每次提交的简略统计信息
* ```git log --since=2.weeks``` 列出最近两周的所有提交,类似 --since 和 --until 这种按照时间作限制的选项很有用
* https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2

### 5.撤消操作
* ```git commit --amend```撤销commit
* ```git reset HEAD xxx```取消暂存(add)的文件
* ```git checkout -- xxx```撤消对文件的修改
* https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C

### 6.远程仓库的使用
* ```git remote -v```查看远程仓库
* ```git remote add pb https://github.com/paulboone/ticgit```添加远程仓库
* https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8

### 7.打标签
* ```git tag```列出标签
* ```git tag -a v1.4 -m "my version 1.4"``` 附注标签
* ```git show v1.4```通过使用 git show 命令可以看到标签信息和与之对应的提交信息
* 后期打标签查看连接
* https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE

### 8.分支
* ```git branch xxx``` 分支创建
* ```git checkout testing``` 分支切换
* https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B
  
### 9.分支的新建与合并
* ```git checkout -b iss53```新建一个分支并同时切换到那个分支上
* 分支合并
  ```
    $ git checkout master
    $ git merge hotfix
    Updating f42c576..3a0874c
    Fast-forward
    index.html | 2 ++
    1 file changed, 2 insertions(+)
  ```
* ```git branch -d hotfix``` 删除分支
* ```git mergetool```启动一个合适的可视化合并工具,解决冲突用
* https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6

### 10.分支管理
* https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%A1%E7%90%86