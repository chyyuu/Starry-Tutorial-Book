# 利用 qemu-linux-user 运行和调试程序

本章节简要介绍怎么利用 `qemu-linux-user` 运行和调试不同架构的 `linux` 程序。

## 环境安装

在[实验环境配置](ch02-01.md)中[安装 QEMU](ch02-01.md#安装qemu)的部分已经指出了安装 qemu 所需要的工具，请确保您在安装 qemu 的时候也安装了对应架构的 `linux-user`，例如 `riscv64-linux-user`。

## 使用方式

可以直接使用 `qemu-riscv64` 运行 `riscv64` 架构的应用程序，如果需要使用类似 `strace` 的功能，可以使用指令：

```shell
qemu-riscv64 -strace command
```

`command` 为需要运行的指令，例如在当下文件夹找到 `busybox` 并运行对应的指令。

```shell
qemu-riscv64 -strace ./busybox ls
```