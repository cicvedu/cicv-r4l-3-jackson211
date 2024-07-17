# 作业2：对Linux内核进行一些配置

```
Please press Enter to activate this console. 
~ # insmod r4l_e1000_demo.ko
[   20.006810] r4l_e1000_demo: loading out-of-tree module taints kernel.
[   20.057226] r4l_e1000_demo: Rust for linux e1000 driver demo (init)
[   20.081257] insmod (78) used greatest stack depth: 13336 bytes left
~ # ip link set eth0 up
~ # ip addr add broadcast 10.0.2.255 dev eth0
ip: RTNETLINK answers: Invalid argument
[  105.670125] ip (80) used greatest stack depth: 13032 bytes left
~ # ip addr add 10.0.2.15/255.255.255.0 dev eth0
ip: RTNETLINK answers: File exists
~ # ip route add default via 10.0.2.1
ip: RTNETLINK answers: File exists
~ # ping 10.0.2.2
PING 10.0.2.2 (10.0.2.2): 56 data bytes
64 bytes from 10.0.2.2: seq=0 ttl=255 time=27.757 ms
64 bytes from 10.0.2.2: seq=1 ttl=255 time=3.509 ms
64 bytes from 10.0.2.2: seq=2 ttl=255 time=3.380 ms
64 bytes from 10.0.2.2: seq=3 ttl=255 time=4.016 ms
^C
--- 10.0.2.2 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 3.380/9.665/27.757 ms
~ # 
```

### Q: 在该文件夹中调用make LLVM=1，该文件夹内的代码将编译成一个内核模块。请结合你学到的知识，回答以下两个问题：
1、编译成内核模块，是在哪个文件中以哪条语句定义的？

Kbuild
```
obj-m := r4l_e1000_demo.o
```
obj-m定义了编译成内核模块


2、该模块位于独立的文件夹内，却能编译成Linux内核模块，这叫做out-of-tree module，请分析它是如何与内核代码产生联系的？

通过Makefile里的M=$$PWD 告诉linux编译该模块的路径为当前模块路径。
然后通过insmod r4l_e1000_demo.ko加载内核模块。         
