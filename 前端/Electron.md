# 简介

Electron是用来开发桌面端的技术

它是由chromium + node.js + native API组成的



# 安装失败？

`这是个大坑一定要牢记！！！`

`这是个大坑一定要牢记！！！`

`这是个大坑一定要牢记！！！`

`npm config` 设置这俩个

```
ELECTRON_MIRROR=http://npm.taobao.org/mirrors/electron/
ELECTRON_CUSTOM_DIR=8.0.3 (版本号)
```

下面这个8.0.3改成你要下载的`electron`的版本



# Hello World

1. 首先，创建一个目录。
2. 在目录下创建 ==main.js== 和 ==index.html==
3. 在目录使用终端命令 「npm init -y」初始化环境，「-y」是同意所有	
4. 添加electron依赖，在目录终端运行命令「npm i -D electron」

**看完第四点会来看这段：**在添加依赖时，由于大陆网络环境原因，会出现安装到一半卡死不动了，或者根本安装不了，报错之类的情况。这个时候就需要设置**镜像源**，具体请看「安装失败？」

**运行：**初始环境搭建好了之后，在终端使用命令「electron .」运行，如果是局部安装请使用「npx electron .」

