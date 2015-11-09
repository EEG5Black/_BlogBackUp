title: 使用Hexo搭建自己的Blog
date: 2015-10-29 12:16:10
tags: Hexo
---
　　前几天萌生了搭建一个属于自己的博客小站的想法，作为一只码虫，自然想到了就要去实现它。在网上了解了下，一般主流的就是使用`WordPress`或者`OctoPress`来建站，功能是大而全的，但是我并不能用得到，而且据说当到了后期博文多了以后（吹个牛逼先），每次生成发布的速度很慢，考虑了下，我还是准备找一个轻量级的工具（其实是因为需要配置的太繁琐，而且逼格不够高）。后来无意间在一个博主的博客看到他说他从WordPress迁移到了Hexo，而且感觉很好，这不由得让我眼前一亮，于是就有了这个博客以及这篇文章。  
　　扯了这么多没用的，我选择Hexo的原因主要有以下的几点：
+ 首先，最近刚做完了一个`Node.js`的项目，所以对基于Node.js的Hexo比较有好感；
+ 其次，Hexo从生成文章到发布的速度非常快，也就几秒，而且命令简单，只需要一句：`Hexo d -g` 就可以搞定；
+ 再次，支持部署到Github等第三方托管平台，且基本不需要什么额外的命令，简单粗暴。这里需要说明一下，本来我是想把我的Blog搭建在我的VPS上，可是我的VPS是OneTime形式付费购买的，所以我对于安全性和稳定性一直不太敢放心，再一个我的VPS的数据中心在加拿大，所以网速是个大问题，并且只是一个博客而已，静态页面足矣，所以为了访问体验，我最后选择将我的Blog部署到Github上；
+ 最后，Hexo足够简单，却能满足一个博客应有的所有功能，并且支持`Markdown`语法，真是满足了我的一切需求，所以最后我选择了Hexo

　　好了，闲话到此为止，下面我将分享此次的blog搭建过程，以及我在过程中遇到的问题和解决方法，因为网上已经有很多的教程，所以这里我会引用部分，最后会进行标明。

<!--more-->
## Hexo的运行环境及准备工作

　　为了方便我可以随时随地的在各种机器上编写blog，所以我将Hexo安装到了我的VPS上，我的VPS是`Ubuntu 14.04`的系统，所以以下我都是在该操作系统下进行的操作，其他系统情况不做讨论。

#### Node.js

