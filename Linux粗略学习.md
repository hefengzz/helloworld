在Linux Terminal中，没有出现报错，就表示操作成功。



> 关机指令

```bash
sync	# 将数据由内存同步到硬盘中
shutdown	# 关机
shutdown -h -now	# 立刻关机
shutdown -h -18:00	# 下午6点关机
shutdown -h +10	# 十分钟后关机
rebot	# 重启
halt	# 关闭系统
```

`不管是「重启」「关闭系统」还是「关机」都要先运行sync命令，把内存中的数据写到磁盘中`

> 目录结构

1. 在linux中一切皆文件。
2. 根目录「/」，所有的文件都挂载在这个节点下。

```bash
pwd	# 显示当前所在目录
mkdir # 创建目录
mkdir -p	# 创建多级目录
rmdir	# 删除目录
rmdir -p	# 删除多级目录

cp 源文件 目的文件 # 拷贝文件
mv 源文件 目的文件 # 用于移动位置或重命名
```

> `rm` 移除文件或者目录非常危险的命令！！！