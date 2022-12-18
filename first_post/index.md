# 在ubantu中安装和配置git

# 前言
&emsp;&emsp;这是我个人使用ubantu安装和配置git的方法，很方便，安装的版本也比较新，供大家参考～（大部分截图由于未保存丢失，故用代码代替）
## 一、git的安装
### 使用apt安装git
安装非常直接，仅仅以sudo权限用户身份运行下面的命令：

![](/images/jietu1.png)

再运行git命令，打印 Git 版本，验证安装过程，如下图：

![](/images/jietu2.png)

这样子git就安装成功啦！
## 二、配置git
### 1、创建github账号
首先我们需要到[https://github.com/](https://github.com/)上面注册一个属于自己的账号，如图

![](/images/jietu3.png)
### 2、配置用户名和用户邮箱

git config --global user.name "lingyuanyousa"


git config --global user.email "2996298542@qq.com"

### 3、配置git的私匙和公匙

ssh-keygen -t rsa -C "2996298542@qq.com"

其中密码设置为空，再按照指引做就好。

上github打开个人设置，点击new ssh kew，如图：


![](/images/jietu4.png)

终端打开id_rsa.pub文件，复制密钥到github上：


![](/images/jietu5.png)

回到终端测试是否连接成功（如图，已经连接成功）：

![](/images/jietu9.png)

### 4、github创建项目
github创建项目，将远程仓库与本地仓库连接起来（点击new）：

![](/images/jietu7.png)

随后你就可以上传你想上传的文件啦，使用命令：

git init `初始化项目`

git add . `将当前目录下的文件添加到仓库（缓冲区）`

git commit -m "init project" `提交到本地仓库`

git push -u origin master `推送到远程仓库`

## 三、我的第一、二步的实验结果截图：


![](/images/jietu8.png)







