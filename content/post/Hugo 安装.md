+++
title = "Hugo 安装"
subtitle = "MacOS下安装Hugo"

date = 2016-04-20T00:00:00
lastmod = 2018-01-14T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["xhtian"]

tags = ["Hugo"]
summary = "MacOS下安装Hugo"
+++


---

#### **Step 1: 安装 Hugo**

* 通过执行命令完成Hugo安装：

```
$ brew install hugo
```

Homebrew，是MacOs下的软件包管理，需要先从[brew.sh](http://brew.sh)下载安装Homebrew。

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/
	install/master/install)"

```

可以通过以下命令，检查Hugo的安装情况，以及安装版本信息。

	$ hugo version

* 生成站点

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

进入mySite站点目录，目录结构如下：

```
|- archetypes ：存放default.md，头文件格式

|- layouts ：主题模板文件

|- static ：静态资源

|- theme.toml ：主题配置文件
```

* 运行Hugo

在你的站点根目录执行 Hugo 命令进行调试：

```
$ hugo server -t=academic -D
```

浏览器里打开： [http://localhost:1313](http://localhost:1313)

* 部署

假设你需要部署在 GitHub Pages 上，首先在GitHub上创建一个Repository，命名为：coderzh.github.io （coderzh替换为你的github用户名）。

在站点根目录执行 Hugo 命令生成最终页面：

```
$ hugo --theme=academic --baseUrl="http://techauthor.github.io/"
```

（注意，以上命令并不会生成草稿页面，如果未生成任何文章，请去掉文章头部的 draft=true 再重新生成。）

如果一切顺利，所有静态页面都会生成到 public 目录，将pubilc目录里所有文件 push 到刚创建的Repository的 master 分支。

```
$ cd public
$ git init
$ git remote add origin https://github.com/techauthor/techauthor.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```

浏览器里访问：http://techauthor.github.io/

---