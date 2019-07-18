# Linux

Resource:
* [Single UNIX® Specification, Version 4, 2008 Edition][susv4]
* [Linux Standard Base][lsb]
* [Filesystem Hierarchy Standard][fhs]

[susv4]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition
[lsb]: http://refspecs.linuxfoundation.org/lsb.shtml
[fhs]: http://refspecs.linuxfoundation.org/fhs.shtml

## Introduction

## Commands and Utilities

* [`[`][test] -- evaluate expression, aka `test`
* [`ar`][ar] -- create and maintain library archives (DEPRECATED)
* [`at`][at] -- examine or delete jobs for later execution
* [`awk`][awk] -- pattern scanning and processing language
* [`basename`][basename] -- return non-directory portion of a pathname
* [`batch`][batch] -- schedule commands to be executed in a batch queue
* [`bc`][bc] -- an arbitrary precision calculator language
* [`cat`][cat] -- concatenate and print files
* [`chfn`][chfn] -- change user name and information
* [`chgrp`][chgrp] -- change the file group ownership
* [`chmod`][chmod] -- change the file modes
* [`chown`][chown] -- change the file ownership
* [`chsh`][chsh] -- change login shell
* [`cksum`][cksum] -- write file checksums and sizes
* [`cmp`][cmp] -- compare two files
* [`col`][col] -- filter reverse line feeds from input
* [`comm`][comm] -- select or reject lines common to two files
* [`cp`][cp] -- copy files
* [`cpio`][cpio] -- copy file archives in and out
* [`crontab`][crontab] -- maintain crontab files for individual users
* [`csplit`][csplit] -- split files based on context
* [`cut`][cut] -- cut out selected fields of each line of a file
* [`date`][date] -- write the date and time
* [`dd`][dd] -- convert and copy a file
* [`df`][df] -- report file system disk space usage
* [`diff`][diff] -- compare two files
* [`dirname`][dirname] -- return the directory portion of a pathname
* [`dmesg`][dmesg] -- print or control the system message buffer
* [`du`][du] -- estimate file space usage
* [`echo`][echo] -- write arguments to standard output
* [`ed`][ed] -- edit text
* [`egrep`][egrep] -- search a file with an Extended Regular Expression pattern
* [`env`][env] -- set the environment for command invocation
* [`expand`][expand] -- convert tabs to spaces
* [`expr`][expr] -- evaluate arguments as an expression
* [`false`][false] -- return false value
* [`fgrep`][fgrep] -- search a file with a fixed pattern
* [`file`][file] -- determine file type
* [`find`][find] -- find files
* [`fold`][fold] -- filter for folding lines
* [`fuser`][fuser] -- identify processes using files or sockets
* [`gencat`][gencat] -- generate a formatted message catalog
* [`getconf`][getconf] -- get configuration values
* [`gettext`][gettext] -- retrieve text string from message catalog
* [`grep`][grep] -- print lines matching a pattern
* [`groupadd`][groupadd] -- create a new group
* [`groupdel`][groupdel] -- delete a group
* [`groupmod`][groupmod] -- modify a group
* [`groups`][groups] -- display a group
* [`gunzip`][gunzip] -- uncompress files
* [`gzip`][gzip] -- compress or expand files
* [`head`][head] -- copy the first part of files
* [`hostname`][hostname] -- show or set the system's host name
* [`iconv`][iconv] -- codeset conversion
* [`id`][id] -- return user identity
* [`infocmp`][infocmp] -- compare or print out terminfo descriptions
* [`install`][install] -- copy files and set attributes
* [`install_initd`][install_initd] -- activate an init script
* [`ipcrm`][ipcrm] -- remove IPC Resources
* [`ipcs`][ipcs] -- provide information on ipc facilities
* [`join`][join] -- relational database operator
* [`kill`][kill] -- terminate or signal processes
* [`killall`][killall] -- kill processes by name
* [`ln`][ln] -- link files
* [`locale`][locale] -- get locale-specific information
* [`localedef`][localedef] -- define locale environment
* [`logger`][logger] -- log messages
* [`logname`][logname] -- return the user's login name
* [`lp`][lp] -- send files to a printer
* [`lpr`][lpr] -- off line print
* [`ls`][ls] -- list directory contents
* [`lsb_release`][lsb_release] -- print distribution specific information
* [`m4`][m4] -- macro processor
* [`mailx`][mailx] -- process messages
* [`make`][make] -- maintain, update, and regenerate groups of programs (DEVELOPMENT)
* [`man`][man] -- display system documentation
* [`md5sum`][md5sum] -- generate or check MD5 message digests
* [`mkdir`][mkdir] -- make directories
* [`mkfifo`][mkfifo] -- make FIFO special files
* [`mknod`][mknod] -- make special files
* [`mktemp`][mktemp] -- make temporary file name (unique)
* [`more`][more] -- display files on a page-by-page basis
* [`mount`][mount] -- mount a file system
* [`msgfmt`][msgfmt] -- create a message object from a message file
* [`mv`][mv] -- move files
* [`newgrp`][newgrp] -- change group ID
* [`nice`][nice] -- invoke a utility with an altered nice value
* [`nl`][nl] -- line numbering filter
* [`nohup`][nohup] -- invoke a utility immune to hangups
* [`od`][od] -- dump files in octal and other formats
* [`passwd`][passwd] -- change user password
* [`paste`][paste] -- merge corresponding or subsequent lines of files
* [`patch`][patch] -- apply a diff file to an original
* [`pathchk`][pathchk] -- check pathnames
* [`pax`][pax] -- portable archive interchange
* [`pidof`][pidof] -- find the process ID of a running program
* [`pr`][pr] -- print files
* [`printf`][printf] -- write formatted output
* [`ps`][ps] -- report process status
* [`pwd`][pwd] -- return working directory name
* [`remove_initd`][remove_initd] -- clean up init script system modifications introduced by install_initd
* [`renice`][renice] -- alter priority of running processes
* [`rm`][rm] -- remove directory entries
* [`rmdir`][rmdir] -- remove directories
* [`sed`][sed] -- stream editor
* [`sendmail`][sendmail] -- an electronic mail transport agent
* [`seq`][seq] -- generate a sequence of numbers
* [`sh`][sh] -- shell, the standard command language interpreter
* [`shutdown`][shutdown] -- shut the system down
* [`sleep`][sleep] -- suspend execution for an interval
* [`sort`][sort] -- sort, merge, or sequence check text files
* [`split`][split] -- split files into pieces
* [`strings`][strings] -- find printable strings in files
* [`strip`][strip] -- remove unnecessary information from strippable files (DEVELOPMENT)
* [`stty`][stty] -- set the options for a terminal
* [`su`][su] -- change user ID
* [`sync`][sync] -- flush file system buffers
* [`tail`][tail] -- copy the last part of a file
* [`tar`][tar] -- file archiver
* [`tee`][tee] -- duplicate standard input
* [`test`][test] -- evaluate expression, aka `[`
* [`tic`][tic] -- the terminfo entry-description compiler
* [`time`][time] -- time a simple command
* [`touch`][touch] -- change file access and modification times
* [`tput`][tput] -- initialize a terminal or query terminfo database
* [`tr`][tr] -- translate characters
* [`true`][true] -- return true value
* [`tsort`][tsort] -- topological sort
* [`tty`][tty] -- return user's terminal name
* [`umount`][umount] -- unmount file systems
* [`uname`][uname] -- return system name
* [`unexpand`][unexpand] -- convert spaces to tabs
* [`uniq`][uniq] -- report or filter out repeated lines in a file
* [`useradd`][useradd] -- create a new user or update default new user information
* [`userdel`][userdel] -- delete a user account and related files
* [`usermod`][usermod] -- modify a user account
* [`wc`][wc] -- word, line, and byte or character count
* [`xargs`][xargs] -- build and execute command lines from standard input
* [`zcat`][zcat] -- uncompress files to standard output

