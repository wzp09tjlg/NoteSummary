在使用git的过程中，总是有些新的发现和新的功能。当然随着使用的熟悉和顺手，越来越觉得git的好用了。下边是对git的一些认识，对于初来认识git的人有一些帮助，和对以后再看git的使用时做个记录：

1.对于本地的仓库，使用
git init就能将本地 的一个文件夹变成一个由git管理的仓库，然后就可以针对这个库做增 删 改 查的操作。
当然使用的命令是git的命令
git add .表示当前的目录下提交所有文件。
git status 查看当前分支的状态，有更新了 未添加 未提交的 都会在这个命令下显示出来。
git branch -a是查看远程的分支
git branch 是查看本地的分支
git branch branchName 创建一个分支
git tag 查看tag
git tag tagName 创建一个tag
git checkout 切换分支，可以查看当前是哪个分支之后，再进行切换的操作
git merge branchName 对于当前的分支进行合并，合并来源是branchName分支
git push origin master:master 对送本地的分支到远程服务的分支 src：des 后边的意思是本地分支 到远程服务分支，如果省略没写远程服务分支，那就代表会在远程服务分支上新建一个分支(如果远程服务上没有这个名字的分支的法).如果省略没写本地服务分支，那就代表删除远程这个名字的分支。
git pull origin master:master 对本地库进行更新，名字的省略和上边push类似。
git HEAD表示当前所在的分支，一般使用在推送的时候不用进行分支的切换，只是将当前分支推到服务上去。

二：远程库的认识
远程仓库可以使用初始化一个裸仓库，然后本地clone一个远程的裸仓库，再进行操作。
命令为git clone “url”
这样本地的仓库是就和远服务的仓库关联上，针对本地仓库操作之后，就可以再同步到服务的仓库。

远程也可以创建一个仓库，本地也创建一个仓库，通过本地添加远程苍库，然后将本地的仓库和远程的仓库关联上。命令如下：
git remote add origin "url"
前提是本地需要创建一个仓库，然后才能进行远程服务仓库的关联。
使用呢remote add 添加一个远程仓库，远程仓库的名字为origin，在远程仓库下有一个分支叫master,本地也有一个分支叫master跟远程苍库的master对等。

clone 和 remote add 的区别：
git clone “url” 本地会默认创建一个url中path不带.git的工程在本地，
remote add则需要先创建一个仓库，然后再讲远程的仓库加载到本地仓库来：
mkdire projectName
cd projectName
git init
git remote add origin "url"
相当于上边的这样几个命令。 

三：
使用，对于一般项目的版本控制，会使用先在服务商创建一个仓库，再通过clone下载到本地，这样就可以开始本地库和远程服务库同步开发了。
对于一般开源的项目，会在本地先创建一个仓库，然后再在github上创建一个仓库，本地的仓库添加远程仓库，将本地的仓库和远程的仓库关联上，然后可以实现将本地的库推送的远程服务的库上去。

要熟悉的命令不多，可以边修改项目边查看git的指令。多联系多看log操作日志。

使用过的命令如下：
git init 
git clone url
git add .
git commit -m ""
git branch 
git branch -a  查看所有分支
git branch -D name
git reflog
git log --graph
git remote -v
git remote add origin url
git remote rm name
git stash list
git stash apply
git stash remove
git push --set-upstream origin name
git remote --all查看本地和远端所有的分支信息


问题及解决办法：
1.使用git时遇到的坑 non-fast-forward
  可能是因为git分支不知道从哪个git服务上拉取代码，所以报错
  git pull origin dev（明确指定服务的远端及分支）
  //处理冲突
  git add  .
  git commit  -m "修改注释"

2.重命名 本地分支
Git branch -m oldbranchname newbranchname

3.git fetch 是什么意思 （出现过本地跟踪到远端库的分支，将远端的分支信息都更新到本地的git上）
上面命令将某个远程主机的更新，全部取回本地