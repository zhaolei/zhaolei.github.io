---
layout: post
title: 树莓派安装ros+mavros
categories: 树莓派, raspberry pi, ros, mavros
---

# 树莓派安装ros+mavros

## 经验建议

1. 树莓派如果选4b(其他版本没测过) , 建议安装ubuntu 20, 二进制安装非常容易 (ubuntu 18, raspbian 测试都安装失败 折腾很久都没搞定)
2. 16G的卡足够,不要太大除非特殊需求
3. 刷系统按照正常流程刷tf卡即可
 

## 安装ros

1. 参考[http://wiki.ros.org/noetic/Installation/Ubuntu](http://wiki.ros.org/noetic/Installation/Ubuntu)
2. sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
3. sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
4. sudo apt update
5. 根据需要选一个，不需要界面选最后一个：sudo apt install ros-noetic-desktop-full ，sudo apt install ros-noetic-desktop， sudo apt install ros-noetic-ros-base 
6. 安装完成 设环境变量就可以用:  source /opt/ros/noetic/setup.bash ,
7. 测试一下: roscore 看是否可以使用

## 安装mavros + mavlink
1. 二进制安装: sudo apt-get install ros-noetic-mavros ros-noetic-mavros-extras ros‐noetic‐control‐toolbox
2. 安装完 : roslaunch mavros px4.launch  如果可以打开表示安装完成


参考链接
> http://wiki.ros.org/noetic/Installation/Ubuntu
> https://erlerobotics.gitbooks.io/erle-robotics-mav-tools-free/content/en/installing_mavproxy.html
> https://dev.px4.io/v1.9.0/zh/ros/mavros_installation.html

