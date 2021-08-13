---
title: hexo-github-yuque个人博客搭建
urlname: pdzf8d
date: '2021-08-13 11:34:35 +0800'
tags: []
categories: []
---

想拥有一个属于自己的博客吗？整理并记录日常工作生活中的点滴，还可以分享给世界各地的朋友，让更多的人认识和了解你。未完待续吧，总之懂得自然懂。

# 基础

hexo 是一个快速，简介且高效的博客框架，更重要的是居然是免费的。使用 hexo 可以迅速建立属于你的博客，可以是本地的，也可以是网络的。hexo 中有很多的主题和插件可以选择，[https://hexo.io/zh-cn/](https://hexo.io/zh-cn/) 这里是官网。

## 准备环境

### git

1. 官网下载 [https://gitforwindows.org/](https://gitforwindows.org/)，一路 next 安装，很简单的，完全默认就可以。
1. 连接 github 和本地 git.

首先右键打开 git bash，然后输入下面命令,把<username>和<email>替换成你自己的。

```shell
git config --global user.name "<username>"
git config --global user.email "<email>"
```

用户名和邮箱根据你注册 github 的信息自行修改。
然后生成密钥 SSH key：

```shell
ssh-keygen -t rsa -C "<email>"
```

打开[github](https://link.zhihu.com/?target=http%3A//github.com/)，在头像下面点击 settings，再点击 SSH and GPG keys，新建一个 SSH，名字随便。
git bash 中输入

```shell
cat ~/.ssh/id_rsa.pub
```

将输出的内容复制到框中，点击确定保存。
输入 ssh -T git@github.com，如果如下图所示，出现你的用户名，那就成功了。

打开博客根目录下的\_config.yml 文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。
修改最后一行的配置：
deploy: type: git repository: https://github.com/godweiyang/godweiyang.github.io branch: master
repository 修改为你自己的 github 项目地址。

### nodejs

官网下载 [https://nodejs.org/en/download/](https://nodejs.org/en/download/)，我选的是 windows LTS 长期支持版本 `Windows Installer (.msi) 64位`，也是默认安装就可以。

### hexo

随便找一个地方，右键选择`Git Bash Here`,进入了 git 的命令行模式。输入下面命令

```shell
安装方式：打开命令提示符窗口，执行下面的命令，全局和局部安装，选择其一即可
# 全局安装
npm install -g hexo-cli
```

## 体验本地博客

软件都安装了，现在来体验一下如果使用 hexo 创建一个本地博客吧.

```shell
#创建一个hexo-github-yuque文件夹，并初始化成hexo工程
hexo init hexo-github-yuque
#构建和运行hexo服务
hexo g && hexo s
```

现在可以按照提示，访问本地连接 [http://localhost:4000/](http://localhost:4000/) 了，就可以看到默认生成的博客长什么样子了。

## 上传到 github，可以在线访问了

到现在为止，hexo 已经可以在本地运行了，但是怎么能让其他人通过互联网访问你的博客呢。接下来就开始了。
这里需要用到 github pages 功能，当前你可以不需要知道 pages 是什么，继续跟着操作就可以了。

1. 登录 github，创建一个仓库，这里仓库的名称要注意，要遵循这个格式`<username>.github.io`,username 是你的 github 的账户名。
1. 修改本地的 \_config.yml,就在刚刚创建的 hexo-github-yuque 路径下。

a. 找到`url:`，把后面的地址替换成你 github 的地址，如 `https://<username>.github.io`
b. 找到`deploy:`，替换成下面的内容，注意这里的<username>也是你的 github 的账户名。

```shell
deploy:
  type: git
  repo: git@github.com:<username>/<username>.github.io.git
  branch: master
  message: "{{ now('YYYY-MM-DD HH:mm:ss') }}"
```

3. 安装 hexo-deployer-git

```shell
npm install hexo-deployer-git --save
```

4. 上传到 github 中

```shell
hexo g && hexo d
```

5. 快试一下吧，线上博客可以访问了，浏览器访问网址 <username>.github.io
6. 之前的步骤已经将博客上传到了 github 中的 master 分支上，还需要将 hexo 工程上传，下次就可以直接在原有基础上修改了，就不用重复之前的操作了。先添加一个`.gitignore`文件，内容如下。

```shell
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
.idea/
```

再执行命令，上传 hexo 工程到 src 分支

```shell
git init
git remote add origin git@github.com:<username>/<username>.github.io.git
git add .
git commit -m "Init commit"
git branch -M src
git push origin src
```

## 雨雀来了

雨雀提供了在线编写 markdown 文档的功能，并且简单易用，无需安装任何环境，直接从浏览器访问雨雀官方，登录后就可以在线编写文档。
这里利用雨雀的功能，通过雨雀编写文档，然后使用`yuque-hexo`从雨雀下载文档，然后通过`hexo`上传到 github 中。

1. 修改`package.json`,增加下面的内容

```shell
,
  "yuqueConfig": {
    "baseUrl": "https://www.yuque.com/api/v2",
    "login": "dlnuxjy", #这里是雨雀的login
    "repo": "myblog", #雨雀的路径
    "mdNameFormat": "title",
    "postPath": "source/_posts/yuque",
    "cachePath": "yuque.json",
    "adapter": "hexo",
    "token": "雨雀TOKEN", #这里也要替换
    "onlyPublished": true,
    "onlyPublic": true
  },
   "scripts": {
    "clean": "hexo clean",
    "clean:yuque": "yuque-hexo clean",
    "deploy": "yuque-hexo sync && hexo deploy",
    "publish": "npm run clean && npm run deploy",
    "dev": "hexo s",
    "sync": "yuque-hexo sync",
    "reset": "npm run clean:yuque && npm run sync"
  },

  "devDependencies": {
    "yuque-hexo": "^1.6.5"
  }
```

2. 从雨雀同步文档，并上传到 github

```shell
npm i -g yuque-hexo
yuque-hexo sync && hexo g && hexo d
```

3. 现在，你的雨雀中 <myblog>里面的文档就上传完成了。
4. 别忘了将 hexo 工程也上次到 github 中的 src 分支中

```shell
git add .
git commit -m "yuque"
git push origin src
```

# 个性化

## 博客标题，子标题，描述，作者，语言怎么设置？

1. 修改`_config.yml`

```shell
# Site
title: 这里写你的标题
subtitle: 这里写你的子标题
description: 这里写你的描述
keywords:
author: 这里写你的名字
language: zh-CN #中文
timezone: '' #时区还是默认吧
```

2. 上传到 github

```shell
yuque-hexo sync && hexo g && hexo d
```

## 换一个主题