Built In Utilities

* [`alias`][alias] -- define or display aliases
* [`bg`][bg] -- run jobs in the background
* [`cd`][cd] -- change the working directory
* [`command`][command] -- execute a simple command
* [`fc`][fc] -- process the command history list
* [`fg`][fg] -- run jobs in the foreground
* [`getopts`][getopts] -- parse utility options
* [`hash`][hash] -- remember or report utility locations
* [`jobs`][jobs] -- display status of jobs in the current session
* [`read`][read] -- read a line from standard input
* [`type`][type] -- write a description of command type
* [`ulimit`][ulimit] -- set or report file size limit
* [`umask`][umask] -- get or set the file mode creation mask
* [`unalias`][unalias] -- remove alias definitions
* [`wait`][wait] -- await process completion

[alias]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/alias.html
[ar]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/ar.html
[at]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/at.html
[awk]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/awk.html
[basename]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/basename.html
[batch]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/batch.html
[bc]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/bc.html
[bg]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/bg.html
[cat]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cat.html
[cd]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cd.html
[chfn]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/chfn.html
[chgrp]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/chgrp.html
[chmod]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/chmod.html
[chown]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/chown.html
[chsh]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/chsh.html
[cksum]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cksum.html
[cmp]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cmp.html
[col]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/col.html
[comm]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/comm.html
[command]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/command.html
[cp]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cp.html
[cpio]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/cpio.html
[crontab]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/crontab.html
[csplit]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/csplit.html
[cut]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/cut.html
[date]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/date.html
[dd]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/dd.html
[df]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/df.html
[diff]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/diff.html
[dirname]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/dirname.html
[dmesg]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/dmesg.html
[du]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/du.html
[echo]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/echo.html
[ed]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/ed.html
[egrep]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/egrep.html
[env]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/env.html
[expand]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/expand.html
[expr]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/expr.html
[false]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/false.html
[fc]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/fc.html
[fg]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/fg.html
[fgrep]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/fgrep.html
[file]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/file.html
[find]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/find.html
[fold]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/fold.html
[fuser]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/fuser.html
[gencat]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/gencat.html
[getconf]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/getconf.html
[getopts]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/getopts.html
[gettext]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/gettext.html
[grep]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/grep.html
[groupadd]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/groupadd.html
[groupdel]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/groupdel.html
[groupmod]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/groupmod.html
[groups]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/groups.html
[gunzip]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/gunzip.html
[gzip]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/gzip.html
[hash]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/hash.html
[head]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/head.html
[hostname]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/hostname.html
[iconv]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/iconv.html
[id]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/id.html
[infocmp]: https://invisible-island.net/ncurses/man/infocmp.1m.html
[install]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/install.html
[install_initd]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/installinitd.html
[ipcrm]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/ipcrm.html
[ipcs]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/ipcs.html
[jobs]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/jobs.html
[join]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/join.html
[kill]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/kill.html
[killall]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/killall.html
[ln]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/ln.html
[locale]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/locale.html
[localedef]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/localedef.html
[logger]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/logger.html
[logname]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/logname.html
[lp]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/lp.html
[lpr]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/lpr.html
[ls]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/ls.html
[lsb_release]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/lsbrelease.html
[m4]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/m4.html
[mailx]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/mailx.html
[make]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/make.html
[man]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/man.html
[md5sum]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/md5sum.html
[mkdir]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/mkdir.html
[mkfifo]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/mkfifo.html
[mknod]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/mknod.html
[mktemp]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/mktemp.html
[more]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/more.html
[mount]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/mount.html
[msgfmt]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/msgfmt.html
[mv]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/mv.html
[newgrp]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/newgrp.html
[nice]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/nice.html
[nl]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/nl.html
[nohup]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/nohup.html
[od]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/od.html
[passwd]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/passwd.html
[paste]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/paste.html
[patch]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/patch.html
[pathchk]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/pathchk.html
[pax]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/pax.html
[pidof]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/pidof.html
[pr]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/pr.html
[printf]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/printf.html
[ps]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/ps.html
[pwd]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/pwd.html
[read]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/read.html
[remove_initd]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/removeinitd.html
[renice]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/renice.html
[rm]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/rm.html
[rmdir]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/rmdir.html
[sed]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/sed.html
[sendmail]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/baselib-sendmail-1.html
[seq]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/seq.html
[sh]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/sh.html
[shutdown]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/shutdown.html
[sleep]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/sleep.html
[sort]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/sort.html
[split]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/split.html
[strings]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/strings.html
[strip]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/strip.html
[stty]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/stty.html
[su]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/su.html
[sync]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/sync.html
[tail]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/tail.html
[tar]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/tar.html
[tee]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/tee.html
[test]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/test.html
[type]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/type.html
[tic]: https://invisible-island.net/ncurses/man/tic.1m.html
[time]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/time.html
[touch]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/touch.html
[tput]: https://invisible-island.net/ncurses/man/tput.1.html
[tr]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/tr.html
[true]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/true.html
[tsort]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/tsort.html
[tty]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/tty.html
[ulimit]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/ulimit.html
[umask]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/umask.html
[umount]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/umount.html
[unalias]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/unalias.html
[uname]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/uname.html
[unexpand]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/unexpand.html
[uniq]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/uniq.html
[useradd]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/useradd.html
[userdel]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/userdel.html
[usermod]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/usermod.html
[wait]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/wait.html
[wc]: http://pubs.opengroup.org/onlinepubs/9699919799.2008edition/utilities/wc.html
[xargs]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/xargs.html
[zcat]: http://refspecs.linuxfoundation.org/LSB_5.0.0/LSB-Core-generic/LSB-Core-generic/zcat.html

### Coreutils

[Coreutils - GNU core utilities](https://www.gnu.org/software/coreutils/),  are the basic file, shell and text manipulation utilities of the GNU operating system.

## Shell

[Bash](./Bash.md)

## Filesystem

### [`/`](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch03.html) -- the toot filesystem

| Directory | Description |
| --- | --- |
| `/bin` | Essential command binaries |
| `/boot` | Static files of the boot loader |
| `/dev` | Device files |
| `/etc` | Host-specific system configuration |
| `/lib` | Essential shared libraries and kernel modules |
| `/media` | Mount point for removable media |
| `/mnt` | Mount point for mounting a filesystem temporarily |
| `/opt` | Add-on application software packages |
| `/run` | Data relevant to running processes |
| `/sbin` | Essential system binaries |
| `/srv` | Data for services provided by this system |
| `/tmp` | Temporary files |
| `/usr` | Secondary hierarchy |
| `/var` | Variable data |
| `home` | User home directories (optional) |
| `lib<qual>` | Alternate format essential shared libraries (optional) |
| `root` | Home directory for the root user (optional) |