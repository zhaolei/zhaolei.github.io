---
layout: post
title: Scipy.misc模块图片使用
categories: Python Scipy
---

Scipy.misc　模块文档地址　[http://docs.scipy.org/doc/scipy/reference/misc.html#module-scipy.misc](http://docs.scipy.org/doc/scipy/reference/misc.html#module-scipy.misc) 

---

那个美女模特　
<pre>
<code>
>>> import scipy.misc
>>> lena = scipy.misc.lena()
>>> lena.shape
(512, 512)
>>> lena.max()
245
>>> lena.dtype
dtype('int32')
>>> scipy.misc.imshow(lenda)
</code>
</pre>

另一个示例图片
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

读取自定义图片
<pre>
<code>
>>> import scipy.misc
>>> lenda = cipy.misc.imread('lenda.png')
>>> scipy.misc.imshow(lenda)
</code>
</pre>



