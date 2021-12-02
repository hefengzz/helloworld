# Git

用来管理和维护代码版本管理工具

SVN是集中式的版本控制，也就是一个中央服务器。

Git是分布式版本库，有一个本地仓库和一个远程仓库。独自开发时可以使用本地仓库，需要和其他人共享代码时，可以将代码push到远程仓库。

原理：左边从下往上。

1. 添加文件到暂存区
2. 提交至本地仓库
3. 提交到远程仓库

原理：右边从上往下

 1. 下载文件到本地仓库
 2. 文件回滚到暂存区
 3. 文件从暂存区清除

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020112511360362.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzU5MTk4MA==,size_16,color_FFFFFF,t_70#pic_center)

- **Workspace**：工作区，就是你平时存放项目代码的地方
- **Index / Stage**：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- **Repository**：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- **Remote**：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

# 首次使用

首次使用需要创建本地仓库，以便闭环开发使用

**第一步，初始化：**

1. 第一种：
	1. 创建仓库目录
	2. 在gitbash命令行中输入「git init」初始化仓库
	3. 随后目录下会生成一个隐藏目录「.git」

2. 第二种：
	1. 创建仓库目录
	2. 右键点击「git GUI here」
	3. 选择你的仓库目录
	4. 随后目录下会生成一个隐藏目录「git」

**第二步，配置：**

1. 配置用户名「git config --global user.name "名字"」

2. 配置邮箱「git config --global user.email "邮箱@.com"」

3. 输入「git config --global --list」，查看配置的全局用户信息

	![image-20210327230932725](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327230932725.png)





# 本地仓库

1. 将文件上传到暂存区，使用命令「git add hello.txt」

	![image-20210327223601054](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327223601054.png)

2. 查看暂存区待提交的文件，使用命令「git status」

	![image-20210327223633235](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327223633235.png)

3. 将暂存区的文件提交至本地仓库，并为文件添加了注释。使用命令「git commit  -m "first commit by zephyr" hello.txt」

	![image-20210327224537182](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327224537182.png)

4. 再次查看暂存区是否已经清空了，没有任何需要提交的东西了

	![image-20210327224623963](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327224623963.png)

5. 查看本地仓库提交的日志，使用命令「git log」

	![image-20210327224840658](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210327224840658.png)

	Author 是作者信息，用户名，邮箱

	Date 是提交的时间

	然后是你提交时为文件添加的注释



# 远程仓库

1. 在C盘用户目录下找到「.ssh」目录，没有自己创建

2. 使用命令生成ssh秘钥「ssh-ketgen -t rsa」，然后回车四次

	![image-20210328000133980](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210328000133980.png)

3. 查看目录下是否生成了两个文件

	![image-20210328000212154](C:\Users\HH\AppData\Roaming\Typora\typora-user-images\image-20210328000212154.png)

	