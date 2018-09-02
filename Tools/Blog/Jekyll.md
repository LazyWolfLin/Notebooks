# `Jekyll`

`Jekyll`是一款基于`Ruby`静态博客生成器，它可以把[`Markdowm`](Tools/Typeset/Markdown.md)文件和[`Liquid`](https://shopify.github.io/liquid/)模板编译为静态Web页面。

## installation

`Jekyll`的安装方法详见[官方指南](https://jekyllrb.com/docs/installation/)。

### Windows Subsystem for Linux

启用`Windows10`上的`WSL`并安装`distributions`后即可安装`Jekyll`。

首先安装`Ruby`：
``` Shell
sudo apt-get install ruby ruby-dev
```

然后配置`Gem`的安装路径到环境变量中：
``` Shell
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

最后安装`Jekyll`和`bundler`
``` Shell
gem install jekyll bundler
```

## Command

### build

将当前文件夹中的内容生成到`./site`文件夹中。

### server

在本地运行一个开发服务器，路径为`http://localhost:4000/`。

## Configuration

`Jekyll`的Configuration可以通过Command指定，也可以在项目的根目录下的`_config.yml`文件中指定，详细参数见[官方指南](https://jekyllrb.com/docs/configuration/)

## CONTENT

### Front Matter

每一个包含Front Matter的文件都将被`Jekyll`作为特殊文件处理。Front Matter必须位于文件开头，并由`YAML`语法组成，用于设置预定义变量及自定义变量，而变量的默认值可以在`_config.yml`文件设置。

### posts

`Jekyll`的每一篇博客文章都存放在`_posts`文件夹下，创建一篇新博客文章仅需在`_posts`文件夹下创建一个符合命名要求且包含Front Matter的新文件。`Jekyll`对于博客文章的命名要求是：`YYYY-MM-DD-title.MARKUP`。

当文章需要链接到图片或者文件时，可以将图片及文件放置到根目录下的某一文件夹中，例如`assets`，然后在文章中链接它们。

### drafts

文件名中没有日期的文章将被视为文章草稿，可以放置在`_drafts`文件夹下。

### pages

除了撰写博客文章，`Jekyll`还可以创建一下特殊的页面，如Homepage(index.html)，about.html等。

### data

`Jekyll`可以从`_data`文件夹中读取`YAML`、`JSON`或`CSV`格式的文件，并作为`site.data`中的数据。