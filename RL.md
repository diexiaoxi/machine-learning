## Model based

学习的全过程：
- 第一步：从与真实世界互动的经历(Experience)中建立模型。
- 第二步：在模型中进行学习(可以使用MDP，TD等等所有之前使用的方法) 更新价值函数和策略。
- 第三步：用学到的价值函数和策略与真实世界进行互动并获得更多的经历。

[![](https://upload-images.jianshu.io/upload_images/10816620-586051ee2b3748a9.png?imageMogr2/auto-orient/strip|imageView2/2/w/261/format/webp)]

模型$M$实际上就是对环境，MDP<S, A, P, R>的参数化$\eta$近似，假设状态$S$和行为空间$A$是已知的。实际上就是对转移函数$P$和奖励$R$的参数化近似。

$M = <\mathcal{P}_{\eta},\mathcal{R}_{\eta}>$
其中 $\mathcal{P}_{\eta} = P(S_{n+1}|S_{n},A_{n})$,$\mathcal{R}_{\eta} = R(S_{n+1}|S_{n},A_{n})$


模型的建立可以通过监督学习的方式，其中从s, a 学习 r 的过程是一个回归问题(regression problem)；从s, a 学习 s' 的过程是一个密度估计问题(density estimation problem)。可以是查表式(Table lookup Model)、线性期望模型(Linear Expectation Model)、线性高斯模型(Linear Gaussian Model)、高斯决策模型(Gaussian Process Model)、和深信度神经网络模型(Deep Belief Network Model)等
训练方法：选择一个损失函数，比如均方差，KL 散度等，优化参数η来最小化经验损失(empirical loss)。

所有监督学习相关的算法都可以用来解决上述两个问题。

## Dyna算法

无模型的强化学习和基于模型的强化学习可以整合在一起吗？答案是肯定的，这就是Dyna算法

Dyna算法从实际经历中学习得到模型，然后联合使用实际经历和模拟经历一边学习，一边规划更新价值和（或）策略函数：


[![](https://upload-images.jianshu.io/upload_images/10816620-46c203905ded26ce.png?imageMogr2/auto-orient/strip|imageView2/2/w/469/format/webp)]


