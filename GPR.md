## 总结一下高斯过程回归(GPR)


假设训练集中的三个点，$x_1$,$x_2$,$x_3$，输出分别为：$f_1$,$f_2$,$f_3$。可以假设有噪声，也可以假设没有。
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/cq9r0vu0lw.png?imageView2/2/w/1620)

而高斯过程的关键点在于：我们认为f符合联合正态分布。
即：
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/f5d7r7z9xt.png?imageView2/2/w/1620)

这个联合正态分布的均值为0，关键在于协方差矩阵K的求解。当X距离较近时，对应f的相关性也较高，要在K上反应出来。也就是说，K是X的函数，需要在一定程度上满足，$K(x_1,x_2)\geq K(x_1,x_3), d(x_1,x_2)\leq d(x_1,x_3)$。
IOW,  K的每个元素对应的是两个X的一个相似性度量:
![Alt text](https://ask.qcloudimg.com/http-save/yehe-1215004/6o759krwva.png?imageView2/2/w/1620)


那么问题来了，这个相似性怎么算？如何保证这个相似性度量所产生的矩阵是一个合法的协方差矩阵？ 

好，现在不要往下看了，你自己想3分钟。你也能想出来的。 提示：合法的协方差矩阵就是 (symmetric) Positive Semi-definite Matrix （。。。。。。。。。。。。思考中） 好了时间到。

　　答案： Kernel functions !

　　矩阵A正定是指,对任意的X≠0恒有X^TAX＞0。
　　矩阵A半正定是指,对任意的X≠0恒有X^TAX≥0。

　　判定A是半正定矩阵的充要条件是：A的所有顺序主子式大于或等于零。

　　如果你了解SVM的话，就会接触过一个著名的Mercer Theorem，（当然如果你了解泛函分析的话也会接触过 ），这个M定理是在说：一个矩阵是Positive Semi-definite Matrix当且仅当该矩阵是一个Mercer Kernel .

　　所以我们在svm里用过的任何Kernel都能拿过来用！

　　举个栗子，在高斯过程回归里，一种非常常见的Kernel就是SVM里面著名的高斯核（但是为了让命名不是那么混淆，文献中一般把这个Kernel称作 squared exponential kernel.

　　具体而言就是

