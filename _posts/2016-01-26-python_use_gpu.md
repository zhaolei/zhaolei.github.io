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

配置 theano * ~/.theanorc
<pre>
<code>
[global] 
device = gpu
floatX = float32
[nvcc] 
fastmath = True
</code>
</pre>
设置环境变量

export CUDA_ROOT=/usr/local/cuda
配置到 .bashrc 或者其他启动执行脚本

然后运行程序：
<pre>
<code>
from theano import function, config, shared, sandbox
import theano.tensor as T
import numpy
import time

vlen = 10 * 30 * 768  # 10 x #cores x # threads per core
iters = 10000

rng = numpy.random.RandomState(22)
x = shared(numpy.asarray(rng.rand(vlen), config.floatX))
f = function([], T.exp(x))
print(f.maker.fgraph.toposort())
t0 = time.time()
for i in xrange(iters):
    r = f()
t1 = time.time()
print("Looping %d times took %f seconds" % (iters, t1 - t0))
print("Result is %s" % (r,))
if numpy.any([isinstance(x.op, T.Elemwise) for x in f.maker.fgraph.toposort()]):
    print('Used the cpu')
else:
    print('Used the gpu')

</code>
</pre>

如果配置了cuda则 结果如下
<pre>
<code>
stone@stone-SVF15327SCW:~$ python gpu_test.py 
Using gpu device 0: GeForce GT 740M
[GpuElemwise{exp,no_inplace}(<CudaNdarrayType(float32, vector)>), HostFromGpu(GpuElemwise{exp,no_inplace}.0)]
Looping 10000 times took 12.144947 seconds
Result is [ 1.23178029  1.61879349  1.52278066 ...,  2.20771813  2.29967761
  1.62323296]
Used the gpu
</code>
</pre>
能看到输出了我显卡型号 耗时大约 14s

如果没有配置cuda则输出如下：
<pre>
<code>
stone@stone-SVF15327SCW:~$ python gpu_test.py 
[Elemwise{exp,no_inplace}(<TensorType(float64, vector)>)]
Looping 10000 times took 52.600777 seconds
Result is [ 1.23178032  1.61879341  1.52278065 ...,  2.20771815  2.29967753
  1.62323285]
Used the cpu
</code>
</pre>
耗时大约 55s

---

mxnet gpu使用方法
>mxnet如果要使用gpu则需要在编译的时候就要支持cuda;

修改mxnet config.mk

改动3个地方 , 代码如下
<pre>
<code>
USE_CUDA = 1
USE_CUDA_PATH=/usr/local/cuda
USE_BLAS = atlas
</code>
</pre>
USE_BLAS = atlas 可根据情况如果安装登录openblas则改成openblas

然后make -j4 编译完成 即可;

使用方法如下:
<pre>
<code>
>>> import mxnet as mx
>>> a = mx.nd.empty((2, 3), mx.gpu()) # create a 2-by-3 matrix on gpu 0
>>> b = mx.nd.empty((2, 3), mx.gpu()) # create a 2-by-3 matrix on gpu 0
>>> c = a+b
</code>
</pre>
如果没有 mx.gpu() 则默认使用cpu()




