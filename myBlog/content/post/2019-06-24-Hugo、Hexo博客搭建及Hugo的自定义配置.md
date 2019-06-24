---
title: "Hugo、Hexo博客搭建及Hugo的自定义配置"
date: 2019-06-24T09:50:50+08:00
draft: false
tags: ["hugo","hexo"]
categories: ["blog"]
---

## 1 Hugo介绍
&emsp;&emsp;世界上最快的网站构建框架。

&emsp;&emsp;`Hugo`是最受欢迎的开源静态站点生成器之一。凭借其惊人的速度和灵活性，`Hugo`使建筑网站再次变得有趣。

&emsp;&emsp;[Hugo官网](https://gohugo.io/)

## 2 Hugo及主题的安装
&emsp;&emsp;[安装教程](https://github.com/factory011/factory011.github.io)

&emsp;&emsp;[在线预览](https://factory011.github.io/)

## 3 通过配置文件deploy.sh实现一键部署到GitHub
（a）`deploy.sh`文件放在站点根目录下；

（b）执行方法分两种（`windows`下）：

* 方法一：站点根目录下，鼠标右键，打开`git bash here`窗口，执行`sh deploy.sh`。
* 方法二：选中`deploy.sh`文件，鼠标右键属性，更改打开方式，将打开方式选择为`git-bash.exe`执行文件，以后写新的文章后，双击下脚本文件即可成功推送到`github`上。
   	
```js
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace by `hugo -t <yourtheme>`

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back
cd ..
```

## 4 Hexo介绍
&emsp;&emsp;快速、简洁且高效的博客框架。

&emsp;&emsp;[Hexo官网](https://hexo.io/zh-cn/)

## 5 Hexo及主题的安装
&emsp;&emsp;[Hexo搭建教程](https://www.cnblogs.com/factory/p/10566462.html)

&emsp;&emsp;[Hexo的next主题安装](https://www.cnblogs.com/factory/p/10567649.html)

&emsp;&emsp;[在线预览](https://liangh.top/)

## 6 从hexo转移到hugo框架
&emsp;&emsp;原因如下：

&emsp;&emsp;（a）之前的`hexo`配置了一些动态背景、评论功能等等，但是后来不想要这些功能（看着比较炫酷，但是没什么实际用处），要调整的话需要到处找文件改配置，比较麻烦；

&emsp;&emsp;（b）经过`github`、`coding`双线部署，静态文件压缩，配置`CDN`后，感觉页面加载速度还不是很快；

&emsp;&emsp;（c）自定义配置的话需要在站点配置、主题配置来回搞，还是嫌麻烦。

## 7 hugo字体图标自定义配置
&emsp;&emsp;[阿里巴巴矢量库](https://www.iconfont.cn/)

&emsp;&emsp;打开图标管理 -> 我的项目 -> `hugo-blog`，将选择好的图标加入购物车，加入项目，修改下图标的名称（名称改为`icon-xxx`）、大小和颜色。

然后点击下载至本地，解压后目录结构如下。

```js
--demo.css
--demo_index.html 
--iconfont.css
--iconfont.eot
--iconfont.js
--iconfont.svg
--iconfont.ttf
--iconfont.woff
--iconfont.woff2
```

将hugo的themes\even\src\fonts\iconfont目录下的4个文件用上一步下载的对应文件替换掉。

```js
└─fonts
    └─iconfont
          --iconfont.eot
          --iconfont.svg
          --iconfont.ttf
          --iconfont.woff
```



打开`themes\even\src\css\_iconfont.scss`文件。

将`/* Social Icon */`下方的只有`content`属性的css样式用下载文件中对应的`iconfont.css`文件对应内容来替换掉。

修改的配置不能立即生效，我们重新编译打包主题文件。因此需要先安装  [Node.js](https://nodejs.org/en/)和[Yarn](https://yarnpkg.com/zh-Hant/) ，安装`Node.js`后，`Yarn`的快速安装方法。

```js
# npm install -g yarn
```

检查`Node.js`和`Yarn`是否安装成功。

```js
# node -v
# npm -v
# yarn --version
```
命令执行后都能查到版本号，说明安装成功。

主题文件的依赖安装和打包。

```js
# cd ./themes/even/
# yarn install
# yarn build
```
## 8 给菜单项加上好看的图标
将`themes\even\layouts\partials\header.html`里的`partials\header.html`文件结构复制到站点根目录下的`layouts`中，对站点根目录下`layouts\partials\header.html`文件对应内容

```html
<a class="menu-item-link" href="{{ .URL | safeURL }}">{{ .Name }}</a>
```

修改为

```html
<a class="menu-item-link" href="{{ .URL | safeURL }}"><i class="iconfont icon-{{ .Identifier }}"></i>{{ .Name }}</a>
```

根据站点根目录下`config.toml`文件中的`identifier`属性匹配字体图标名称。

图标显示出来后感觉和字距离太近了，可以调整下`css`样式，配置下站点根目录下的`config.toml`文件，启用自定义css文件。

```js
customCSS = ['custom.css']
```

配置站点根目录`/static/css/custom.css`文件（注意这是`css`文件，不要将`themes`中的`scss`样式直接复制过来改改，会报错），自定义`custom.css`、`custom.js`可以覆盖主题里设置的`scss`、`js`，这样我们可以不用去改动主题文件，方便以后对主题的切换。

```css
/* 设置菜单栏icon偏移位置 */
.menu-item-link .iconfont::before {
	padding-right: 8px;
}
```
## 9 完整的custom.css文件，需要改动样式的可自定义
```css
/* =============================== custom.css ================================== */
/* 去除顶部border */
body {
	border-top: 0;
}

/* 设置版心 */
.container {
	width: 800px;
	margin: 0 auto;
}

/* 设置a标签样式 */
a {
	color: rgba(139,69,19,0.8);
}

/* 设置文章目录单行省略 */
.toc-link {
	display: inline-block;
	width: 100%;
	overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

/* 设置页面最小高度，我的电脑100vh为722.4，window.innerHeight为722，导致出现了一小段垂直滚动条，网上说清除body的margin解决不了这个问题，然后我用了calc减去10px刚好，兼容ie9+ */
.slideout-panel {
    min-height: calc(100vh - 10px);
	background-color: #f5f5f5;
}

/* 设置main最小高度，保证标签、分类页面的footer在底部 */
.main {
	min-height: 453px;
}

/* ================================ 设置header样式 ============================== */
.header {
	padding: 10px;
	background: -webkit-linear-gradient(200deg, #FFFFFF 0%, #EBEBEB 80%); /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(200deg, #FFFFFF 0%, #EBEBEB 80%); /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(200deg, #FFFFFF 0%, #EBEBEB 80%); /* Firefox 3.6 - 15 */
    background: linear-gradient(200deg, #FFFFFF 0%, #EBEBEB 80%); /* 标准的语法（必须放在最后） */
}

/* 设置菜单项hover样式 */
.header .site-navbar .menu .menu-item:hover {
    background-color: #CCCCCC;
	border-radius: 6px;
}

/* 设置title字体大小 */
.header .logo-wrapper .logo {
	position: relative;
    font-size: 36px;
    line-height: 68px;
}

/* 设置title上横线 */
.header .logo-wrapper .logo::before {
    content: '';
    position: absolute;
	top: -10px;
	left: 27px;
    width: 160px;
    height: 2px;
    background-color: #333;
}

/* 设置title下横线 */
.header .logo-wrapper .logo::after {
    content: '';
    position: absolute;
	bottom: -10px;
    left: 0;
	left: 27px;
    width: 160px;
    height: 4px;
    background-color: #333;
}

/* ========================= 设置菜单栏icon偏移位置 ================================ */
.menu-item {
	padding: 0 10px;
}

.menu-item-link .iconfont::before {
	padding-right: 8px;
}


/* ============================== 调整阅读更多样式 ======================================= */
.post .post-content .read-more .read-more-link {
    border: 2px solid #222;
    padding: 0.5em 1em;
    background-color: #222;
    color: #fff;
}

.post .post-content .read-more .read-more-link:hover {
    border-bottom: 2px solid #222;
	color: #222;
    background: #fff;
}

/* 去除文章border-bottom */
.posts {
	border-bottom: none;
}

/* 设置文章盒子阴影 */
.post {
	padding: 1em 1em;
    margin: 1.5em 0;
	box-shadow: 0 8px 8px rgba(10,16,20,.24), 0 0 8px rgba(10,16,20,.12);
	-webkit-box-shadow: box-shadow: 0 8px 8px rgba(10,16,20,.24), 0 0 8px rgba(10,16,20,.12);
}

/* 设置文章目录的ul样式 */
.post .post-toc .post-toc-content ul {
    list-style: telugu;
}

/* 设置文章标题hover样式 */
.post .post-header .post-link:hover {
    background-color: #CCCCCC;
	padding: 1px 10px;
	border-radius: 6px;
}

/* 设置文章代码片段样式 */
.post .post-content code, .post .post-content pre {
    background: none; 
}	

/* 让阅读更多居中 */
.read-more {
	text-align: center;
	padding: 0 0 20px;
}

/* 调整返回顶部icon位置和大小 */
.back-to-top {
    right: 30px;
    bottom: 45px;
    font-size: 2em;
}

/* ============================= 设置菜单项的标签、分类页面样式 ===================================== */
.terms .terms-tags .terms-link {
    margin: 10px 10px;
    border-radius: 50em;
    padding: 5px 10px;
    background-color: #FFF2AB;
}

/* 设置菜单项的标签、分类页面的统计数字样式 */
.terms .terms-tags .terms-link .terms-count {
    top: -2px;
    right: -1px;
    display: inline-block;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #B45B3E;
    color: #fff;
}

/* ========================= 设置底部heart跳动样式动画 =============================== */
.footer .copyright .copyright-year .heart {
    color: #ff7171;
	display: inline-block;
	animation: heartAnimate 1.33s ease-in-out infinite;
}

@keyframes heartAnimate {
	0%, 100% {
    transform: scale(1);
	}

	10%, 30% {
		transform: scale(.9);
	}
	20%, 40%, 60%, 80% {
		transform: scale(1.1);
	}
	50%, 70% {
		transform: scale(1.1);
	}
}
```