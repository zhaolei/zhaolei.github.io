---
layout: post
title: quantopian-学习笔记
categories: Python 股票
---
## 函数介绍

### initialize 函数
* 接受context做为输入
* 脚本开始执行一次
* 放信息的初级化
* 每个脚本必须有这个函数


### handle_data 函数
* 接受context, data做为输入
* 每分钟执行一次
* 

### before_trading_start 函数
* 每日交易前完成data.current(sid(24), 'price')
* 接受context,data作为输入

### sid 函数
* 接受

### order_target_percent 函数
* 下单

    order_target_percent(sid(24), 0.50)
    order_target_percent(sid(24), -0.50)
### data.current 函数
* 打印当前价格

    data.current([sid(24), sid(8554)], ['low', 'high'])
    data.current([sid(24), sid(8554)], 'price')
    
### data.can_trade 函数

* 检查是否可以交易

    data.can_trade(sid(24))

---




  