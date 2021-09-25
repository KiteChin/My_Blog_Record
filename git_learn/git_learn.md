# Git 学习 
Git是Linus Torvalds 为了帮助管理Linux 内核开发而开发的一个开放源码的版本控制软件，它可以帮助我们方便管理项目，同时也可以使用Git将本地仓库推送至Github

推荐一个Git学习的游戏 [`git game`](https://learngitbranching.js.org/?locale=zh_CN)

* ## [常见命令](#常见命令)
  - ### [git add](#git-add)
  - ### [git commit](#git-commit)
  - ### [git branch](#git-branch)
  - ### [git checkout](#git-checkout)
  - ### [git merge](#git-merge)
  - ### [git rebase](#git-rebase)
  - ### [git reset and git revert](#git-reset-and-git-revert)
  - ### [git fetch](#git-fetch)
  - ### [git pull](#git-pull)
  - ### [git push](#git-push)


## 常见命令
- `git add`
 `git commit`
 `git branch`
 `git checkout`  
 `git merge`
 `git rebase`
 `git fetch`
 `git pull`  
 `git push`

---

### git add
`git add` 将文件添加到暂存区

**eg.** `git add -A`

---

### git commit
`git commit` 将暂存区的文件提交到git库里

**eg.**`git commit -m "comment"` `git commit -am "comment"`

---

### git branch
`git branch` 创建分支( 不切换 )

**eg.**`git branch bugFix`

`git branch -f main HEAD~3` 将main分支移动到HEAD的第3级父提交

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:12:10.jpg)

---

### git checkout 
`git checkout` 切换分支( -b 创建并切换分支 )

**eg.**`git checkout bugFix` `git checkout -b newBugFix` `git checkout origin/main`

`git checkout` 实际上是改变HEAD的指向

**eg.**`git checkout hash`将HEAD指向hash值所对应到记录

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:02:59.png)

---

### git merge
`git merge` 合并分支

**eg.**`git merge bugFix`将bugFix合并到main里( 两分支不再同一路 )

合并后可以切换到bugFix分支使用`git merge main`将bugFix分支移动到main分支上

---

### git rebase
`git rebase` 另一种合并分支命令

![1jpg](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2013:55:03.png)

---

`git rebase main` or `git rebase main bugFix`:

![1jpg](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2013:55:20.png)

切换到main `git rebase bugFix`:

![1jpg](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2013:55:40.png)

---

### git reset and git revert
`git reset` 将当前分支退回之前到提交记录

**eg.**`git reset HEAD~1` `git reset hash`

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:25:37.jpg)

`git revert` 将要退回到记录提交到新到记录(用于协作)

**eg.**`git revert HEAD`

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:27:04.jpg)

PS.上图中C2'与C1记录是一样的

---

### git fetch
`git fetch` 拉取远程仓库

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:54:47.jpg)

`git fetch`:

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2016:54:58.jpg)

---

### git pull
在`git fetch`后，你可以通过以下命令像合并本地分支那样来合并远程分支  

- `git cheery-pick origin/main`
- `git rebase origin/main`
- `git merge origin/main`

由于需要经常在`git fetch`后使用合并命令，git提供`git pull`命令便捷实现这两个操作  

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2017:15:30.jpg)

`git pull`:

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2017:15:44.jpg)

---

### git push
`git push`将本地变更上传到远程仓库，并在远程仓库合并你的新的提交记录

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2017:45:21.jpg)

`git push`:

![](https://github.com/KiteChin/Photo-cloud/raw/master/git_learn/screenshot-2021-09-17%2017:45:31.jpg)

PS.当所在分支和远程分支不再同一条节点线上时( 即与远程仓库提交历史偏离 ) `git`将不允许你`push`变更,这时可以先用`git pull`再使用`git push`







