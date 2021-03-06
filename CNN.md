
卷积是为了让神经网络理解**平移不变性（translation invariance）**这个概念。
而卷积操作则类似于**滑框搜索**。
将图片分割成不同的小块，
然后通过卷积操作（权重相同的小型神经网络），得到输出矩阵。
为了减小矩阵大小，我们利用一种叫做**最大池化（max pooling）**的函数来降采样（downsample）。
池化层的作用类似于**压缩**,只保留最重要信息。
![池化](https://pic2.zhimg.com/80/v2-c6a065c1c19cf0da251042aee207de01_hd.jpg "池化")

池化之后，一般需要全连接层，进行预测。
