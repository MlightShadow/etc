# jvm

## jvm 内存

jvm 内存包含

* 程序计数器

    > 对程序运行过程做记录, 在多线程切换时有重要意义

* jvm栈

    > 常说的栈区(java 栈)
    > 与线程对应, 线程不共享
    > 每调用一个方法, 就会创建并压入一个新的栈帧
    > 随线程创建和消毁

* 本地方法栈 (C 栈)

    > 虚拟机本地方法对应使用的栈区, 于j栈类似

* 堆

    > 所有线程共享

* 方法区

> 是堆的一部分
> 存放类信息, 常量, 静态变量, 即时编译器编译后的代码

* 直接内存

> java虚拟机之外的内存, jvm也能使用, 当然这不属于jvm内存

## HotSpot 对象内存

* 对象头
* 实例数据
* 对齐填充

## 垃圾回收

通过引用判断存活

* 引用计数法: 存在互相引用无法回收的问题, 多数jvm不采用
* 可达性分析法: 通过GC Roots(j栈, c栈, 方法区常量, 方法区类静态属性 引用的对象) 判断对象是否存活

四种引用: 分别对应了垃圾回收中的不同影响

* 强引用
* 软引用
* 弱引用
* 虚引用

finalize 只能被执行一次, 并且不保证能被执行
finalize 中通过指定引用也许可以自救一次(笑)

## HotSpot 垃圾收集器

## 内存分配与回收策略

## jvm 性能调优

* 使用64位jdk, 这样能够使用较多的内存
* 使用部署多个32位虚拟机进行负载均衡来合理使用硬件

## .class 的结构

## 类加载的时机

## 类加载的过程

## 类记载器
