# 系统调用模块

该模块实现了一系列 Unix-like/POSIX-like 的系统调用，均以 `sys_xxx(args...) -> LinuxResult<isize>` 的形式提供。

该模块的目的之一是取代 [`arceos_posix_api`](https://arceos.org/arceos/arceos_posix_api/)，期望实现一个同时兼容 unikernel（用于 [`axlibc`](https://arceos.org/arceos/axlibc/)）和宏内核又尽可能安全的 POSIX API 模块。

通过 [UserPtr](userptr.md) 对传入的用户指针进行检查。
