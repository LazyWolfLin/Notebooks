# Linux

## Introduction

## Command

### Coreutils

[Coreutils - GNU core utilities](https://www.gnu.org/software/coreutils/),  are the basic file, shell and text manipulation utilities of the GNU operating system.

Version: 8.28

* Output of entire files
    * [cat](./Command/Coreutils/cat.md): Concatenate FILE(s) to standard output.
    * tac
    * nl
    * od
    * base32
    * base64
    * basenc
* Formatting file contents
    * fmt
    * pr
    * fold
* Output of parts of files
    * head
    * tail
    * split
    * csplit
* Summarizing files
    * wc
    * sum
    * cksum
    * b2sum
    * md5sum
    * sha1sum
    * sha224sum
    * sha256sum
    * sha384sum
    * sha512sum
* Operating on sorted files
    * sort
    * shuf
    * uniq
    * comm
    * ptx
    * tsort
* Operating on fields
    * cut
    * paste
    * join
* Operating on characters
    * tr
    * expand
    * unexpand
* Directory listing
    * [ls](./Command/Coreutils/ls.md): List information about the FILEs (the current directory by default).
    * dir
    * vdir
    * dircolors
* Basic operations
    * [cp](./Command/Coreutils/cp.md): Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.
    * dd
    * install
    * [mv](./Command/Coreutils/mv.md): Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.
    * [rm](./Command/Coreutils/rm.md): Remove (unlink) the FILE(s).
    * shred
* Special file types
    * mkdir
    * rmdir
    * unlink
    * mkfifo
    * mknod
    * ln
    * link
    * readlink
* Changing file attributes
    * chgrp
    * chmod
    * chown
    * [touch](./Command/Coreutils/touch.md): Update the access and modification times of each FILE to the current time.
* Disk usage
    * df
    * du
    * stat
    * sync
    * truncate
* Printing text
    * [echo](./Command/Coreutils/echo.md): Echo the STRING(s) to standard output.
    * printf
    * yes
* Conditions
    * false
    * true
    * test
    * expr
* Redirection
    * tee
* File name manipulation
    * dirname
    * basename
    * pathchk
    * mktemp
    * realpath
* Working context
    * [pwd](./Command/Coreutils/pwd.md): Print the full filename of the current working directory.
    * stty
    * printenv
    * tty
* User information
    * id
    * logname
    * whoami
    * groups
    * users
    * who
* System context
    * date
    * arch
    * nproc
    * uname
    * hostname
    * hostid
    * uptime
* SELinux context
    * chcon
    * runcon
* Modified command invocation
    * chroot
    * env
    * nice
    * nohup
    * stdbuf
    * timeout
* Process control
    * kill
* Delaying
    * sleep
* Numeric operations
    * factor
    * numfmt
    * seq

### Other

* [Grep](./Command/Grep.md): Search for PATTERN in each FILE.
* [less](https://www.gnu.org/software/less/): GNU less is a program similar to more, but which allows backward movement in the file as well as forward movement. 

## Shell

[Bash](./Bash.md)