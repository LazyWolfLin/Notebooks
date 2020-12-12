# Virtualization

为了让系统更易于使用，操作系统需要将资源虚拟化并进行管理。资源虚拟化主要包括虚拟化 CPU（virtualizing the CPU）和虚拟地址空间（virtual address space）。虚拟化 CPU 提供一种假象，系统拥有非常多的虚拟 CPU，它将单个 CPU（或其中一小部分）转换为看似无限数量的 CPU，从而让许多程序看似同时运行。虚拟地址空间提供一种假象，每个正在运行的程序都完全拥有自己的物理内存，每个进程访问自己的私有虚拟地址空间被操作系统以某种方式映射到机器的物理内存上。

## Introduction


Process