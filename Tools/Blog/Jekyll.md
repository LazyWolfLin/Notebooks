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

