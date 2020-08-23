学习笔记
  https://www.jianshu.com/p/40ffdd0654f4
  https://www.cnblogs.com/alex-415/p/6912294.html
  https://blog.csdn.net/u012145252/article/details/80628451
  当在GitHub中fork了一个项目，如何建立本地仓库与远程仓库的连接
   1.先下载项目到本地
   2.保证对项目内容先不做更改
   3.结合上面两个网址步骤去做
		1. git init //初始化仓库
		2. git add .(文件name) //添加文件到本地仓库
		3. git commit -m "first commit" //添加文件描述信息
		4. git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支
		5. git pull origin master --allow-unrelated-histories// 把本地仓库的变化连接到远程仓库主分支
		6. git push origin master:master //把本地仓库的文件推送到远程仓库
