当前来讲，版本控制器越来越多 功能也越来越强，以前使用的svn 已经不再能满足当前的需求了，git 会更加适用于项目的开发。
在搭建git服务器之后，需要将加入git服务器的用户添加到服务器中，每个用户在加入服务器之前。需要将自己机器上的 ssh key传到服务器上。

自己机器上的ssh key在于自己的系统盘中 ---> 用户---->计算机名字 --->.ssh目录下  的id_rsa.pub，使用文本打开，这里就是ssh key

之前搭建的git 环境，在以后添加仓库的时候，直接 使用git clone 地址，就可以将仓库添加到本地了。

git的使用参考之前的写的笔记。