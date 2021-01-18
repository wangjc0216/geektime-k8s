# 极客时间 深入剖析Kubernetes 学习


## 疑问清单
- [ ] 20210112 第五章，可以使用golang实现创建PID为1的线程的代码吗？ 

- [ ] 20210112 如何理解，第五章评论区下面的： 从操作系统内核态的角度来看是没有线程的？

- [ ] 20210113 第六章，对于安全问题，可以通过**Seccomp**等技术对容器内部发起的所有系统调用进行过滤与甄别来进行安全加固，，但这种方法因为多了一层对系统调用的过滤，必然会拖累容器的性能。因为安全问题，没有人敢把运行在物理机上的Linux容器直接放到公网上。**后面会讲到虚拟化独立内核技术的容器实现，则可以很好的在隔离与性能之间做出选择。**
            
            ​    seccomp 是一个怎么样的技术，有无实践操作？
            
            
            
- [ ] 20210113 第六章，通过`mount -t cgroup`看到执行结果为一些挂载目录，了解下mount的完整使用。

- [ ] 20210113 第六章，了解Cgroup具体类型及其对应的设置规则

     如： blkio，为块设备设定I/O 限制，一般用于磁盘等设备；

     ​         cpuset，为进程分配单独的 CPU 核和对应的内存节点；

     ​		 memory，为进程设定内存使用的限制。

- [ ] 20210113 第六章，根据top命令查看CPU执行类型，如下：

     ```
     $ top%Cpu0 :100.0 us, 0.0 sy, 0.0 ni, 0.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
     ```

     

- [ ] 20210113 第六章， 你是否知道如何修复容器中的 top 指令以及 /proc 文件系统中的信息呢？（提示：lxcfs）

- [ ] top命令的linux相关知识

- [ ] 20210114 磊总提问，kubernetes如何做到高可用 -- controller manager 和scheduler 会通过选举实现高可用，endpoint会注册到etcd中。

- [ ] 20210114 磊总提问，overlay网络  docker子网络，flannel技术，不甚了解

- [ ] 20210118 在Mac上执行了下面的命令，没有达到预期的效果，不知道什么原因。

     ```
     otool -L /bin/ls | egrep -o '/usr.*\.dylib'
     /usr/lib/libutil.dylib
     /usr/lib/libncurses.5.4.dylib
     /usr/lib/libSystem.B.dylib
     ```

     那么我在执行下面的命令的时候却会出现错误：

     ```
     for i in $list; do  ls  "$i"    ; done
     ```







## kubernetes 知识图谱
![kubernetes.jpg](./one_chapter/kubernetes.jpg)