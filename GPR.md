## 总结一下高斯过程回归(GPR)


假设训练集中的三个点，$x_1$,$x_2$,$x_3$，输出分别为：$f_1$,$f_2$,$f_3$。可以假设有噪声，也可以假设没有。
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/cq9r0vu0lw.png?imageView2/2/w/1620)

而高斯过程的关键点在于：我们认为f符合联合正态分布。
即：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/f5d7r7z9xt.png?imageView2/2/w/1620)

这个联合正态分布的均值为0，关键在于协方差矩阵K的求解。当X距离较近时，对应f的相关性也较高，要在K上反应出来。也就是说，K是X的函数，需要在一定程度上满足，$K(x_1,x_2)\geq K(x_1,x_3), d(x_1,x_2)\leq d(x_1,x_3)$。
IOW,  K的每个元素对应的是两个X的一个相似性度量:
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/6o759krwva.png?imageView2/2/w/1620)

如何保证这个相似性度量所产生的矩阵是一个合法的协方差矩阵——>Mercer矩阵，SVM里面的核函数，例如高斯核，就可以拿来用了。即：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/q2xf1rlw1r.png?imageView2/2/w/1620)

但这跟回归有什么关系：现在我们有一个新点了$x^{\ast}$, 想要求对应的$f^{\ast}$：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/7w808ogcm6.png?imageView2/2/w/16200)

根据假设，我们假设$f^{\ast}$和训练集里的$f_1$, $f_2$, $f_3$同属于一个（4维的）联合正态分布！
也就是：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/suwm4u6kma.png?imageView2/2/w/1620)

然后利用训练集计算黄色的K，然后利用测试点和每个训练集的X求出绿色的K*，然后整个联合分布就可以知道了。


我们既然已经知道$(f,f^{\ast})$的联合分布$P(f, f^{\ast})$的所有参数, 如何求$p(f^{\ast})$? 好消息是这个联合分布是正态的，我们直接用公式就能搞出来下面的结果（using the marginalization  property）：

接下来的事情就好办了，我们既然已经知道$f,f^{\ast}$的联合分布$P(f,f^{\ast})$的所有参数, 如何求$p(f^{\ast})$?好消息是这个联合分布是正态的，我们直接用公式就能搞出来下面的结果（using the marginalization  property）：

不难求出$f^{\ast}$隶属于一个1维的正态分布， 参数是:

![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/obj4h7sv1v.png?imageView2/2/w/1620)

所以不难看出，高斯过程回归其实是一种贝叶斯方法：因为此处求出的其实是整个后验概率的分布。
同时，高斯过程回归不仅可以得到$f^{\ast}$这个点的分布，对于未知的函数也可以进行推断。如果把一个函数作为一个变量，那么高斯过程回归也可以求出这个函数的分布。对于一个连续函数，通过在一次取样均匀的采样，然后求出测试点和训练集所对应的的$y$的联合分布，然后在这个高维联合分布里采样，就可得到函数近似的样本。

高斯过程是在函数上的正态分布（Gaussian distribution over functions)。具体而言就是
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/5fmvausfmw.png?imageView2/2/w/1620)

我们观察到一个训练集D
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/nsogbd2v9d.png?imageView2/2/w/1620)

给定一个测试集 X* （ X* 是一个 N* x D 的矩阵， D是每一个点的维度）我们希望得到 一个 N* 维的预测向量 f*. 高斯过程回归的模型假设是
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/pxgzec332e.png?imageView2/2/w/1620)

然后根据贝叶斯回归的方法，我们可以求出来f*的后验概率：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/nxx0ophphx.png?imageView2/2/w/1620)

全文参考：https://cloud.tencent.com/developer/article/1353538
  
  完。