　　Hexo基于Node.js，故我们先安装Node.js到机器上，如果你不确定电脑上是否有Node.js，请输入：`node-v`来查看是否已安装了Node.js，如果有则会显示版本号，否则会提示命令无效。安装[Node.js](https://nodejs.org)，可以移步官网查看相关安装、下载文档等，这里不做过多描述，以下贴出官网提供的Ubuntu的安装方法：  
　　`curl --silent --location https://deb.nodesource.com/setup_4.x | sudo bash -`  
　　`sudo apt-get install --yes nodejs`  
　　安装成功以后则可以输入`node -v`来验证是否成功。如下图：  
　　![Node.js安装成功](http://7xnuga.com1.z0.glb.clouddn.com/Nodejs安装成功.png)

#### Git

　　为了将我们的博客推送到Github上进行展示，我们需要安装Git，安装命令如下：  
　　`sudo apt-get install --yes git`  
　　安装成功以后则可以输入`git --version`来验证是否成功。如下图：  
　　![Git安装成功](http://7xnuga.com1.z0.glb.clouddn.com/Git安装成功.png)

#### Hexo

　　现在准备工作基本就绪，我们可以来安装Hexo了，同样只需要一条命令即可：  
　　`npm install -g hexo`  
　　安装过程可能会报WARN，不用去管他。过程如下图：  
　　![Hexo安装成功](http://7xnuga.com1.z0.glb.clouddn.com/Hexo安装成功.png)  
　　安装成功以后则可以输入`hexo -v`来验证是否成功。如下图：    
　　![Hexo安装成功](http://7xnuga.com1.z0.glb.clouddn.com/Hexo安装成功2.png)

## 开始Hexo

　　到现在为止，Hexo的准备工作我们就已经完成了，下面我们就是开始创建Blog。

#### 初始化

　　这里我将Hexo创建在~/下面，并新建一个blog文件夹（这里根据自己喜好选择），将其放在其中，使用以下命令即可：  
　　`hexo init blog`  
　　初始化完成后它会提示你应该先执行`npm install`，才能启动你的博客，这时需要先进入上一步初始化hexo的文件夹下，再执行该命令，如下：  
　　`cd blog`  
　　`npm install`

#### 启动Hexo

　　初始化完成后，执行 `hexo s` 命令，即可启动（这里有个细节需要注意，所有的hexo的命令都需要在初始化Hexo的文件夹路径下执行，否则将不会成功，例如这里hexo初始化在blog的文件夹下，hexo s的命令就只能cd 到 ~/blog下执行，当然在blog的子文件夹下也可以执行）。结果如下图：  
　　![Hexo启动成功](http://7xnuga.com1.z0.glb.clouddn.com/Hexo启动成功.png)  
　　现在，我们的Hexo就已经启动了，如果是本机，我们可以通过http://0.0.0.0:4000/ 访问，否则请将0.0.0.0替换成IP地址进行访问。当我们打开页面，你会看见简洁的Hexo以及熟悉的Hello World。至此，Hexo已经安装完毕。

#### 部署到Github

　　具体这里可以参考这篇[博客](http://ibruce.info/2013/11/22/hexo-your-blog/)，需要补充的是以下几点：
+ 在按照该Blog设置好SSH Key后，执行`ssh -T git@github.com`，可能会得到如下反馈，`Permission denied (publickey).`，是因为这中间漏了一步：  
  执行`ssh-agent -s`或`eval $(ssh-agent -s)`，  
  然后执行`ssh-add 你的SSH Key保存的地址`添加SSH Key到代理中，这之后再执行`ssh -T git@github.com`，就会得到成功的反馈了  
+ 每次准备提交blog到Github前，都需要执行`ssh-add -l`命令确认代理中有SSH Key，否则还是会得到Github的`Permission denied (publickey).`反馈，不能发布成功，解决该问题的方法是重新执行一遍上一点提到的操作。
+ CNAME文件需要放到~/blog/source/文件夹下，否则每次生成blog的时候会把CNAME删掉。

#### 动手写吧

　　现在，一切就绪，开始动手写我们的第一篇blog吧，执行以下命令创建一篇文章：  
　　`hexo n "文章标题"`  
　　![Hexo文章创建成功](http://7xnuga.com1.z0.glb.clouddn.com/Hexo文章创建成功.png)  
　　需要注意，创建完文章后Hexo并不会直接跳转进文章进行编辑，你需要自己定位到文章的路径下进行编辑，这里不作过多阐述。  

#### 发布

　　文章写好以后我们可以先通过`hexo s`命令，在本机启动预览一下文章效果，当觉得OK没有问题以后我们就可以将其发布到Github上。  
+ 首先我们要修改~/blog文件夹下的_config.yml文件，在其中找到deploy：
+ 在其下的type：后面写上git
+ 在repository：后面写上`git@github.com:你的仓库地址`，保存关闭_config.yml
+ 然后执行`npm install hexo-deployer-git --save`命令（以上仅为第一次发布时需要做的工作）
+ 最后执行`hexo d -g`命令，完成发布

　　现在我们在浏览器中访问你的仓库地址，即可看到你的blog了。

#### 主题

　　我使用的是Next的主题，具体内容及使用方式，可以访问iissnan的[Github](https://github.com/iissnan/hexo-theme-next)

#### 绑定域名

　　如果你有域名的话，请自行上网google，如何将Github和域名绑定，我实在是太懒了，写了这么多我自己都惊呆了。。。之后有空我会继续补充

## 感谢

　　如果你看到了这里，我感觉十分的欣慰，希望我的文章能对你有所帮助，我在搭建Hexo的时候参考如下几篇博文，所以我的这篇文章自然也引用了其中大部分内容，特此注明：  
　　[博客：不如](http://ibruce.info/2013/11/22/hexo-your-blog/)  
　　[简书：CnFeat](http://www.jianshu.com/p/05289a4bc8b2)  
　　[ITnose](http://www.itnose.net/detail/6231502.html)

