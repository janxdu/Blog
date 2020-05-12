---
title: Windows下部署YAPI完全指南
categories: Front End
date: 2018-03-21 00:00:00
---

由于React框架前后端分离的实践，需要方便地管理前后端交互的API、mock数据。根据网上开源的RAP2、YAPI、Easy Mock等项目，发现YAPI能优雅实现我们的需求。故先尝试在Windows下部署YAPI，验证功能可用性。
YAPI依赖Node.js和mongodb环境。
### 安装Node.js（7.6+)
推荐使用nvm管理node版本，使用PowerShell代替console。
```powershell
$ git clone git@github.com:creationix/nvm.git ~/.nvm
$ source ~/.nvm/nvm.sh
# 安装目前最新稳定版本
$ nvm install v8.10.0
# 如存在多版本node则需要切换使用的版本
$ nvm use 8.10.0
```
> 如果node版本过低，后续通过yapi-cli安装yapi时可能会报async/await无法解析的异常，因为低版本不支持此语法。

### 安装mongodb（2.6+）
在[mongodb官网](https://www.mongodb.com/download-center?jmp=nav#community)下载安装包并安装。
>安装mongodb compass可视化工具时可能由于下载失败导致整体失败，此时可取消安装compass组件，后续若有需要自行下载。

```powershell
# 设置dbpath
$ D:\yourPath\mongodb\bin\mongod --dbpath D:\yourPath\mongodb\data\db
# 启动mongo
$ D:\yourPath\mongodb\bin\mongo.exe
```
可以把mongodb作为系统服务启动，由于本地部署资源有限，暂不讨论此做法。
mongod默认无用户名和密码，常用命令:
```powershell
# 查看数据库
$ show dbs
# 创建数据库(新建的数据库不在数据库列表中，要插入一条数据才会展示)
$ use dbname
# 插入数据
$ db.dbname.insert({"name":"value"})
```

### 安装YAPI
[官方有2种安装方式](https://yapi.ymfe.org/devops.html#安装)，由于众所周知的原因，按照可视化部署比较容易失败，此介绍命令行部署的方式。在[yapi项目的github主页](https://github.com/YMFE/yapi)下载zip包并解压到本地文件夹。
```powershell
# 切换到zip解压的文件夹下
$ cd yapi/vendors
$ cp config_example.json ../config.json
$ npm install --production --registry https://registry.npm.taobao.org
```
设置config.json的db节点下的配置，可在mongodb命令行工具新建数据库，默认用户名和密码均为空。
```json
{
  "port": "3000",
  "adminAccount": "admin@admin.com",
  "db": {
    "servername": "127.0.0.1",
    "DATABASE":  "test",
    "port": 27017,
    "user": "",
    "pass": ""
  },
  "mail": {
	  /*省略，可暂时不配置*/
    }
  }
}
```
最后就可以安装server并启动项目了。
```powershell
# 安装yapi server
$ npm run install-server
# 启动
$ node server/app.js
```
最后是启动效果图。
![@登录默认用户后创建一个简单接口示例](http://ojs1n6jlb.bkt.clouddn.com/1521617828719.png)




