# Operating System

## Introduction

操作系统（Operating System，OS），负责让程序运行变得容易（甚至允许你同时运行多个程序），允许程序共享内存，让程序能够与设备交互，以及其他类似的有趣的工作。

操作系统有三个关键概念：虚拟化（virtualization）、并发（concurrency）和持久化（persistence）。对 CPU、内存或磁盘等物理资源（resources）进行虚拟化（virtualize）；处理与并发（concurrency）相关的麻烦且棘手的问题；持久化（persistently）存储内存数据。

操作系统的设计与实现有三个目标：建立一些抽象（abstraction），让系统易于使用；提供高性能（performance），最小化操作系统的开销（minimize the overhead）；在应用程序之间以及在 OS 和应用程序之间提供保护（protection），让进程彼此隔离（isolation）。

## Virtualization

为了让系统更易于使用，操作系统需要将资源虚拟化并进行管理。资源虚拟化主要包括虚拟化 CPU（virtualizing the CPU）和虚拟地址空间（virtual address space）。虚拟化 CPU 提供一种假象，系统拥有非常多的虚拟 CPU，它将单个 CPU（或其中一小部分）转换为看似无限数量的 CPU，从而让许多程序看似同时运行。虚拟地址空间提供一种假象，每个正在运行的程序都完全拥有自己的物理内存，每个进程访问自己的私有虚拟地址空间被操作系统以某种方式映射到机器的物理内存上。

## Concurrency

## Persistence

在系统内存中，数据容易丢失，因为像 DRAM 这样的设备以易失（volatile）的方式存储数值。如果断电或系统崩溃，那么内存中的所有数据都会丢失。因此，操作系统需要通过硬件和软件的支持来持久地（persistently）存储数据。

## Resource

* [Operating Systems: Three Easy Pieces](http://pages.cs.wisc.edu/~remzi/OSTEP/)