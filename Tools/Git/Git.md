# Git

Book：[Pro Git](https://git-scm.com/book/zh/v2)

## Git Command

### git init

```
git init
```

创建一个新的 Git 仓库或者重新初始化现有的 Git 仓库。

### git clone

```
git clone <repo url>
```

将已有的 Git 仓库克隆到一个新目录中。Git 支持多种数据传输协议，包括 ssh、git、http 以及 https。

### git status

```
git status
```

显示工作目录下文件状态。

### git add

```
git add <pathspec>
```

把文件添加到 `index` 中。`index` 暂存了工作空间内容的快照，并将作为下一次提交的内容。

### git diff

```
git diff
```

显示代码库不同快照之间的之间的差异。默认比较工作目录中当前文件和已暂存区域快站之间的差异。

### git commit

```
git commit
```

记录代码库的更改。默认记录已暂存的更改。

`-m <msg>` 使用给定的 `<msg>` 作为提交信息。

`-a` 自动将所有跟踪过的文件暂存起来作为 `commit` 记录的更改。

### git rm

```
git rm <file>
```

从工作目录和 `index` 中删去文件。

### git log

```
git log
```

显示提交记录日志。

## gitignore

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。在这种情况下，我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件模式。

`.gitignore` 文件的格式规范如下：
* 所有空行或者以 `＃` 开头的行都会被 Git 忽略。
* 可以使用标准的 glob 模式匹配。
* 匹配模式可以以 `/` 字符开头防止递归。
* 匹配模式可以以 `/` 字符结尾指定目录。
* 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号 `!` 取反。

gitignore 的更多信息见 https://git-scm.com/docs/gitignore

GitHub 的 `.gitignore` 文件模板可在 https://github.com/github/gitignore 上获取。
