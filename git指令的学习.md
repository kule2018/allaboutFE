创建一个空目录

```javascript
$ mkdir learngit
$ cd learngit
$ pwd
```

将目录变成git可以管理的仓库

```javascript
git init
```

进入文件修改

```javascript
vi
然后esc键，：wq保存并退出
```

将文件添加到仓库(实际上是添加到暂存区)

```javascript
git add 文件名
```

将文件提交到仓库（实际上是把暂存区中的东西全都添加到分支）

```javascript
git commit -m "提交说明"
```



初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

1. 使用命令`git add `，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m `，完成。



查看历史记录

```
git log
```

 `git log`命令显示从最近到最远的提交日志 

如果嫌弃输出信息太多则添加

```
git log --pretty=online
```



 Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

使用git reset命令

```
git reset --hard HEAD~次数
```

 

若是文档回退，则会像一个时光机器，回退到某一版本之后的修改都不会显示在git log中，若是想要回到指定版本，则

```
git reset--hard ****（commit id，可只写前几位)
```



查看文档

```
cat 文件名
```



命令`git reflog`用来记录你的每一次命令：

```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```



 ![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0) 



查看状态

```
git status
```

 

每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。 



丢弃在工作区的修改

```
git checkout -- 文件名
```



从工作区和版本库都删除掉文件

```
git rm 文件名               删除的不可恢复
git commit -m"delete ****"
```

若工作区删错了，可以从暂存区中恢复

```
rm 文件名        删除文件
git checkout -- 文件名             从暂存区中恢复文件
```



要关联一个远程库，使用命令`git remote add origin git@github.com:server-name/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；



 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。 

```javascript
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```



 我们创建`dev`分支，然后切换到`dev`分支： 

```
$ git checkout -b dev

相等于下面两个命令：
$ git branch dev
$ git checkout dev
```

切换分支

```
$git checkout 分支名称
```

 

用`git branch`命令查看当前分支：

```
$ git branch
* dev
  master
  
git branch命令会列出所有分支，当前分支前面会标一个*号。
```



 `git merge` 命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。 否则，master分支中的修改操作不包含dev分支中的操作。

```javascript
//切换到master分支之后
$ git merge 分支名称
//这种分支是快速模式，Fast-forward。然而，在删除分支后，则会丢掉分支信息


$ git merge --no-ff -m "merge with no-ff" 分支名称   
//本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
//--no-ff参数，表示禁用Fast forward
```



合并完成后，就可以放心地删除`dev`分支了：

```
$ git branch -d dev
Deleted branch dev (was b17d20e).
```





**分支策略**

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

**小结**

Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。





储存当前工作进度

```
$ git stash
 Saved working directory and index state WIP on dev: f52c633 add merge
```



一般需要处理bug的时候：

- $ git stash   储存当前分支的工作,可用 $git stash list 查看

- $ git checkout master   回到master分支

- $git checkout -b ***  创建一个修改Bug的分支

- 修改完之后，add  commit 提交

- $ git checkout master  切换到master分支

- $ git merge --no-ff -m "******" ******           完成合并修改Bug的分支

- 删除Bug分支

- 回到之前工作的分支 $git checkout ***

- 恢复stash   $git stash apply 然后删除 $git stash drop

    或者直接恢复删除 $git stash pop

  - 恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令： 





