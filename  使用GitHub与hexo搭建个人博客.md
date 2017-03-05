---
title: 使用Github和hexo搭建个人博客
---

> 对于程序员来说，写博客是一个好的习惯，今天给大家介绍一下怎么使用`github`和`hexo`来搭建一个博客。

使用github的page服务来搭建博客有几个好处：
1. 显得比较有geek范儿，跟是用来csdn等博客平台相比，需要一定的动手与折腾能力
2. 和其他的博客平台相比，可以自己完全控制现实的内容，哪的样式不好看，不喜欢，直接动手改css样式即可，和其他的博客平台满是广告和有点丑爆的界面相比，有一种自己掌控全局的感觉，而不是将自己的东西交给别人托管
3. 写博客来说毕竟还是要稳定比较好，虽然说自己也可以写一个博客系统或者使用WordPress来搭建一个博客，但是东西放在云服务器上万一哪天忘了续费，或者服务器挂了数据丢失那不是太可惜了。而github博客是把博客内容全放在github上面，至少不会担心数据稳定性的问题。而且借助于git在什么地方，换台电脑使用git 将博客pull下来就能接着写。

---
废话有点多，现在开始吧:

首先你需要有个`Git`，这个东西应该大家都装了的，毕竟是吃饭干活必备的家伙，

第二：需要装有`NodeJs`,这里主要是要用到随同`NodeJs`一起的`npm`包管理工具，npm和nodejs的关系应该就像maven之于java，composer之于php，可以允许用户直接从npm服务器上下载别人编写好的第三方包到本地使用，我们就是借助于`npm`下载`hexo`

mac用户可以使用brew安装nodejs
```bash
brew install nodejs
```

windows用户就要去nodejs的官网上面下载安装包来进行安装[NodeJs下载地址](https://nodejs.org/zh-cn/)
安装完成后将其添加到path路径中，就可以直接在cmd中使用npm命令了

正题开始： 安装hexo
```bash
npm install -g hexo-cli
```
安装过程可能会比较慢，因为会去国外的npm服务器上拉取依赖，你也可以设置国内的npm镜像，比较好用的是淘宝的npm镜像服务器，[设置教程](https://npm.taobao.org/)
安装完成后可以使用
```bash
hexo -v
```
来验证hexo有没有安装成功
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/Smt0S)

如下图一样，打印出hexo的信息就代表安装成功，离革命成功又进了一步

然后我们在我们的本地新建一个文件夹，用来存放hexo的配置信息，以及我们即将要写的博客文件，进入该文件夹
```bash
mkdir ~/hexo-test 
cd ~/hexo-test
hexo init
```
初始化会去hexo服务器下载一些相关的资源，然后安装对应的依赖，依赖安装完成后会显示安装过的依赖列表
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/FjChW)
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/IYsHZ)

完后过后可以在刚才的文件中看到生成了以下的内容
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/PpIr0)

- _comfig.yml： 主要存放的是hexo的相关配置，比如等会要进行的主题，github账户等等都是在这里边进行配置,hexo的大部分配置都在这个文件里面
- node_modules： hexo的依赖包
- package.json：  hexo的依赖描述文件
- scaffolds：模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。Hexo的模板是指在新建的markdown文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。
- source：资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。
- themes： 主题文件夹，Hexo 会根据主题来生成静态页面。

现在我们使用
```bash
hexo generate
hexo server
```
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/gfgJc)

打开浏览器，输入[localhost:4000](localhost:4000)，就能看到我们的博客界面了。


![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/5FrId)
到此我们大部分的工作就已经差不多了，不过我们还需要做些其他的调整，比如将博客部署到GitHub上面，以及调整hexo生成的html的样式主题，让其看起来好看一些。

部署到GitHub上面：
首先我们要去我们的github账户上面新建一个repostory，命名必须为yourname.github.io,比如我的github用户名为kinderao，那么仓库名称为kinderao.github.io,这个地方必须按照用户名命名。
然后继续bash中输入

```bash
npm install hexo-deployer-git --save
```
安装hexo的部署插件
然后编辑（hexo-test）博客目录下的_config.yml文件，找到deploy节点，
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/34pWG)

然后将type设置为git，repo设置为刚才在github上面新建的仓库地址，现在我们在bash中输入：
```bash
hexo deploy
```
这样我们博客就已经部署到github上了，我们可以打开浏览器，输入github用户名.github.io，我的账户名为kinderao，所以我的博客地址为kinderao.github.io，你就可以看到博客已经成功的部署到github上了。

如果对于博客的界面感觉不太满意，下面教大家修改主题，在[hexo官网](https://hexo.io/themes/)上有很多漂亮的主题，选择自己喜欢的主题，然后将其拷贝或者使用git pull到theme文件夹下，然后再次回到_config.yml文件中修改theme节点，修改为对应的主题名称，然后重新使用hexo生成一次网页，就可以看到漂亮的主题已经成功的应用到了网页上了。

这里给大家推荐一下自己使用的主题，apollo主题，[主题地址](https://github.com/pinggod/hexo-theme-apollo)。

到此基本上我们的博客也就搭建成功了。每次需要写博客可以使用
```bash 
hexo n
```
新建一篇博客，也可以直接在soure文件夹下的_post文件夹下新建一个markdown文件，然后hexo会自动重载md文件，也就可以在本地浏览器上预览生成的网页，觉得写得差不多了过后，使用deploy命令就可以将其部署到github上了。

另外如果大家写博客需要插入图片的话，由于GitHub的网络不是特别好，所以图片传上去会挂，推荐大家使用图床结合markdown来写博客，我自己使用的是七牛的云存储来做图床，可以注册账号，有免费的10个g流量，基本上够用，而且只要把图片一传到七牛，然后拿着外链粘贴到markdown中，markdown中就只用保存文字内容即可，随便把里面的内容粘贴到其他的平台就可以直接发布博客了，而不用像之前一张图片一张图片的上传。

由于一直手动上传图片到七牛也是一件重复低效的事，这里给大家推荐一下ipic图床软件，一个专注于图片上传的软件，只需要一个快捷键就能将图片上传上去，或者是使用mweb或者wordmark这两款带图床上传功能的markdown编辑器，这几款软件都是收费的（逃）。虽然收费，不过还是推荐大家使用哈，毕竟还是可以提高我们的工作效率，专注于博客本身。
![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/81qx1)

![Untitled Image](http://ok8j2fjtv.bkt.clouddn.com/URbJq)