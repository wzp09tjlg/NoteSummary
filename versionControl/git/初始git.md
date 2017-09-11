git现在是越来越火，功能也越来越强大。下面来认识下git吧。
1.安装，我是window 64位的系统，安装选择相应的安装文件。
2.本地初建仓库
 首先需要设置用户名 git config --global user.name "wzp09tjlg"
在设置邮件                 git config --global user.email "wzp09tjlg@163.com"
 
然后查看是否存在ssh key
命令行为 cd  ~/.ssh 
生成秘钥： ssh-keygen -t rsa -C "wzp09tjlg@163.com"
摁三个回车键，密码为空

然后就可以得到两个文件，在.ssh/目录下 id_rsa 和 id_rsa.pub文件

一：
如果是希望在github上上传本地的项目，就需要用到id_rsa.pub中的ssh key
首先需要一个github账号，然后再github上创建一个repository,修改title及描述。然后需要添加ssh key
最后在本地的git仓库中 使用命令行
 git remote add origin https://github.com/wzp09tjlg/testForPushFile.git  
关联远程仓库，
git push -u origin master
将本地仓库中的文件推到github上
然后就可以在github上的项目了

二：
如果是希望从服务器上下载项目到本地，需要执行的命令是
git clone git://git.kernel.org/pub/scm/git/git.git  "需要指定的目录"

本地仓库和远程服务的仓库没有关系，远程仓库可以通过clone下载到本地，然后本地会新建服务器上的一个副本在本地。这样就和服务器上的仓库关联上了。
