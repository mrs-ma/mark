

# Linux(CentOS)安装nodejs

参考https://www.cnblogs.com/sirdong/p/11447739.html

因为需要安装12.13.1版本的，需要简单改下具体的命令，如下

```bash
#养成一个好习惯，建立一个独立的目录
mkdir web
cd web
#下载安装包
wget https://nodejs.org/dist/v12.13.1/node-v12.13.1-linux-x64.tar.xz
#解压安装包
tar xf node-v12.13.1-linux-x64.tar.xz 
# 注释掉的这些命令是为了查看是否安装成功的
# ls node-v12.13.1-linux-x64 如果有bin和npm说明成功安装了

# 接下来需要修改一下环境变量，以方便直接运行node命令
# 养成修改重要文件之前先备份的好习惯
cp /etc/profile /etc/profile.bak
# 打开profile文件，并在在最下面添加一行 export PATH=$PATH: 后面跟上node下bin目录的路径
vim /etc/profile
# GG 跳转到文首
# shift+G 跳转到文末
# i 进入文件编辑模式
# 文末添加下面这一行：
# export PATH=$PATH:/root/web/node-v12.13.1-linux-x64/bin
# ESC 退出编辑模式
# :wq 连续输入保存并退出文件。  多学一点，不小心改错了的话，:q!不保存退出。

# 使配置文件立即生效
source /etc/profile
# 查看是否可以成功运行
node -v

```



# 部署服务

https://www.onlinedown.net/soft/618043.htm  安装xftp5 产品密钥：101210-450789-147200

`目标`：

​	通过node创建http服务器运行项目

`步骤`：

1. 在桌面创建prorun目录

2. 把dist打包文件复制给prorun目录

3. 给prorun目录执行  npm  -y  init  生成 package.json文件

4. 给prorun目录执行 npm i express  安装需要的依赖包

5. 给prorun目录 创建  app.js文件 ，内容如下：

   ```js
   // 通过express创建一个http服务
   // 引入express
   var express = require('express')
   
   // 创建express实例化对象
   var app = express()
   
   // 设置dist目录被托管(运行内部的文件)
   app.use(express.static('./dist'))
   
   // 创建http服务
   app.listen(16677,function(){
     console.log('项目已经运行，具体在\n\nhttp://127.0.0.1:16677')
   })
   
   ```

6. 执行命令  node  app.js  运行项目

现在项目就可以执行了

在后台启动服务：`nohup node app.js > run.log 2>&1 &`



# Windows共享文件夹

参考：https://jingyan.baidu.com/article/b2c186c83a1642c46ef6ffc2.html

1.如何设置共享

cmd命令`ipconfig`可以查看本地ip地址。

win7共享文件夹参考：https://baijiahao.baidu.com/s?id=1606700126172760134&wfr=spider&for=pc

win10共享文件夹参考：https://jingyan.baidu.com/article/358570f6633ba4ce4624fc48.html



2.如何访问共享

访问其他电脑上的共享文件夹，输入IP地址`\\192.168.0.xxx`,弹出输入用户名密码

