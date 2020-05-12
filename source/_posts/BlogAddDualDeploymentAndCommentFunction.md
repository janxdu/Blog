---
title: 博客双部署及引入评论功能
date: 2018-05-28 00:00:00
---
博客原来部署在Github Pages上，由于众所周知的原因，访问速度十分不稳定，严重影响阅读体验。而且由于第三方的评论平台一直在不断关闭，所以一直没有引入评论功能。这次把它们一起解决。

### 部署到Coding.net
1、创建项目。在Coding.net创建一个项目名为 yourname.coding.me 的项目（yourname为实际用户名）。在该项目的代码tab页，勾选快速初始化（生成README.md），选择默认分支master。
2、SSH Key生成及部署。由于我的Coding.net账户和Github账户绑定同一邮箱，想复用原来的Key，但是passphrase已经忘记了，无奈需要创建一个新Key，passphrase设置为空。本地命令行执行以下命令
```
// 生成SSH Key
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
// 可自定义Key文件名
$ Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
// 可输入passphrase
$ Enter passphrase (empty for no passphrase): [Type a passphrase]
$ Enter same passphrase again: [Type passphrase again]
// 将公钥复制到剪贴板
$ pbcopy < ~/.ssh/id_rsa.pub
```
拿到公钥之后就可以到Coding.net的账户-SSH公钥tab页新增公钥配置了。配置完成后本地验证连通性，如果结果为success即部署成功。

```
$ ssh -T git@git.coding.net
```
1、Hexo配置更新
我使用Hexo模版引擎生成静态博客，本身支持多部署。修改本地项目仓库的_config.yml的deploy参数
```
deploy:
  type: git
  repo: 
    github: git@github.com:your_name/your_name.github.io.git,master
    coding: git@git.coding.net:your_name/your_name.coding.me,master
```
2、正常部署Hexo验证结果
```
$ hexo d
```
### 引入Disqus评论
由于博客没有备案，无法使用搜狐畅言的评论系统。故选择国外的Disqus，比较稳定。其官网需要科学上网才能访问，使用很方便，新建一个Disqus并设置Website Name即可。
本地项目使用了Next主题，本身支持Disqus评论，只需配置主题下_config.yml的disqus参数即可。
```
disqus:
  enable: true
  shortname: your_shortname
  count: true
```
此次双部署及评论引入中间还遇到Https失效，主题升级后样式错误等问题。最终都得以解决，还是一个很有意义的过程。