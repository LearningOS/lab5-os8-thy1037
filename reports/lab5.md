# 实验报告

## 简述功能
引入了线程机制，并实现了互斥锁、信号量、条件变量机制来实现线程间同步，最终加入了死锁判断功能。

## 简答题
1. 需要回收的资源包括：
    * 线程控制块，其内部可变数据块；
    * 进程控制块，其内部可变数据；
    * 子进程控制块向量；
    * 子线程的 tid/trap_cx/ustack
    * 用户空间中的数据（code/data）；
    * 文件描述符向量；
    
    可能在子进程中被引用，不用回收，在 sys_waittid 被调用时会进行释放回收。

2. `Mutex1` 中不管是否有等待线程都将 `mutex_inner.locked` 设为了 `false`，这会在有等待线程时造成 Mutex 状态错误，因为等待线程被唤醒时，并无法将 `mutex_inner.locked` 设为了 `true`；`Mutex1` 中在有等待线程时，并不会改变 `Mutex`的状态，只有在无等待线程时才将 `mutex_inner.locked` 设为了 `false`，可以始终保证 `Mutex` 状态的正确性。

## 完成记录
1. 在进程控制块中添加死锁检测、资源计数等数据结构；
2. 在互斥锁、信号量的创建、获取、释放操作中添加 步骤1 中的数据的初始化与检查。

