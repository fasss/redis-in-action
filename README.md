<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [常见监控工具实战](#%E5%B8%B8%E8%A7%81%E7%9B%91%E6%8E%A7%E5%B7%A5%E5%85%B7%E5%AE%9E%E6%88%98)
  - [top](#top)
    - [举例说明](#%E4%B8%BE%E4%BE%8B%E8%AF%B4%E6%98%8E)
    - [top命令常见技巧](#top%E5%91%BD%E4%BB%A4%E5%B8%B8%E8%A7%81%E6%8A%80%E5%B7%A7)
    - [故障排除](#%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4)
  - [ps](#ps)
    - [ps最常用的命令](#ps%E6%9C%80%E5%B8%B8%E7%94%A8%E7%9A%84%E5%91%BD%E4%BB%A4)
    - [按消耗的内存对进程进行排序](#%E6%8C%89%E6%B6%88%E8%80%97%E7%9A%84%E5%86%85%E5%AD%98%E5%AF%B9%E8%BF%9B%E7%A8%8B%E8%BF%9B%E8%A1%8C%E6%8E%92%E5%BA%8F)
  - [pidstat](#pidstat)
    - [内存使用情况统计](#%E5%86%85%E5%AD%98%E4%BD%BF%E7%94%A8%E6%83%85%E5%86%B5%E7%BB%9F%E8%AE%A1)
    - [IO使用情况统计](#io%E4%BD%BF%E7%94%A8%E6%83%85%E5%86%B5%E7%BB%9F%E8%AE%A1)
    - [cpu使用情况统计](#cpu%E4%BD%BF%E7%94%A8%E6%83%85%E5%86%B5%E7%BB%9F%E8%AE%A1)
  - [sar](#sar)
    - [监控cpu颈瓶](#%E7%9B%91%E6%8E%A7cpu%E9%A2%88%E7%93%B6)
    - [监控内存颈瓶](#%E7%9B%91%E6%8E%A7%E5%86%85%E5%AD%98%E9%A2%88%E7%93%B6)
    - [监控IO颈瓶](#%E7%9B%91%E6%8E%A7io%E9%A2%88%E7%93%B6)
  - [mpstat](#mpstat)
  - [iostat](#iostat)
    - [iostat 案例分析](#iostat-%E6%A1%88%E4%BE%8B%E5%88%86%E6%9E%90)
    - [如何判定磁盘性能问题](#%E5%A6%82%E4%BD%95%E5%88%A4%E5%AE%9A%E7%A3%81%E7%9B%98%E6%80%A7%E8%83%BD%E9%97%AE%E9%A2%98)
  - [vmstat](#vmstat)
  - [lsof](#lsof)
    - [lsof 基础](#lsof-%E5%9F%BA%E7%A1%80)
    - [使用lsof分析打开的文件](#%E4%BD%BF%E7%94%A8lsof%E5%88%86%E6%9E%90%E6%89%93%E5%BC%80%E7%9A%84%E6%96%87%E4%BB%B6)
    - [检查打开的数据文件和日志文件](#%E6%A3%80%E6%9F%A5%E6%89%93%E5%BC%80%E7%9A%84%E6%95%B0%E6%8D%AE%E6%96%87%E4%BB%B6%E5%92%8C%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6)
    - [pt-ioprofile脚本lsof中的应用](#pt-ioprofile%E8%84%9A%E6%9C%AClsof%E4%B8%AD%E7%9A%84%E5%BA%94%E7%94%A8)
  - [ss](#ss)
  - [netstat](#netstat)
    - [显示路由表信息](#%E6%98%BE%E7%A4%BA%E8%B7%AF%E7%94%B1%E8%A1%A8%E4%BF%A1%E6%81%AF)
    - [查看监听的端口](#%E6%9F%A5%E7%9C%8B%E7%9B%91%E5%90%AC%E7%9A%84%E7%AB%AF%E5%8F%A3)
    - [查询TCP的状态信息](#%E6%9F%A5%E8%AF%A2tcp%E7%9A%84%E7%8A%B6%E6%80%81%E4%BF%A1%E6%81%AF)
  - [strace](#strace)
    - [strace 基本使用方法](#strace-%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95)
    - [strace 跟踪mysqld启动进程](#strace-%E8%B7%9F%E8%B8%AAmysqld%E5%90%AF%E5%8A%A8%E8%BF%9B%E7%A8%8B)
    - [strace 统计nginx进程信息](#strace-%E7%BB%9F%E8%AE%A1nginx%E8%BF%9B%E7%A8%8B%E4%BF%A1%E6%81%AF)
    - [strace 举例](#strace-%E4%B8%BE%E4%BE%8B)
    - [strace 统计php-cgi 进程信息](#strace-%E7%BB%9F%E8%AE%A1php-cgi-%E8%BF%9B%E7%A8%8B%E4%BF%A1%E6%81%AF)
    - [strace 解决 502 错误](#strace-%E8%A7%A3%E5%86%B3-502-%E9%94%99%E8%AF%AF)
    - [strace 解决sshd登录慢的问题](#strace-%E8%A7%A3%E5%86%B3sshd%E7%99%BB%E5%BD%95%E6%85%A2%E7%9A%84%E9%97%AE%E9%A2%98)
    - [strace 分析mysql客户端走的协议](#strace-%E5%88%86%E6%9E%90mysql%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%B5%B0%E7%9A%84%E5%8D%8F%E8%AE%AE)
    - [strace 和awk结合显示时间](#strace-%E5%92%8Cawk%E7%BB%93%E5%90%88%E6%98%BE%E7%A4%BA%E6%97%B6%E9%97%B4)
    - [strace 查看脚本执行的位置](#strace-%E6%9F%A5%E7%9C%8B%E8%84%9A%E6%9C%AC%E6%89%A7%E8%A1%8C%E7%9A%84%E4%BD%8D%E7%BD%AE)
  - [ltrace](#ltrace)
  - [tcpdump](#tcpdump)
  - [sysdig](#sysdig)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# 常见监控工具实战
![top.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/17/0319346bc8d451830f8a7fb97bc4e95b.png)

## top

top命令提供了实时的对系统处理器的状态监视.它将显示系统中CPU最“敏感”的任务列表.该命令可以按CPU使用.内存使用和执行时间对任务进行排序

top命令能够得到的信息
* 系统已运行的时间
* 当前已经登录的用户数
* 1，5，15分钟的平均负载情况
* 所有以及单个CPU的利用率

下面是一个top命令输出的截图
![top.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/18/35540d92cf68926b650908260020cffe.png )


### 举例说明
**「第一行」任务队列信息，输出结果等同于uptime**
  - 09:16:35 当前时间
  - up 29 days, 22:40,系统已经运行了29天22小时40分
  - 3 users, 当前有3个用户
  - load average: 0.76, 0.18, 0.06  1分钟，5分钟，15分钟负载

**「第二行」任务进程**
  - Tasks: 217 total,   1 running, 216 sleeping,   0 stopped,   0 zombie

**「第三行」cpu信息**
  - 5.9%us 用户态百分比
  - 1.5%sy 内核态百分比
  - 0.0%ni 改变过优先级的进程百分比
  - 84.7%id 空闲CPU百分比
  - 7.8%wa   等待IO请求完成的百分比

**「第四行」内存信息**
  - 24523680k total 总内存 24G
  - 1572828k used 使用内存
  - 22950852k free 空闲内存
  - 171004k buffers 缓存内存

**「第五行」Swap交换分区**
 - Swap:  4095992k total, 交换内存总量4G      
 - 0k used 使用的交换区总量 0K
 - 4095992k free 空闲交换去总量 4G
 - 796408k cached

**「第七行」各进程（任务）的状态监控**
 * VIRT 虚拟内存
 * RES  物理内存
 * SHR  共享内存
 * %CPU cpu使用率百分比
 * %MEM 内存使用率百分比

通过上面的输出得到:「mysqld」进程的PID:「4741」。占用虚拟内存为「4455M」，占用的物理内存为「222M」
占用的CPU时间百分比为 53.1%。 占用总内存的百分比为0.9%， 这也可以通过下面的公式换算
由于此服务器的总内存为「24G」 ,而该Mysqld进程占用物理内存222M 「222/1024/24 ~ 0.009」

### top命令常见技巧

* 输入大写P，输出结果按CPU占用降序排序。
* 输入大写M，输出结果按内存占用降序排序。
* 按数字 1 则可以显示所有CPU核心的负载情况。
* top -d 3    每隔 3 秒刷新一次，默认 1 秒
* top -p 4360,4358    监控指定多个进程
* 「top -p 4741 」 只显示指定pid的进程信息

### 故障排除

```
PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
16064 root      20   0  205m 6596 4328 R 99.7  0.0   0:28.51 php
```

「16064」这个php进程，占用了「99.7%」的CPU资源，由于该php程序执行了一个死循环
导致了占用如此高的cpu。

## ps
ps命令可以确定有哪些进程正在运行和运行的状态、进程是否结束、进程有没有僵死、哪些进程占用了过多 的资源(cpu,内存)等等。

### ps最常用的命令
```
ps aux | grep mysqld
```

或者

```
ps -ef | grep mysqld
```
> 该命令检查是否在运行mysqld进程。 通过管道符 然后grep 过滤相关信息



### 按消耗的内存对进程进行排序


第一种方法

```
ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user,uid' | sort -k5nr
```

第二种方法

```
ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user,uid' --sort -rsz
```


输出结果

```
[root@web3_u ~]# ps -e -o 'pid,comm,args,pcpu,rsz,vsz,stime,user' | sort -k5nr
23946 php-cgi         /usr/local/php/bin/php-cgi   0.0 129540 440000 Oct06 nobody
24418 php-cgi         /usr/local/php/bin/php-cgi   0.0 129336 437684 Oct06 nobody
18973 php-cgi         /usr/local/php/bin/php-cgi   0.0 129268 440176 Oct06 nobody
17219 php-cgi         /usr/local/php/bin/php-cgi   0.0 126588 439840 Oct06 nobody
 6996 php-cgi         /usr/local/php/bin/php-cgi   0.0 125056 438104 Oct09 nobody
23850 php-cgi         /usr/local/php/bin/php-cgi   0.0 122984 440036 Oct09 nobody
```


参数解析:

* -e  显示所有进程
* -o 定制显示信息,用户自定义输出格式
* pid 进程ID
* comm 进程名
* args 启动命令
* pcpu 占用CPU 百分比
* rsz 占用物理内存大小
* vsz 占用虚拟内存大小
* stime 进程启动时间
* user 启动用户

以第一行为例

* 进程ID 23946
* 进程名 php-cgi
* 启动命令 /usr/local/php/bin/php-cgi
* 占用CPU 0
* 占用物理内存 129540
* 占用虚拟内存  440000
* 启动时间 Oct06
* 启动用户 nobody


## pidstat
pidstat主要用于监控全部或指定进程占用系统资源的情况，如CPU，内存、设备IO、任务切换、线程等。pidstat首次运行时显示自系统启动开始的各项统计信息，之后运行pidstat将显示自上次运行该命令以后的统计信息。用户可以通过指定统计的次数和时间来获得所需的统计信息。


### 内存使用情况统计

内存使用情况统计「-r」

```
[root@img1_u redis_data]# pidstat -p 12934 -r 1
Linux 2.6.32-431.11.7.el6.ucloud.x86_64 (img1_u) 	12/15/2015 	_x86_64_	(8 CPU)

12:55:52 PM       PID  minflt/s  majflt/s     VSZ    RSS   %MEM  Command
12:55:53 PM     12934    167.00      0.00 9173108 9039032  36.83  redis-server
12:55:54 PM     12934    298.00      0.00 9173108 9039032  36.83  redis-server
12:55:55 PM     12934    380.00      0.00 9173108 9039032  36.83  redis-server
12:55:56 PM     12934    182.00      0.00 9173108 9039032  36.83  redis-server
12:55:57 PM     12934    224.00      0.00 9173108 9039032  36.83  redis-server
```
### IO使用情况统计

IO使用情况统计「-d」

使用「-d」选项，可以查看进程IO的统计信息

命令 ：「pidstat -p 26724 -d 1」

```
[root@img1_u ~]# pidstat -p 26724 -d 1
Linux 2.6.32-431.11.7.el6.ucloud.x86_64 (img1_u) 	12/15/2015 	_x86_64_	(8 CPU)

12:43:04 PM       PID   kB_rd/s   kB_wr/s kB_ccwr/s  Command
12:43:05 PM     26724      0.00  59756.00      0.00  redis-server
12:43:06 PM     26724      0.00  62368.00      0.00  redis-server
12:43:07 PM     26724      0.00  62428.00      0.00  redis-server
12:43:08 PM     26724      0.00  61824.00      0.00  redis-server
12:43:09 PM     26724      0.00  62040.00      0.00  redis-server
```
由于redis fork一个进程，用于写RDB文件。 该进程写入的速度大概是 60M/s


输出含义;

* kB_rd/s: 每秒进程从磁盘读取的数据量(以kB为单位)
* kB_wr/s: 每秒进程向磁盘写的数据量(以kB为单位
* Command  进程 启动命令

### cpu使用情况统计

 cpu使用情况统计「-u」

使用 「-u」选项，pidstat将显示各活动进程的cpu使用统计

命令 「pidstat -p 12934 1」
```
[root@img1_u redis_data]# pidstat -p 12934 1
Linux 2.6.32-431.11.7.el6.ucloud.x86_64 (img1_u) 	12/15/2015 	_x86_64_	(8 CPU)

12:49:29 PM       PID    %usr %system  %guest    %CPU   CPU  Command
12:49:30 PM     12934    3.00    2.00    0.00    5.00     0  redis-server
12:49:31 PM     12934    1.00    2.00    0.00    3.00     0  redis-server
12:49:32 PM     12934    1.00    3.00    0.00    4.00     0  redis-server
12:49:33 PM     12934    2.00    1.00    0.00    3.00     0  redis-server
12:49:34 PM     12934    1.00    1.00    0.00    2.00     0  redis-server
12:49:35 PM     12934    2.00    2.00    0.00    4.00     0  redis-server
```

## sar
### 监控cpu颈瓶
命令 「sar -u -P ALL 2」

```
16时07分16秒     CPU     %user     %nice   %system   %iowait    %steal     %idle
16时07分18秒     all     42.90      0.00     10.47      7.38      0.00     39.24
16时07分18秒       0     44.22      0.00     10.55     21.61      0.00     23.62
16时07分18秒       1     42.86      0.00     11.22     14.80      0.00     31.12
16时07分18秒       2     41.62      0.00     12.18      1.52      0.00     44.67
16时07分18秒       3     43.15      0.00     10.66      9.64      0.00     36.55
16时07分18秒       4     43.94      0.00      9.09      1.01      0.00     45.96
16时07分18秒       5     41.92      0.00     11.11      1.01      0.00     45.96
16时07分18秒       6     42.71      0.00      9.55      3.02      0.00     44.72
16时07分18秒       7     41.71      0.00     10.05      7.04      0.00     41.21
```

命令 「sar -q  2」
```
16时08分36秒   runq-sz  plist-sz   ldavg-1   ldavg-5  ldavg-15
16时08分38秒        22       440      7.80      3.55      1.35
16时08分40秒        13       440      7.80      3.55      1.35
16时08分42秒        13       440      7.50      3.55      1.36
16时08分44秒         0       440      7.50      3.55      1.36
16时08分46秒         9       440      8.34      3.79      1.45
```

命令解释
* -q 运行队列的意思
* 2 表示每2秒采样一次

输出项说明：
* runq-sz：运行队列的长度（等待运行的进程数）
* plist-sz：进程列表中进程（processes）和线程（threads）的数量
* ldavg-1：最后1分钟的系统平均负载（System load average）
* ldavg-5：过去5分钟的系统平均负载
* ldavg-15：过去15分钟的系统平均负载


### 监控内存颈瓶

### 监控IO颈瓶

## mpstat
mpstat是MultiProcessor Statistics的缩写,是实时系统监控工具。 在多核的系统里，不但能查看
所有CPU的平均情况，还能查看特定的CPU使用状况

```
14时20分24秒  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
14时20分27秒  all   30.61    0.00    8.14    7.63    0.00    0.04    0.00    0.00   53.58
14时20分27秒    0   31.21    0.00    9.06   14.09    0.00    0.34    0.00    0.00   45.30
14时20分27秒    1   32.77    0.00    9.12   28.38    0.00    0.00    0.00    0.00   29.73
14时20分27秒    2   31.19    0.00    8.47    2.03    0.00    0.00    0.00    0.00   58.31
14时20分27秒    3   32.09    0.00    8.78    8.78    0.00    0.00    0.00    0.00   50.34
14时20分27秒    4   31.08    0.00    7.09    0.68    0.00    0.00    0.00    0.00   61.15
14时20分27秒    5   30.67    0.00    8.00    2.00    0.00    0.33    0.00    0.00   59.00
14时20分27秒    6   28.19    0.00    7.05    2.01    0.00    0.00    0.00    0.00   62.75
14时20分27秒    7   27.80    0.00    7.80    3.05    0.00    0.00    0.00    0.00   61.36
```

参数的含义:

- user     表示处理用户进程所使用 CPU 的百分比。
- system   表示内核进程使用的 CPU 百分比  
- iowait   表示等待IO完成 所使用的 CPU 时间百分比  
- irq      表示用于处理系统中断的 CPU 百分比  
- soft     表示用于软件中断的 CPU 百分比  
- idle     显示 CPU 的空闲时间比例


> mpstat跟vmstat的区别: mpstat 可以统计每个CPU的信息。 如果是ALL的话，那么统计的是平均时间
> vmstat 统计的是所有cpu

有些进程比如mysql,可以跑在多个处理器上。 而像redis 这种应该程序，只绑定在一个cpu上，
从而导致一个 CPU 过载，而其他 CPU 却很空闲。通过 mpstat 可以轻松诊断这些类型的问题。


## iostat
![iostat.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/17/a514960d3500ef488f84048c63a4a9b8.png )

输出解析:
 * rrqm/s 每秒这个设备相关的读取请求有多少被Merge
 * wrqm/s 每秒这个设备相关的写入请求有多少被Merge
 * r/s 每秒读次数
 * w/s 每秒写次数
 * rkB/s 每秒读取字节数
 * wkB/s 每秒写入字节数
 * avgrq-sz 平均每次设备I/O操作的数据大小(扇区)。
 * avgqu-sz 平均I/O队列长度。
 * await  平均每次设备I/O操作的等待时间(毫秒)。
 * svctm  每次完成IO请求的时间。 反过来每一个IO请求的处理的平均时间
 * %util  一秒中有百分之多少的时间用于I/O操作

```
 平均单次IO大小(IO Chunk Size) <=> avgrq-sz
 平均IO响应时间(IO Response Time) <=> await
 IOPS(IO per Second) <=> r/s + w/s
 吞吐率(Throughtput) <=> rkB/s + wkB/s
```
在进入到操作系统的设备层(/dev/sda)之后，计数器开始对IO操作进行计时，最终的计算结果表现是await，这个值就是我们要的IO响应时间了；svctm是在IO操作进入到磁盘控制器之后直到磁盘控制器返回结果所花费的时间，这是一个实际IO操作所花的时间,当await与svctm相差很大的时候，我们就要注意磁盘的IO性能了.


如何理解await
  * 包含在队列中的时间和服务时间
  * 如果await 和 svctm 相差很大，那么一定表示等待过久，磁盘繁忙

### iostat 案例分析

**例子一:**
```
avgrq-sz avgqu-sz   await  svctm  %util
83.02    22.58   33.95   1.38  91.80

avgrq-sz avgqu-sz   await  svctm  %util
72.26    11.20   28.00   2.31  92.30
```

查看第二行: 「await」是 33.95，「svctm」是1.38 await 和 svctm 不在一个数量级
所以磁盘的压力有点大


**例子二:**
```
avgrq-sz avgqu-sz   await  svctm  %util
13.01     1.62    5.53   3.45  98.70
avgrq-sz avgqu-sz   await  svctm  %util
13.03     1.56    5.63   3.47  98.30
```
查看第二行: 「await」是 5.53，「svctm」是3.45 await 和 svctm 相差不大




### 如何判定磁盘性能问题
如何看磁盘性能问题:
* await与svctm相差很大


## vmstat
```
procs -----------memory---------- ---swap-- -----io---- --system-- -----cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
28  3      0 23014368 170692 740488    0    0     0 15444 15249 75987 46 12 36  6  0
 0  4      0 23014560 170692 740488    0    0     0 20868 16752 82086 49 12 31  7  0
 0  3      0 23014252 170692 740492    0    0     0 20176 15664 77874 48 12 32  8  0
 1  2      0 23014624 170692 740492    0    0     0 19008 13234 65379 38 10 42 10  0
 0  3      0 23014780 170692 740492    0    0     0 22988 14216 69369 44 10 39  7  0
17  2      0 23014236 170692 740492    0    0     0 19428 9155 41659 28  7 51 14  0
24  1      0 23014108 170692 740492    0    0     0 18944 13841 69258 41 10 39  9  0
```

输出参数说明:

Procs
 * R:等待被执行的进程数，即表示运行和等待CPU时间片的进程数
 * B:排队的进程数，即等待资源的进程数


Memory
 * Swap : 虚拟内存，切换到虚拟内存的内存大小
 * Free: 空闲的物理内存大小
 * Buff: 缓冲区大小
 * Cache: 缓存大小

Swap
 * Si:磁盘写入虚拟内存，即由内存进入到虚拟内存的大小。
 * So:虚拟内存写入磁盘，即由虚拟内存进入到磁盘的大小。

IO
 * Bi:由块设备读入的数据总量，读磁盘
 * Bo:由块设备写入的数据总量，写磁盘

System
 * In: 每秒设备中断数
 * Cs:每秒上下文切换的次数

Cpu
 * Us:用户进程消耗cpu百分比
 * Sy:内核进程消耗cpu百分比
 * Id:cpu处于空闲状态的时间百分比
 * Wa：Io等待cpu所占时间的百分比

## lsof

### lsof 基础

lsof基本命令  

```
不加参数，后面跟文件名: 某个文件正在被哪些进程访问
-c 程序名  $1
-p 进程id  $3
-u 用户名  $4
```

lsof 显示字段 

```
COMMAND     PID      USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
```
查看某个文件被哪个进程访问 

```
shell > lsof /etc/hosts
```
查看mysqld进程打开的文件 方法一：通过进程名

```
lsof  -c mysqld
lsof  -c nginx
```
方法二:通过进程id

```
lsof -p $(pidof mysqld)
lsof -p $(pidof nginx)
```
方法三:通过 awk 或grep过滤

```
lsof -n | awk '$1 ~ /mysqld/'
```
 查看打开文件的数量最多的前30个进程 

```
shell > lsof -n |awk '{print $2}'|sort|uniq -c |sort -nr|head -30
```
 查看进程mysqld打开的数量 

```
shell > lsof -n | awk '$1 ~ /mysqld/ ' | wc -l
```
 查看mysql用户打开文件的数量   方法一:

```
lsof -n | awk '$3 ~ /mysql/' | wc -l
```
 方法二: 参数 -u 

```
lsof -u mysql | wc -l
```
 查看端口运行的进程 

```
lsof -i:8099
```
 通过-i 选项，lsof列出所有打开网络套接字(TCP和UDP)的进程。i internet 

```
shell>  lsof -i tcp:3306
...
COMMAND PID USER   FD   TYPE    DEVICE SIZE/OFF NODE NAME
haproxy 372 root    5u  IPv4 776907118      0t0  TCP *:mysql (LISTEN)
```
查看53端口哪个程序在使用 

同时查看tcp和udp 

```
shell>  lsof -i :53
```
只查看tcp 

```
shell>  lsof -i tcp:53
```
只查看udp 

```
shlle> lsof -i :1194
...
COMMAND   PID USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
openvpn 31054 root    5u  IPv4 69326827      0t0  UDP *:openvpn
```

查询DNS 端口 53
```
shell> lsof -i :53
...
COMMAND   PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
dnsmasq 14369 nobody    4u  IPv4 106164      0t0  UDP *:domain
dnsmasq 14369 nobody    5u  IPv4 106165      0t0  TCP *:domain (LISTEN)
dnsmasq 14369 nobody    6u  IPv6 106166      0t0  UDP *:domain
dnsmasq 14369 nobody    7u  IPv6 106167      0t0  TCP *:domain (LISTEN)
```
### 使用lsof分析打开的文件

lsof打印后的结果格式如下 
```
COMMAND   PID  USER   FD   TYPE             DEVICE   SIZE/OFF      NODE NAME
mysqld  20692 mysql    4uW  REG                8,2 5999951872  27723478 /usr/local/mariadb/data/ibdata1
mysqld  20692 mysql    9uW  REG                8,2   67108864  27723479 /usr/local/mariadb/data/ib_logfile
```

格式说明如下 
```
第一列:命令名
第二列:进程号
第三列:用户名
第四列:文件描述符
第五列:类型
第九列:文件名

```

 lsof 用fd建立关联数组 
```
#!/bin/bash

lsof -p $(pidof mysqld) | \
awk '
    /^COMMAND/ { mode = "lsof";   }
    /^Process/ { mode = "strace"; }
    

        {
            if ($5 == "REG"){
                fd=$4;
                gsub(/[uW].*/,fd,"")
                for_filelist[fd]=$9
            }
        }
        END{
            printf("MODE:%s\n",mode)
            for(fd in for_filelist){
                printf("%-3d\t%-20s\n",fd,for_filelist[fd])
            }
        }
'
```

### 检查打开的数据文件和日志文件

查看打开mysql的innodb 日志文件 

```
shell > lsof -p $(pidof mysqld) | grep ib_log
....
mysqld  28535 mysql    9uW  REG                8,2 67108864  27068766 /usr/local/percona/data/ib_logfile0
mysqld  28535 mysql   10uW  REG                8,2 67108864  27068767 /usr/local/percona/data/ib_logfile1
```
> 文件描述符是:9 和 10

查看打开的innodb 数据文件

```
shell > lsof -p $(pidof mysqld) | grep ibdata
....
mysqld  28535 mysql    4uW  REG                8,2 18874368  27068765 /usr/local/percona/data/ibdata1
```
> 文件描述符是:4。想想为什么不用「pgrep」。使用「pgrep」将得到两个进程号，mysqld和mysqld_safe两个进程 记住: pidof是精确匹配, pgrep 是模糊匹配。所以，强制停止mysqld服务器时，使用下面命令
「killall mysqld mysqld_safe」


### pt-ioprofile脚本lsof中的应用
lsof 格式 

```
mysqld  10439 mysql    9uW  REG                8,2   67108864  27723479 /usr/local/mariadb/data/ib_logfile0
mysqld  10439 mysql    4uW  REG                8,2 5999951872  27723478 /usr/local/mariadb/data/ibdata1
```
文件描述符和文件名对应关系 

```
lsof -p $(pidof mysqld) |\
 awk '
    $5 ~ /REG/
    {
        gsub(/[rwu-].*/, "", $4);filename_for[$4] =$9
    }
    END{
        for(fd in filename_for)
            print fd, filename_for[fd]
    }
    '
```
模拟二维数组 

```
10756 pwrite 9 1536 0.000019 /usr/local/mariadb/data/ib_logfile0
10756 write 90 835 0.000018 /usr/local/mariadb/data/mysql-bin.000079
10756 pwrite 9 512 0.000016 /usr/local/mariadb/data/ib_logfile0
10756 pwrite 9 1536 0.000021 /usr/local/mariadb/data/ib_logfile0
10756 write 90 835 0.000018 /usr/local/mariadb/data/mysql-bin.000079
```
```
cat tabulated_samples |\
awk '{file[$6 "," $2] += 1}
END{
    for (f in file){
        split(f,arr,",")
        print arr[1],arr[2],file[f]
        }
    }
'
```
源数据

```
[pid 10756] pwrite(9, ""..., 512, 50402304) = 512 <0.000009>
```
系统调用函数 

```
wanted_pat  = "read|write|sync|open|close|getdents|seek|fcntl|ftrunc";
```
得到pid 

```
pid = substr($2, 1, length($2) - 1);
```
放入全局数组 filename_for 

```
filename_for[fd] = $9;
```
 系统调用的函数名 

```
funcn = substr($3, 1, index($3, "(") - 1);
```
 文件描述符 

```
fd  = substr($3, index($3, "(") + 1);
```


## ss

## netstat

netstat命令用户显示网络连接信息，显示与IP、TCP、UDP和ICMP协议相关的统计数据


常见的命令行参数

* -t 仅显示tcp连接信息
* -u 仅显示udp连接信息
* -n 把主机名显示为ip地址 数字形式
* -p pid 程序进程id
* -l listen 程序在监听
* -r 路由表 route信息

### 显示路由表信息

![屏幕快照 2015-12-20 下午5.01.21.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/20/fc970c8fc4f0429449c6e965fbb1cc43.png "屏幕快照 2015-12-20 下午5.01.21.png")

> 除了 netstat -r 。也可以用「ip route」命令

### 查看监听的端口

![屏幕快照 2015-12-20 下午5.01.31.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/20/68fc42bebe8693f0658a85ff6981c04b.png )


### 查询TCP的状态信息
![屏幕快照 2015-12-20 下午5.11.04.png](http://7d9op5.com1.z0.glb.clouddn.com/2015/12/20/aff3480db3fedef643386f671ac01d26.png )

脚本 ```netstat -tn | awk '/^tcp/ {s[$NF]++} END {for(i in s) print i, s[i]}'```解释：



默认 「netstat -tn」输出的字段如下。
```
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address               Foreign Address             State
tcp        0      0 10.10.74.19:80              42.62.37.181:35386          TIME_WAIT
```

> 通过「awk」工具，匹配第一列为tcp。「s」表示关联数组的名称。「$NF」，最后一列的值。
awk的关联数组会经常用到。所以一定要熟练该用法


## strace

通过strace可以跟踪到一个进程产生的系统调用,包括参数，返回值，执行消耗的时间。
我通过strace解决了很多系统的故障，以及对于理解应用程序的内在机制也大有裨益。


### strace 基本使用方法

```
-p 跟踪指定的进程
-f 跟踪由fork子进程系统调用
-F 尝试跟踪vfork子进程系统调吸入，与-f同时出现时, vfork不被跟踪
-o filename 默认strace将结果输出到stdout。通过-o可以将输出写入到filename文件中
-ff 常与-o选项一起使用，不同进程(子进程)产生的系统调用输出到filename.PID文件
-r 打印每一个系统调用的相对时间
-t 在输出中的每一行前加上时间信息。 -tt 时间确定到微秒级。还可以使用-ttt打印相对时间
-v 输出所有系统调用。默认情况下，一些频繁调用的系统调用不会输出
-s 指定每一行输出字符串的长度,默认是32。文件名一直全部输出
-c 统计每种系统调用所执行的时间，调用次数，出错次数。
-e expr 输出过滤器，通过表达式，可以过滤出掉你不想要输出
-T  Show the time spent in system calls.   
```
> strace可以使用参数-T将每个系统调用所花费的时间打印出来，
每个调用的时间花销现在在调用行最右边的尖括号里面。
> -f 参数，fork进程

```
shell > strace -f ./mysqld_safe --user=mysql 2>&1 | grep ib_logfile
...
[pid  1139] open("./ib_logfile0", O_RDWR|O_CREAT|O_EXCL, 0660) = -1 EEXIST (File exists)
[pid  1139] open("./ib_logfile0", O_RDWR) = 4
[pid  1139] open("./ib_logfile1", O_RDWR|O_CREAT|O_EXCL, 0660) = -1 EEXIST (File exists)
[pid  1139] open("./ib_logfile1", O_RDWR) = 4
[pid  1139] open("./ib_logfile0", O_RDWR) = 9
[pid  1139] open("./ib_logfile1", O_RDWR) = 10
```


对于输出的解释：每一行都是一个系统调用，等号左边的系统调用函数名，等号右边是调用的返回值。由于Mysql启动时，默认读取两个文件「ib_logfile0」和「ib_logfile1」

常见的坑
  - 参数「-f」，因为mysql的io_thread是「fork」出来的，所以要加「-f」参数
  - 「2>&1」 strace输出的结果输出到标准错误中。所以需要「2>&1」
  - 参数「-T」，系统调用的时间
  - 参数「-e」，过滤指定的系统函数


统计跟IO 有关的

```
strace -f  -e open,pwrite,fsync,fdatasync ./mysqld_safe --user=mysql 2>&1
```

pt-ioprofile脚本的strace用法

```
strace -T -s 0 -f -p $proc_pid >> "$samples" 2>&1 &
```

### strace 跟踪mysqld启动进程
```
strace -f -t  -e fdatasync ./mysqld_safe --user=mysql 2>&1 | grep fdatasync\(9\)
```
参数说明
 * -f 跟踪fork进程
 * -e 只打印fdatasync的系统调用
 * -t 显示系统时间
 * ./mysqld_safe --user=mysql 启动mysqld_safe
 * 2>&1
 *  grep fdatasync\(9\): 只打印文件描述符为9的fdatasync系统调用。

> 文件描述符9是打开的一个redo log日志


### strace 统计nginx进程信息

方法一: -c 参数，统计所有的耗时操作
```
  strace -c  $(pgrep nginx | awk '{print "-p " $0}')
```


''pgrep 和pidof 显示的结果是不一样的,pgrep 一个进程号显示一行，pidof一行显示多个进程号''
```
strace -c `pidof nginx | awk '{while(i++ <NF) print "-p", $i}'`
```

方法二: 自己脚本过滤
2.1 跟踪所有的nginx进程，并输出到nginx.strace文件中

```
  strace -T  $(pgrep nginx | awk '{print "-p " $0}') -o nginx.strace
```

查询耗时的操作
```
cat nginx.strace | awk '{a=$NF;gsub(/[<>]/,"",a);print a}' | sort -nr | head -10
```

根据指定的时间查找
```
cat nginx.strace | grep -A5 耗时时间
```
### strace 举例

strace 跟踪多个进程 sed版：
```
strace `pidof php-cgi | sed 's/\([0-9]*\)/-p \1/g'`
```
```
strace `pidof php-fpm | sed 's/\([0-9]*\)/-p \1/g'`
```

strace 跟踪执行的mysql语句
```
strace -f -F -ff -o mysqld-strace -s 1024 -p $(pidof mysqld)
find mysqld-strace.*  -exec grep -Hni 'insert' {} \;
```

* 不同的fork进程，输出到不同的文件
* -ff 常与-o选项一起使用，不同进程(子进程)产生的系统调用输出到filename.PID文件

### strace 统计php-cgi 进程信息

```
strace -c $(pgrep php-cgi | awk '{print "-p",$0 }')
```


### strace 解决 502 错误

当时我们线上有个团购业务，每次点击该页面都随机出现502错误。首先通过前端负载均衡器「nginx」排查，出现502错误的机器，只有其中一台服务器出现。接着我们在负载均衡器上去掉了该台后端服务器，虽然暂时解决了「502」的问题，但现在需要查找为什么
那台机器当执行那个页面时，会出现502错误。我通过调整「fpm」参数，然后，使用「strace」命令，跟踪所有的系统调用，结果发现如下的输出

```
lstat64("/webwww", {st_mode=S_IFDIR|0755, st_size=4096, ...}) = 0
lstat64("/webwww/shop2", {st_mode=S_IFDIR|0755, st_size=4096, ...}) = 0
lstat64("/webwww/shop2/log", {st_mode=S_IFDIR|0755, st_size=4096, ...}) = 0
lstat64("/webwww/shop2/log/execurl.log", {st_mode=S_IFREG|0644, st_size=2147483647, ...}) = 0
open("/webwww/shop2/log/execurl.log", O_WRONLY|O_CREAT|O_APPEND, 0666) = 8
fstat64(8, {st_mode=S_IFREG|0644, st_size=2147483647, ...}) = 0
lseek(8, 0, SEEK_CUR)                   = 0
lseek(8, 0, SEEK_CUR)                   = 0
write(8, "===========\350\216\267\345\217\226\346\225\260\346\215\256========="..., 34) = -1 EFBIG (File too large)
--- SIGXFSZ (File size limit exceeded) @ 0 (0) ---
Process 20876 detached
[root@boqii9 logs]# du -sh /webwww/shop2/log/execurl.log
2.1G    /webwww/shop2/log/execurl.log
[root@boqii9 logs]# rm -rf /webwww/shop2/log/execurl.log
[root@boqii9 logs]# mv /webwww/shop2/log/execurl.log /webwww/shop2/log/execurl.log2
[root@boqii9 logs]# strace -p 20876
```

php出现502的问题
通过php读取超过2G的文件时，提示File size limit exceeded。
删除 「/webwww/shop2/log/execurl.log」文件后，该页面「502」的问题不再复现，后来通过查询资料
得知32位的系统「fpm」进程读取超过2G文件时，「fpm」进程都会挂掉。因此，删除该日志文件后，故障恢复。

### strace 解决sshd登录慢的问题

新安装的一台linux服务器，每次远程登录，都超级慢，因此想看看到底什么原因导致了慢。
假设通过系统命令，得到「sshd」的进程ID为「24428」，然后通过「strace」命令跟踪系统调用


「strace -o sshd.strace -fT -p 24428」

生成了「sshd.strace」文件，然后查找耗时的操作
```
cat sshd.strace | awk '{a=$NF;gsub(/[<>]/,"",a);print a}' | sort -nr | head -3
...
5.655878
5.521372
5.000016

```
> 有多个「5」秒的超时调用，然后去定位其中一个耗时为「5.000016」的相关系统调用


```
cat sshd.strace | grep -B5 5.000016
....
28398 connect(4, {sa_family=AF_INET, sin_port=htons(53), sin_addr=inet_addr("118.114.114.114")}, 28) = 0 <0.000027>
28398 fcntl(4, F_GETFL)                 = 0x2 (flags O_RDWR) <0.000020>
28398 fcntl(4, F_SETFL, O_RDWR|O_NONBLOCK) = 0 <0.000021>
28398 poll([{fd=4, events=POLLOUT}], 1, 0) = 1 ([{fd=4, revents=POLLOUT}]) <0.000023>
28398 sendto(4, "\207/\1\0\0\1\0\0\0\0\0\0\0012\00222\003168\003192\7in-add"..., 43, MSG_NOSIGNAL, NULL, 0) = 43 <0.000050>
28398 poll([{fd=4, events=POLLIN}], 1, 5000) = 0 (Timeout) <5.000016>
```

### strace 分析mysql客户端走的协议

由于 「mysql -h localhost」老是报错，「Can't connect to local MySQL server through socket '/tmp/mysql.sock'」。但我已正常启动mysql。现在要分析mysql客户端
指定「-h localhost」。走「TCP」协议，还是读取「socket」文件

方法一:使用lsof分析
如果是以「-h 127.0.0.1」的方式的话，走tcp协议

```
lsof -p 7056
...
mysql   7056 root    3u  IPv4 681529      0t0       TCP db3.boqii.com:41579->db3.boqii.com:mysql (ESTABLISHED)
```

如果是以「-h localhost」的方式的话，走socket文件

```
lsof -p 6382
....
mysql   6382 root    3u  unix 0xffff81042d0c68c0      0t0    681370 socket
```


方法二:使用strace分析
如何查看当前mysql客户端走的是哪个socket文件
```
strace -f  mysql -hlocalhost -u aa -p123456 2>&1 | grep -i sock
...
socket(PF_FILE, SOCK_STREAM, 0)         = 3
socket(PF_FILE, SOCK_STREAM, 0)         = 3
connect(3, {sa_family=AF_FILE, path="/tmp/mysql.sock"...}, 110) = 0
```


为什么不指定host的情况下，默认走的是socket协议
```
strace -f  mysql  -u aa -p123456 2>&1
...
socket(PF_FILE, SOCK_STREAM, 0)         = 3
fcntl(3, F_SETFL, O_RDONLY)             = 0
fcntl(3, F_GETFL)                       = 0x2 (flags O_RDWR)
connect(3, {sa_family=AF_FILE, path="/tmp/mysql.sock"...}, 110) = 0
```
通过strace命令跟踪，得到默认不添加host选项时，读取「/tmp/mysql.sock」文件

当主机指定参数为「-h 127.0.0.1 」时，走tcp协议
```
strace -f  mysql -h127.0.0.1  -u aa -p123456 2>&1
...
connect(3, {sa_family=AF_INET, sin_port=htons(3306), sin_addr=inet_addr("127.0.0.1")}, 16) = 0

```

总结:
* 「-h localhost」 mysql客户端读写socket文件
* 「-h 127.0.0.1」 mysql客户端走TCP协议

### strace 和awk结合显示时间
awk显示时间

```
echo "" | awk '{print strftime("%T",systime()),$0 }'
```

awk和vmstat 结合

```
vmstat 1| awk '{print strftime("%T",systime()),$0 }'
```


监控一个日志文件每秒新增的数量

perl版本
```
tail -F access.log | perl -ne 'print time(), "\n";' | uniq -c
```

awk版本
```
tail -F access.log | awk '{print systime()}' | uniq -c
```

### strace 查看脚本执行的位置

我们的一个定时任务在命令行下执行，通过「top」命令得到该php进程ID为「29711」
由于该脚本默认没有标准输出，因为当我需要知道该程序已经执行到什么位置时，只能通过使用「strace」查看目前执行的位置。由于该脚本要往多个接口发起请求，并且已经带有关键字「router」，所以我通过「strace」命令就能查看想要的结果。

```
strace -p 29711 2>&1 -s 4096 | grep router
```

## ltrace

## tcpdump

## sysdig

