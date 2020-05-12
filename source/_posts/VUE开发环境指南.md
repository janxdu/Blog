---
title: VUE开发环境指南
categories: Front End
tags: [VUE] 
date: 2017-04-07 00:00:00
---
## 一、安装
#### 使用nvm管理node版本
```powershell
$ git clone git@github.com:creationix/nvm.git ~/.nvm
$ source ~/.nvm/nvm.sh
# 安装
$ nvm install v6.10.2
# 显示当前本地安装的所有 Node.js
$ nvm ls 
# 显示服务器所有可用的 Node.js
$ nvm ls-remote
# 本地可用的 Node.js 中使用 6.10.2
$ nvm use 6.10.2
# 设置每次启动默认版本
$ nvm alias default 6.10.2
# 切换npm源
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 更新npm至最新版本
```powershell
$ npm install npm@latest -g
```

## 二、基础工程
### 项目简介
本项目基于[vue-cli](https://github.com/vuejs/vue-cli)项目进行改造，项目地址为[vue-scaffold](https://github.com/janxdu/vue-scaffold)
#### 结构
```
├── build//打包配置文件
├── config//项目配置文件
├── src
│   ├── api//开放接口
│   ├── assets//静态资源
│   ├── components//组件
│   ├── page//页面
│   ├── router//路由配置
│   └── store//状态管理配置
└── test//测试
    └── unit//单元测试
        └── specs//单元测试配置
```
此处不列举node自动编译生成的文件夹。
#### 基本组件
- vue2
- vue-router
- babel
- webpack2
- less
- eslint
- karma+mocha+chai

#### 主要配置文件说明
- `package.json`用于定义项目的基本信息（名称、版本号、组件依赖等），API详见官方文档https://docs.npmjs.com/files/package.json
- `build.js`,产线环境打包配置。
- `webpack.xxx.conf.js`用于配置打包任务（加载器、插件等），针对开发、测试和产线环境区分不同的打包策略。API详见官方文档https://webpack.js.org/configuration/
	- `webpack.base.conf.js`配置入口文件、输出信息、要处理的文件类型、处理完成后的动作、模块处理方式（eslint校验、vue-loader+babel转换vue为ES5、图片字体文件名生成规则、css处理器）
	- `webpack.dev.conf.js`配置热替换插件、html插件、错误提示插件。
	- `webpack.test.conf.js`暂时无特别配置。
	- `webpack.prod.conf.js`配置HTML、JS、CSS、图片、压缩插件，合并JS插件，
## 三、运行项目

从服务器获取基础工程源码，terminal切换到项目根目录下执行
```powershell
$ npm install
```
以开发模式启动项目
```powershell
$ npm run dev
```
以产品模式启动项目
```powershell
$ npm run build
```
运行单元测试
```powershell
$ npm run unit
```


