+++
title = "使用Hugo创建静态站点"
subtitle = "MacOS下创建Hugo站点"

date = 2016-04-20T00:00:00
lastmod = 2018-01-16T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["xhtian"]

tags = ["Hugo"]
summary = "MacOS下创建Hugo站点"
+++


---

#### **Step 1:安装Homebrew**

Homebrew，是MacOs下的软件包管理，需要先从[brew.sh](http://brew.sh)下载安装Homebrew，参考官网的安装方法。

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/
	install/master/install)"

```

#### **Step 2: 安装 Hugo**

通过执行以下命令完成安装：

```
$ brew install hugo
```

可以通过以下命令，检查Hugo的安装情况，以及安装版本信息。

	$ hugo version

#### **Step 3: 生成站点**

执行下面命令，在home目录下生成名为mySite的站点。

```
$ hugo new site ~/mySite
```

下面显示站点创建成功

```
Congratulations! Your new Hugo site is created in ~/mySite.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/, or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".
```

进入mySite站点目录，关键目录结构如下说明：

```
|- archetypes ：存放default.md，头文件格式

|- config.toml ： 主配置文件

|- content/post ：文章主目录，需要发布的文章放在这里

|- static ：静态资源文件

|- themes ：主题文件
```

图片路径示例：

假设测试baseurl为http://localhost:1313/，图片位置：/static/img/1.png，那么在Markdown中写作`![图片说明](/img/1.png)`,无论在本地还是发布出去，图片的路径都是相对于baseurl而言的。

#### **Step 4: 创建文章**

```
$ hugo new post/first.md
```

是考验你的MD和文字功底的时候了……

启动Hugo边创作边预览：

```
$ hugo server -t=academic -D
```
浏览器里打开： [http://localhost:1313](http://localhost:1313)，Hugo会检测文件是否更新，刷新页面预览效果。666

```
-t 使用的主题名称
-D 包含草稿文件（MD文件中，draft = true，即标记为草稿状态的文件）否则草稿文件被忽略
```

#### **Step 5: 安装皮肤**

Hugo有众多社区支持者贡献了非常多优秀的主题。大家可以到[https://themes.gohugo.io](https://themes.gohugo.io)选择安装。

本文安装的主题为：academic([GitHub地址](https://github.com/gcushen/hugo-academic))

该主题非常强大，关注者与使用者众多，文档非常齐全，安装和使用说明也非常详细完备，推荐给大家供参考选用。

#### **Step 6: 生成页面部署**

[Hugo支持多种部署方式,点击链接查看支持部署方式](https://gohugo.io/hosting-and-deployment/)。

本文以部署到GitHub为例，其他请参考上述链接地址。

假设你需要部署在 [GitHub Pages](https://pages.github.com) 上，首先在GitHub上创建一个Repository，命名为：techauthor.github.io （techauthor替换为你的github用户名）。

User/organization site 和 Project site 不尽相同，区别和Repository创建方法，请查看[GitHub Pages](https://pages.github.com)相关说明，此处不再赘述。

在站点根目录执行 Hugo 命令生成最终页面：

```
$ hugo --theme=academic --baseUrl="http://techauthor.github.io/"
```

（注意，以上命令并不会生成草稿页面，如果未生成任何文章，请将文章头部的 `draft=true` 改为 `draft=false` ）

如果一切顺利，所有静态页面都会生成到 public 目录，将pubilc目录里所有文件 push 到刚创建的Repository的 master 分支。

```
$ cd public
$ git init
$ git remote add origin https://github.com/techauthor/techauthor.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```

浏览器里访问：http://techauthor.github.io/，即可预览你的创作成果。

祝贺大功告成。

---