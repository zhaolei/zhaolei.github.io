---
layout: post
title: numpy使用技巧总结
categories: Python numpy
---

# 总结自己经常使用的numpy技巧总结




```python
%pylab inline
```

    Populating the interactive namespace from numpy and matplotlib


## numpy 矩阵操作技巧

> 定义 一个列表 Va, 转为矩阵Ma （5，2）


```python
Va = numpy.arange(10)
Ma = Va.reshape(5,2)

print(Ma)
```




    array([[0, 1],
           [2, 3],
           [4, 5],
           [6, 7],
           [8, 9]])



###  两个矩阵按列连接


```python
newMa = np.hstack((Ma,Ma))

print(newMa)
```




    array([[0, 1, 0, 1],
           [2, 3, 2, 3],
           [4, 5, 4, 5],
           [6, 7, 6, 7],
           [8, 9, 8, 9]])



### 两个矩阵按行连接


```python
newMa = np.vstack((Ma,Ma))

print(newMa)
```




    array([[0, 1],
           [2, 3],
           [4, 5],
           [6, 7],
           [8, 9],
           [0, 1],
           [2, 3],
           [4, 5],
           [6, 7],
           [8, 9]])



### 按行或者列求矩阵最大值


```python
tmpMa = np.max(Ma,axis=1)

print(tmpMa)
```




    array([1, 3, 5, 7, 9])




```python
tmpMa = np.max(Ma,axis=0)

print(tmpMa)
```




    array([8, 9])




```python
tmpMa = np.max(Ma,axis=1,keepdims=True)

print(tmpMa)
```




    array([[1],
           [3],
           [5],
           [7],
           [9]])




```python
tmpMa = np.max(Ma,axis=0,keepdims=True)

print(tmpMa)
```




    array([[8, 9]])



### 按列或者行求和


```python
np.sum(Ma,axis=0)
```




    array([20, 25])




```python
np.sum(Ma,axis=0,keepdims=True)
```




    array([[20, 25]])




```python
np.sum(Ma,axis=1)
```




    array([ 1,  5,  9, 13, 17])




```python
np.sum(Ma,axis=1,keepdims=True)
```




    array([[ 1],
           [ 5],
           [ 9],
           [13],
           [17]])



### 只取矩阵的特性列或者行


```python
newMa = np.hstack((Ma,Ma))
print(newMa)
```




    array([[0, 1, 0, 1],
           [2, 3, 2, 3],
           [4, 5, 4, 5],
           [6, 7, 6, 7],
           [8, 9, 8, 9]])



#### 只取:0,1,2列


```python
newMa[:,(0,1,2)]
```




    array([[0, 1, 0],
           [2, 3, 2],
           [4, 5, 4],
           [6, 7, 6],
           [8, 9, 8]])



#### 只取: 1,2行


```python
newMa[(1,2),:]
```




    array([[2, 3, 2, 3],
           [4, 5, 4, 5]])



### 矩阵倒置


```python
Ma[::-1]
```




    array([[8, 9],
           [6, 7],
           [4, 5],
           [2, 3],
           [0, 1]])






