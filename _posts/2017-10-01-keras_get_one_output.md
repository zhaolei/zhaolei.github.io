---
layout: post
title: keras读取模型某一层的输出 
categories: python 
---


>  keras提供很多训练好的模型 vgg16,vgg19,InceptionV3等如何获取这些模型的某一层的输出
> 这些模型每个模型都有超过10个层，如果想检查中间的某层输出如何操作

--- 

### 1. 加载模型

* 以vgg16为例

```python
from keras.applications.vgg16 import VGG16

model = VGG16(weights='imagenet', include_top=False)
print(model.layers)
```

* 如果第一次使用vgg16则模型需要一段时间下载，下载完成下次就会直接加载 下载完保存在(~/.keras/models/)目录
* 加载完可以看到 输出一个list每一项为一layer


---

### 2. 定义输出中间层layer模型

* 下面代码定义个输出第3层的模型

```python
from keras.models import Model

layer_model = Model(inputs=model.input, outputs=model.layers[3].output)

```

* 定义好的layer_model就是输出第3层

---

### 3. 完整的测试代码

```python
from keras.applications.vgg16 import VGG16
from keras.preprocessing import image
from keras.applications.vgg16 import preprocess_input
from keras.models import Model
import numpy as np
import pylab

base_model = VGG16(weights='imagenet')
layer_model = Model(inputs=model.input, outputs=model.layers[3].output)

img_path = 'elephant.jpg'
img = image.load_img(img_path, target_size=(224, 224))
x = image.img_to_array(img)
x = np.expand_dims(x, axis=0)
x = preprocess_input(x)

features = model.predict(x)

print(features.shape)
pylab.imshow(features[0][:,:,0])
pylab.show()

```


