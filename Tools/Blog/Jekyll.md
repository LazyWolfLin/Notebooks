# `Jekyll`

`Jekyll`是一款基于`Ruby`静态页面生成器，它可以把[`Markdowm`](Tools/Typeset/Markdown.md)文件和[`Liquid`](https://shopify.github.io/liquid/)模板编译为静态Web页面。

## installation

`Jekyll`的安装方法详见[官方指南](https://jekyllrb.com/docs/installation/)。

### Windows Subsystem for Linux

启用`Windows10`上的`WSL`并安装`distributions`后即可安装`Jekyll`。

首先安装`Ruby`：
``` Shell
sudo apt-get install ruby ruby-dev
```

然后将`Gem`的安装路径配置到环境变量中：
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

### jekyll build

构建网站并将静态网站的内容输出到`./site`文件夹。

### jekyll server

在本地的4000端口(`http://localhost:4000/`)运行本地页面服务器。

## Configuration

`Jekyll`的Configuration可以通过Command指定，也可以在项目的根目录下的`_config.yml`文件中指定，详细参数见[官方指南](https://jekyllrb.com/docs/configuration/)

## CONTENT

### Front Matter

Front Matter是位于文件开头，用于设置`page`属性的`YAML`片段。而属性的默认值可以在`_config.yml`文件设置。每一个包含Front Matter的文件都将被`Jekyll`作为特殊文件处理。

### posts

`Jekyll`的每一篇博客文章都存放在`_posts`文件夹下，创建一篇新博客文章仅需在`_posts`文件夹下创建一个符合命名要求且包含Front Matter的新文件。`Jekyll`对于博客文章的命名要求是：`YYYY-MM-DD-title.MARKUP`。

当文章需要链接到图片或者文件时，可以将图片及文件放置到根目录下的某一文件夹中，例如`assets`，然后在文章中链接它们。

### drafts

文件名中没有日期的文章将被视为文章草稿，可以放置在`_drafts`文件夹下。

### pages

除了撰写博客文章，`Jekyll`还可以创建一些特殊的页面，如Homepage(index.html)，about.html等。

### Data

`Jekyll`将从`_data`文件夹下读取`YAML`、`JSON`或`CSV`格式的文件，并储存到`site.data`中。

### Layout

Layout是位于`_layouts`文件夹下的页面模板文件。


### `Include`

`Include`是`Jekyll`内置的`Liquid`[标签](#tags)，用于在页面中包含位于`_includes`下的另一文件。

# APPENDIX

## `Liquid`

`Liquid`是一种模板语言，主要由对象(`objects`)，标签(`tags`)及过滤器(`filters`)三大部分组成。

### objects

objects是`Liquid`填充内容的位置。`Liquid`用两个花括号`{{ object }}`表示objects。例如：

``` Liquid
{{ page.title }}
```
表示将变量`page.title`的值填充到页面上。

### tags

tags是`Liquid`对模板的逻辑控制流。`Liquid`用花括号和百分号`{% tag %}`表示tags。例如：

``` Liquid
{% if page.show_sidebar %}
  <div class="sidebar">
    sidebar content
  </div>
{% endif %}
```
表示如果变量`page.show_sidebar`为`true`时则显示边栏。

### filters

filters是`Liquid`对objects修饰。`Liquid`用一条竖线`|`表示调用竖线后方的filters对竖线前方的objects。例如：

``` Liquid
{{ "hi" | capitalize }}
```
表示`capitalize`对`"hi"`进行修饰，将输出字符串`"Hi"`。