# Global Interpretation Lock

## 引入GIL的原因

1. 规避资源竞争问题
2. CPython大量使用C语言库，而大部分C语言库都不是线程安全的，所以引入GIL确保线程安全。

## 线程主动释放GIL

- check_inteval

CPython中的check_interval机制会每隔一段时间强制当前线程释放GIL，让其他的线程有执行的机会。

## 多核系统中，多线程慢于单线程

多核下，CPU0释放GIL后，其他CPU上的线程会醒着等待到切换时间后又进入待调度状态，这样会造成线程颠簸(thrashing)，导致效率低下。

## 绕过GIL的两种思路

1. 绕过CPython，使用Pypy/JPython等解释器；
2. 把关键性能代码放到其他语言中实现，比如C++。

## 并行方法

多核处理器想要提高效率通常会使用multi-processing，多进程中每个进程各自有一个GIL，互不干扰。
