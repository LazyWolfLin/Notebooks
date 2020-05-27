# Make

Version: 4.1

Resource:
* [GNU Make Manual](https://www.gnu.org/software/make/manual/make.html)
* [跟我一起写 Makefile](https://blog.csdn.net/haoel/article/details/2886)

## Introduction

`make` 能够自动确定大型代码库中需要编译的文件，并发出指令重新编译它们。

使用 `make` 之前，你必须编写一个名为 `makefile` 的文件，用于描述你的代码库中的文件关系并提供用于更新每个文件的命令。如果有了合适的 Makefile 文件，那么每次修改源码之后执行以下命令即可完成必要的重编译。

```
make
```

## Command

```
Usage: make [options] [target] ...
Options:
  -b, -m                      Ignored for compatibility.
  -B, --always-make           Unconditionally make all targets.
  -C DIRECTORY, --directory=DIRECTORY
                              Change to DIRECTORY before doing anything.
  -d                          Print lots of debugging information.
  --debug[=FLAGS]             Print various types of debugging information.
  -e, --environment-overrides
                              Environment variables override makefiles.
  --eval=STRING               Evaluate STRING as a makefile statement.
  -f FILE, --file=FILE, --makefile=FILE
                              Read FILE as a makefile.
  -h, --help                  Print this message and exit.
  -i, --ignore-errors         Ignore errors from recipes.
  -I DIRECTORY, --include-dir=DIRECTORY
                              Search DIRECTORY for included makefiles.
  -j [N], --jobs[=N]          Allow N jobs at once; infinite jobs with no arg.
  -k, --keep-going            Keep going when some targets can't be made.
  -l [N], --load-average[=N], --max-load[=N]
                              Don't start multiple jobs unless load is below N.
  -L, --check-symlink-times   Use the latest mtime between symlinks and target.
  -n, --just-print, --dry-run, --recon
                              Don't actually run any recipe; just print them.
  -o FILE, --old-file=FILE, --assume-old=FILE
                              Consider FILE to be very old and don't remake it.
  -O[TYPE], --output-sync[=TYPE]
                              Synchronize output of parallel jobs by TYPE.
  -p, --print-data-base       Print make's internal database.
  -q, --question              Run no recipe; exit status says if up to date.
  -r, --no-builtin-rules      Disable the built-in implicit rules.
  -R, --no-builtin-variables  Disable the built-in variable settings.
  -s, --silent, --quiet       Don't echo recipes.
  -S, --no-keep-going, --stop
                              Turns off -k.
  -t, --touch                 Touch targets instead of remaking them.
  --trace                     Print tracing information.
  -v, --version               Print the version number of make and exit.
  -w, --print-directory       Print the current directory.
  --no-print-directory        Turn off -w, even if it was turned on implicitly.
  -W FILE, --what-if=FILE, --new-file=FILE, --assume-new=FILE
                              Consider FILE to be infinitely new.
  --warn-undefined-variables  Warn when an undefined variable is referenced.
```

## Makefile

每一个 Makefile 文件通常由多个规则组成，每个规则具有 `target`、`prerequisites` 和 `recipe`：

```
target … : prerequisites …
	recipe
	…
	…
```

`target` 通常是代码生成的文件名，也可以是可执行的操作的名称。

`prerequisites` 是用于生成 `target` 的一个或多个文件。

`recipe` 是供 `make` 执行的一条或多条命令。`recipe` 可以由多行组成，但是每一行都需要以一个 tab 符为起始。