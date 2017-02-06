---
layout: post
title:  php扩展实现控制树莓派gpio
categories: php gpio 树莓派 wiringpi
---

>php扩展开发学习，从入门到放弃系列《php扩展实现操作树莓派gpio》

-----
# 准备工作

* php 源码包 
* 树莓派板子
* 伺服电机，led灯,杜邦线

----

# 准备知识

* php,C,makefile
* gpio控制
* 数字电路基本知识

-----
# 准备环境

* raspbian
* php-cli, phpize php-config (需要提前编译一次php)
* 安装WiRingPi (控制gpio库)

---

# 第一步 创建模块

* 熟悉 ext_skel 目录 ext/
* 运行如下图

![help][1]

* 用extame创建新模块

![create][2]

* 创建完成并告知 后续操作
-----

# 第二步 打开编译选项

> 如果几乎动态编译php模块则无需修改编译选项

* 修改m4文件， 修改如下图
![m4][3]
* dnl 去掉，dnl表示注释
* 重新生成编译检查信息 如下图

![config][4]

-----

# 第三步  编译空模块，将模块加载到php 

* 重新编译php, 尽量打开调试 --enable-debug ,此选项会在编译中增加代码符号，方便gdb调试(Makefile增加 -g , -O0)

![enter description here][5]

* 编译完成检查 模块是否加载成功

![enter description here][6]

![enter description here][7]
* 看到图中 stonex模块表示模块加载成功

----------
# 第四步 熟悉一下 树莓派 

* gpio如下图针脚功能

![enter description here][8]
* 5v表示5v正极, 0v表示负极，....

----------
# 第五步 gpio库的初始化

* 修改模块中的 stonex.c 文件
* 增加依赖的头文件 

![enter description here][9]
* 增加函数

![enter description here][10]
> 几个关键宏的作用 
> PHP_MINIT_FUNCTION 定义模块初始化 

> PHP_MSHUTDOWN_FUNCTION 定义模块析构

> PHP_RINIT_FUNCTION 定义请求初始化

> PHP_RSHUTDOWN_FUNCTION 定义请求析构

> PHP_MINFO_FUNCTION 模块phpinfo信息输出

> PHP_FUNCTION定义php函数

* 在模块初始化中初始化gpio控制库 wiringpi的初始化 如下图

![enter description here][11]


------------------
# 第六步 实现一个php函数

* 在自定义函数 stonex_gpio_led中，定义函数名，获取函数调用参数，逻辑控制gpio  如下图

![enter description here][12]


---------

# 第七步 动态编译php方便调试

* 生成编译检查信息 phpize

![enter description here][13]
* 运行编译检查 configure

![enter description here][14]
* 编译这个模块

![enter description here][15]
* 查看自己编译的模块 动态链接库 stonex.so

![enter description here][16]
* 修改 php.ini 动态加载stonex

![enter description here][17]

![enter description here][18]
----------
# 最后 测试我们新扩展库

* php 代码 如下
```
<?php
stonex_gpio_led('off');
usleep(1000000);
stonex_gpio_led('on');
usleep(1000000);
stonex_gpio_led('off');
usleep(1000000);
stonex_gpio_led('on');
usleep(1000000);
```
* 运行需要加 sudo 因为wiring库需要root权限


  [1]: http://okyeze2m9.bkt.clouddn.com/c01.png "c01.png"
  [2]: http://okyeze2m9.bkt.clouddn.com/c02.png "c02.png"
  [3]: http://okyeze2m9.bkt.clouddn.com/c03.png "c03.png"
  [4]: http://okyeze2m9.bkt.clouddn.com/c04.png "c04.png"
  [5]: http://okyeze2m9.bkt.clouddn.com/c05.png "c05.png"
  [6]: http://okyeze2m9.bkt.clouddn.com/c06.png "c06.png"
  [7]: http://okyeze2m9.bkt.clouddn.com/c07.png "c07.png"
  [8]: http://okyeze2m9.bkt.clouddn.com/c08.png "c08.png"
  [9]: http://okyeze2m9.bkt.clouddn.com/c09.png "c09.png"
  [10]: http://okyeze2m9.bkt.clouddn.com/c10.png "c10.png"
  [11]: http://okyeze2m9.bkt.clouddn.com/c11.png "c11.png"
  [12]: http://okyeze2m9.bkt.clouddn.com/c13.png "c13.png"
  [13]: http://okyeze2m9.bkt.clouddn.com/c13.png "c13.png"
  [14]: http://okyeze2m9.bkt.clouddn.com/c14.png "c14.png"
  [15]: http://okyeze2m9.bkt.clouddn.com/c15.png "c15.png"
  [16]: http://okyeze2m9.bkt.clouddn.com/c16.png "c16.png"
  [17]: http://okyeze2m9.bkt.clouddn.com/c17.png "c17.png"
  [18]: http://okyeze2m9.bkt.clouddn.com/c18.png "c18.png"