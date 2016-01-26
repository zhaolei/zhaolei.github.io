---
layout: post
title: Python使用GPU做计算 
categories: Python GPU mxnet theano 
---

有两个Python库可以使用GPU做计算 mxnet & theano, 两个库的使用各有优缺点;
目前能使用的GPU只有NVidia系列支持CUDA的显卡, 支持gpu计算的mxnet & theano都只能支持cuda. 使用GPU之前需要安装CUDA,如何安装可以google. 比较简单;
如果你的显卡不是nvidia系列,python暂时是没有办法使用;
确保机器有nvidia显卡&已经成功安装cuda ;
使用示例是ubuntu

---


Theano 方案:
* ~/.theanorc

<pre>
<code>

</code>
</pre>

代码示例
<pre>
<code>
>>> import scipy.misc
>>> ascent = scipy.misc.ascent()
>>> ascent.shape
(512, 512)
>>> ascent.max()
255
>>> scipy.misc.imshow(ascent)
</code>
</pre>
---

mxnet方案:



