# 使用hugo搭建网站

# 前言
&emsp;&emsp;HUGO 是一套模版静态化的系统，了解其目录结构有助于创建我们的网站系统，下面我分享以下我的搭建过程，希望对大家有点帮助～
## 一、hugo的安装与配置
安装hugo我是直接用的这条命令（截止这篇文章完结之时，这是最新的hugo版本）
```markdown
wget https://github.com/gohugoio/hugo/releases/download/v0.108.0/hugo_0.108.0_Linux-64bit.tar.gz
```
安装完成后需要解压
```markdown
tar -zxf hugo_0.108.0_Linux-64bit.tar.gz
```
解压完成后使用这条命令查看是否安装成功
```markdown
hugo version
```

![](/images/jietu10.png)

## 二、开始使用hugo搭建网站
### 1、创建我们的博客目录
```markdown
hugo new site mysite
```
### 2、下载主题

去主题官网https://themes.gohugo.io,找到想要的主题，我的主题是LoveIt。

![](/images/jietu15.png)

### 3、创建我的第一篇文章

![](/images/jietu16.png)

### 4、在本地启动博客

在mysite目录下命令：
```markdown
hugo serve --buildDrafts
```
就可以去本地查看到自己的博客啦！

![](/images/jietu17.png)

### 5、在github上部署hugo

首先我们需要在github中创建一个仓库，名字必须为github的用户名+github.io为后缀(图片中警告的原因是我已经创建过这个仓库了)!

![](/images/jietu18.png)

用hugo生成网页，托管到Github仓库中
```markdown
hugo --theme=LoveIt --baseUrl="https://zhengqinjie11.github.io/" --buildDrafts
```
注意:theme后面为主题的名字！且在执行完这条语句之后，会在当前目录下生成对应的public文件，最后我们需要将public推送至远程github！

### 6、将public推送至远程github
```markdown
cd public
git init
git add .
git commit -m "push"
git branch -M main
git remote add origin + .....git
git push -u origin main
```
如图，public推送成功！

![](/images/jietu19.png)

在github上也可以看见推送成功的文件，如图：

![](/images/jietu20.png)

现在我们可以访问我们刚刚部署的网站了，访问zhengqinjie11.github.io

![](/images/jietu21.png)


