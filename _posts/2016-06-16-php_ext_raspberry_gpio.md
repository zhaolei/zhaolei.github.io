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
![image](http://chuantu.biz/t5/10/1465987956x1032300884.png)

* 用extname创建新模块
![image](http://chuantu.biz/t5/10/1465988011x1032300884.png)

* 创建完成并告知 后续操作
-----

# 第二步 打开编译选项

> 如果几乎动态编译php模块则无需修改编译选项

* 修改m4文件， 修改如下图
![image](http://chuantu.biz/t5/10/1465988033x1032300884.png)
* dnl 去掉，dnl表示注释
* 重新生成编译检查信息 如下图
![image](http://chuantu.biz/t5/10/1465988051x1032300884.png)

-----

# 第三步  编译空模块，将模块加载到php 

* 重新编译php, 尽量打开调试 --enable-debug ,此选项会在编译中增加代码符号，方便gdb调试(Makefile增加 -g , -O0)
![image](http://chuantu.biz/t5/10/1465988093x1032300884.png)

* 编译完成检查 模块是否加载成功
![image](http://chuantu.biz/t5/10/1465988136x1032300884.png)
![image](http://chuantu.biz/t5/10/1465988147x1032300884.png)
* 看到图中 stonex模块表示模块加载成功

----------
# 第四步 熟悉一下 树莓派 

* gpio如下图针脚功能
![image](http://chuantu.biz/t5/10/1466041947x1032300875.png)
* 5v表示5v正极, 0v表示负极，....

----------
# 第五步 gpio库的初始化

* 修改模块中的 stonex.c 文件
* 增加依赖的头文件 
![image](http://chuantu.biz/t5/10/1466042279x1032300875.png)
* 增加函数
![image](http://chuantu.biz/t5/10/1466042482x1032300875.png)
> 几个关键宏的作用 
> PHP_MINIT_FUNCTION 定义模块初始化 

> PHP_MSHUTDOWN_FUNCTION 定义模块析构

> PHP_RINIT_FUNCTION 定义请求初始化

> PHP_RSHUTDOWN_FUNCTION 定义请求析构

> PHP_MINFO_FUNCTION 模块phpinfo信息输出

> PHP_FUNCTION定义php函数

* 在模块初始化中初始化gpio控制库 wiringpi的初始化 如下图
![image](http://chuantu.biz/t5/10/1466044502x1032300875.png)


------------------
# 第六步 实现一个php函数

* 在自定义函数 stonex_gpio_led中，定义函数名，获取函数调用参数，逻辑控制gpio  如下图
![image](http://chuantu.biz/t5/10/1466046814x1032300875.png)


---------

# 第七步 动态编译php方便调试

* 生成编译检查信息 phpize
![image](http://chuantu.biz/t5/10/1465988174x1032300884.png)
* 运行编译检查 configure
![image](http://chuantu.biz/t5/10/1465988184x1032300884.png)
* 编译这个模块
![image](http://chuantu.biz/t5/10/1465988196x1032300884.png)
* 查看自己编译的模块 动态链接库 stonex.so
![image](http://chuantu.biz/t5/10/1465988208x1032300884.png)
* 修改 php.ini 动态加载stonex
![image](http://chuantu.biz/t5/10/1465988220x1032300884.png)
![image](http://chuantu.biz/t5/10/1466048304x1032300875.png)

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


