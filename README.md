## 介绍

---

### 平台：HEXO

hexo是一款基于Node.js的静态博客框架。它的依赖库很少，易于安装，很方便我们在不同的设备上进行博客项目的部署。

### 文章：技术相关

与本人工作相关的技术型文章，学习交流使用。

## 操作

---

### 配置git

【Windows下操作】
1. 安装git bash到Windows：[git for windows](https://gitforwindows.org/)
2. 配置`user.name`和`user.email`信息：

```bash
git config --global user.name "<github用户名>"
git config --global user.email "<邮箱>"
ssh-keygen -t rsa -C "<上面的邮箱>"
```

3. 到C:/Users/\<admin\>/.ssh/中把`id_rsa.pub`复制到GitHub设置中；
4. 测试网络连通性：

```bash
ssh -T git@github.com
```



### 安装Node.js和HEXO

1. 安装Node.js，[Node.js](https://nodejs.org/zh-cn/)，注意包含环境变量和npm；
2. 可在cmd中输入指令测试是否安装成功：

```bash
node -v
npm -v
```

3. 安装hexo，输入：

```bash
npm install -g hexo-cli
```



### 项目

1. 获取项目


```bash
git clone https://github.com/Lucky-Jenny/twyz-blog.git

```

2. 编译项目

```bash
hexo g       # hexo generate   生成网页
hexo d       # hexo deploy  部署到GitHub中
hexo clean   # 清除"public"目录，即清除缓存
```



## 结构

### branch

- \<master\> : 存放hexo博客源码，包括各种配置和文章内容；
- \<gh-pages\> : hexo生成网页后部署到这里，后台page设置与域名绑定；
- \<init-br\> : hexo初始化状态，暂无他用；

### 使用

- 对项目的所有改动操作都在\<master\>中；
- 文章放在`./source/_posts/`下，文章的一些标签信息在头部写清楚：

```markdown
---
title: Markdown语法介绍
date: 2021-05-02
tags: Markdown
categories: grammar
summary: 作为一款适用于代码与issue简述的编辑插件，Markdown一直深受程序员的喜欢。
---
```

- 这里使用的风格是`matery`，它也有专门的yml文件，不要跟主目录的配置文件搞混淆；



### 目录

```txt
.
|-- scaffolds
|   |-- draft.md
|   |-- page.md
|   `-- post.md
|-- source                     # 存放各种文章的目录，每个文件夹对应不同的模块
|   |-- 404
|   |   `-- index.md
|   |-- about
|   |   `-- index.md
|   |-- categories
|   |   `-- index.md
|   |-- pics
|   |   `-- ptr-figure.png
|   |-- _posts                 # _posts是HEXO默认的，即编辑者的文章应放置在这里。
|   |   |-- hello-world.md
|   |   |-- Markdown.md
|   |   `-- pointer.md
|   |-- tags
|   |   `-- index.md
|   `-- CNAME
|-- themes
|   `-- hexo-theme-matery      # 我喜欢的风格，是由国内前端工程师"极狐"开发的
|       |-- languages          # 支持英文、简体(繁体)中文
|       |-- layout
|       |-- source
|       |-- CHANGELOG.md
|       |-- _config.yml        # 这是整个博客插件的核心配置文件，使用非常方便
|       |-- LICENSE
|       |-- README_CN.md       # 使用文档_中文版
|       `-- README.md
|-- _config.landscape.yml
|-- _config.yml                # HEXO的核心配置文件，是全局的配置。
|-- package.json
`-- package-lock.json
```
