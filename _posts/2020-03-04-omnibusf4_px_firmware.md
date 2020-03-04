---
layout: post
title: omnibusf4刷pix ardupilot固件
categories: pix, apm, omnibusf4
---

# omnibusf4 刷pix ardupilot固件

### 1. 刷入DFU驱动(必须) 

1. zadig 管理员方式打开, 菜单 Options=>list All Devices 
2. 在设备列表里选择你的飞控，一定要选对，选成别的usb设备不确定你的那个设备还能不能再用了
3. 选好点 install Driver, 我已经安装过了 显示是 Replace Driver

### 2. 刷bootloader (必须)
1. 下载bootloader [https://github.com/PX4/px4_user_guide/raw/master/assets/flight_controller/omnibus_f4_sd/omnibusf4sd_bl_d52b70cb39.hex](https://github.com/PX4/px4_user_guide/raw/master/assets/flight_controller/omnibus_f4_sd/omnibusf4sd_bl_d52b70cb39.hex) 
2. 刷bootloader 很简单,按着飞控上的boot按钮，接入usb, 松开boot按钮
3. 打开betaflight 刷固件页， 选我们刚下的bootloader 固件， 刷入飞控 

### 3. 刷固件

#### MissionPlanner 刷 ardupilot: rover, ardupilot:plane,ardupilot:copter 
1. 打开MissionPlanner ， 硬件配置 => 安装固件 ，选择好自己要的固件类型 ，按照提示就可以，中间会提示拔一下飞控usb, （提示cubeblock, chilios等都选否)
2. 也可以自己选版本 选自定义固件 https://firmware.ardupilot.org/

#### qgrouncontrol 刷px
1. 打开 qgroundcontrol  ![image.png](attachment:image.png)
2. 按照 提示刷px固件 

### 说明
1. 以后更新固件无需刷DFU和bootloader 

>
链接: https://pan.baidu.com/s/1rSA6LkGrbAvoKChsSVvXQw 提取码: 7wz7 复制这段内容后打开百度网盘手机App，操作更方便哦

