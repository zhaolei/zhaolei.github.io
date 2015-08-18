---
layout: post
title: numpy.meshgrid函数使用
categories: Python Numpy
---

Numpy.meshgrid　文档地址　[http://docs.scipy.org/doc/numpy/reference/generated/numpy.meshgrid.html](http://docs.scipy.org/doc/numpy/reference/generated/numpy.meshgrid.html) 

---


---

meshgrid计算两个矩阵的XX 写XX是因为我不知道这个在矩阵里叫什么计算
两个n,m矩阵 meshgrid 计算完成后 输出两个矩阵 N M
N为:
n转为1行 然后重复 m列次行

M为:
m转为1列 然后重复n列次 列
<pre>
<code>
>>> x01 = np.arange(1,3)
>>> x02 = np.arange(2,6)
>>> x01
array([1, 2])
>>> x02
array([2, 3, 4, 5])
>>> x03,x04 = np.meshgrid(x01, x02)
>>> x03
array([[1, 2],
       [1, 2],
       [1, 2],
       [1, 2]])
>>> x04
array([[2, 2],
       [3, 3],
       [4, 4],
       [5, 5]])
>>> x01
array([1, 2])
>>> x03
array([[1, 2],
       [1, 2],
       [1, 2],
       [1, 2]])
>>> x05, x06 = np.meshgrid(x01, x03)
>>> x05
array([[1, 2],
       [1, 2],
       [1, 2],
       [1, 2],
       [1, 2],
       [1, 2],
       [1, 2],
       [1, 2]])
>>> x06
array([[1, 1],
       [2, 2],
       [1, 1],
       [2, 2],
       [1, 1],
       [2, 2],
       [1, 1],
       [2, 2]])
</code>
</pre>



