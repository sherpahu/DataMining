# 整理

# 问题一 缺失数据

有很多人问到了缺失值处理的问题。统一汇总提问：

为什么需要处理缺失值？

缺失率大于多少时应当抛弃该特征？

缺失值填充有哪些方法？

采用均值填充的影响或者优缺点？

需要依据什么样的准则去选择合适的方法？



![img](https://uploader.shimo.im/f/1AU60J9fNj8sMmx0.png!thumbnail)



1 为什么需要处理缺失值？

就如同一件喜欢的衣服上有洞的情况一样，洞小、洞少情况下舍不得扔，打打补丁不影响美观的情况下还可以继续穿。但若洞大洞多了，没法穿或穿出去被围观，就只能忍痛仍了缺失值的缺失率和重要性，以及不同缺失值的处理方式在一定程度上影响了特征提取、建模和模型训练缺失值太多，可以尝试着直接删除，如果不删除，处理不好，可能会引来噪声缺失值较少，少于某一缺失率时，直接删除又会带来信息的损失，此时可以采取适当的填充方式



2 缺失率大于多少时应当抛弃该特征？

一般为70%,但是还要分析该特征与训练目标的重要程度



3 缺失值填充有哪些方法？(1). 插值填充

​    \- 特殊值，均值、中位数、众数等(2). 插补法

​    \- 随机插补法----从总体中随机抽取某个样本代替缺失样本

​    \- 多重插补法----通过变量之间的关系对缺失数据进行预测，利用蒙特卡洛方法生成多个完整的数据集，在对这些数据集进行分析，最后对分析结果进行汇总处理

​    \- 热平台插补----指在非缺失数据集中找到一个与缺失值所在样本相似的样本（匹配样本），利用其中的观测值对缺失值进行插补

​    \- 拉格朗日差值法和牛顿插值法

​    

4 采用均值填充的影响或者优缺点？   

缺点：大大降低数据的方差，即随机性



5 需要依据什么样的准则去选择合适的方法？

(1) 删除

- 如果行和列的缺失达到一定的比例，建议放弃整行或整列数据(2) 插补

- 列的维度上，如果是连续性，就使用平均值插补，如果是离散性，就使用众数来插补

- 行的维度上，引入预测模型，可考虑辅助回归，通过变量间的关系来预测缺失数据

(3) 不处理

​    当缺失值对模型的影响不大时，直接在包含空值的数据上进行数据挖掘

1. 丢弃  

2. 补全 统计法：对于数值型的数据，使用均值、加权均值、中位数等方法补足；对于分类型数据，使用类别众数最多的值补足。

3. 模型法：更多时候我们会基于已有的其他字段，将缺失字段作为目标变量进行预测，从而得到最为可能的补全值。如果带有缺失值的列是数值变量，采用回归模型补全；如果是分类变量，则采用分类模型补全。·

4. 专家补全：对于少量且具有重要意义的数据记录，专家补足也是非常重要的一种途径。

5. 真值转换。该思路的根本观点是，我们承认缺失值的存在，并且把数据缺失也作为数据分布规律的一部分，这将变量的实际值和缺失值都作为输入维度参与后续数据处理和模型计算。但是变量的实际值可以作为变量值参与模型计算，而缺失值通常无法参与运算，因此需要对缺失值进行真值转换。

6. 很多模型对于缺失值有容忍度或灵活的处理方法，因此在预处理阶段可以不做处理。常见的能够自动处理缺失值的模型包括：KNN、决策树和随机森林、神经网络和朴素贝叶斯、DBSCAN



# 问题二 数据探索

对于字段较少的情况下经常使用绘图来更直观的观察数据的分布，进而对数据进行针对性的处理；但是再字段量较多的情况下一个一个字段去绘图会比较费时间，那应该用怎么的顺序逻辑对字段进行处理？



对于第二个问题，这个情况在银行业普遍存在，当然，其他领域估计也会有。以我个人经历，在实际生产中会有一张表超过300个字段的情况，哪些字段该要哪些不该要确实比较麻烦。我采取的方式是首先去判断哪些字段值重复率较高，这个通过sql语句group by可以直接看出来。其次把数据通过spss对每一个特征进行分析，是绘图还是简单的分析，软件里面都有提供，基本上通过上面两步保证百分之七八十吧，如果仅仅是是在数据探索阶段的话，基本上就完成了

# 问题三 时间序列

时间序列应该怎么处理？除了提取天数还能做什么处理？

依情况处理，主要看单独时间字段或时间字段与某些字段的组合属性对目标分析的作用程度，再采取相应方式来进行特征提取比如：可以将时间字段与其他字段属性进行组合，分析每天、每周、每月或特点星期几等情况下特征数据频率信息，总的来说还是得看分析得目标

通常看到的情况是，除了考虑时间序列这个单独的特征外，往往是将时间序列和具有时间属性的特征联合起来分析，查看组合特征的对所需要分析的内容的影响

时间特征处理：Python标准库包含用于日期（date）和时间（time）数据的数据类型，而且还有日历方面的功能。参考资料：<https://www.jianshu.com/p/29ece4592178>  《利用Python进行数据分析·第2版》第11章 时间序列

# 问题四 异常值和离群值

怎样判断离群值以及是否需要删除离群值或怎样替代离群值？（比如一些手动录入过程中出错产生的离群值等）

离群点可以用分位数搞定我觉得

看跟平均值的偏差超过几倍标准差

LOF算法

describe的时候加一个 箱型图

<https://www.jianshu.com/p/0c967a1526ef>  可以看下这篇博客

大多数的参数统计数值，如均值、标准差、相关系数 等，以及基于这些参数的统计分析，均对离群值高度敏感。因此，离群值的存在会对数据分析造成极大影响

#  

# 问题五 分类数据的编码

这里城市的分类显然不适合用独热码编码了，那么如果在其它时候使用sklearn.preprocessing中的LabelBinarizer后重新编码的文本特征又怎样应用到预测中？





好像有两种编码，一种是one-hot，那就是彼此之间没关系。一种是dummy，那就是有顺序性的特征

试想编码出来只是数字，建模的时候本质上计算的是   类别间的距离。

所以我们就需要根据实际情况去判断，我们的类别间到底存不存在距离关系。

比如成绩的 优良差。他们是有距离关系的，差和优的"距离"确实比 良和优的"距离”要远的

再比如，人种，人种之间是不存在距离区别的，黑人和白人的"距离"和白人和黄种人的"距离"是一样的



# 问题六 类别不平衡问题

<https://imbalanced-learn.readthedocs.io/en/stable/api.html>

![img](https://uploader.shimo.im/f/EJTLGalflnQau2YD.png!thumbnail)

![img](https://uploader.shimo.im/f/eDmWxM0RgQ8vkmHM.png!thumbnail)

怕大家对数据不平衡没有直观感受，举两个实际场景例子：

一，信用卡欺诈 可能几百几千个客户里面才会有一个欺诈情况出现

二，网页广告点击率，这个比例更夸张

三, 医生病情误判情况





机器学习中如何处理不平衡数据？ <https://www.jiqizhixin.com/articles/021704>

# ![img](https://uploader.shimo.im/f/Wk0HJKweAgwJZWKm.png!thumbnail)

总结下，处理数据不平衡问题

大家的回答主要是两方面

1. 改变数据量大小，使类别间变得平衡

2. 不改变数据量，设置成本矩阵或代价函数来限定~





#  

#  

# 附录 我收集整理的一些资料

## 缺失值处理思维导图

机器学习缺失值处理方法汇总 <https://blog.csdn.net/w352986331qq/article/details/78639233>





## ![img](https://uploader.shimo.im/f/TwS5Ej0M8gQYMXsz.png!thumbnail)



## 数据编码

处理高基数单类别变量的方案

<https://mp.weixin.qq.com/s/U93vvFwZ8vSJuswk24yc6w>



## 数据不平衡问题

what?

通常出现在类别问题中，类别间数据量差异过大

例如：10W正例，100反例



why?

**为什么会出现**

  

1. 收集的数据量不多，不全面

  

1. 数据集本身特点，如信用卡欺诈、用户投诉、机器故障数据，可能1K个顾客里面，只有1个会欺诈。

 



**为什么需要处理**

​        类别间的不平衡，会很容易导致模型预测偏移。比如信用卡欺诈，直接跑决策树，可能预测准确率会高达99.99%不会欺诈。这样的结果并没有意义。

​        所以像这种类别不平衡的，我们需要采取一些策略去调整数据。



how?

**目标**：

  

1. 改变数据量，使类别间数据量尽量相等。 正例数据量 = 反例数据量

 

  

1. 数据量不变，通过采用不同模型或者评估方法来消除不平衡的影响

 



**策略**：

  

1. **扩大数据集**。以期得到更多的分布信息；同时扩大数据量后也方便后面的重新采样。

2. **尝试新角度理解问题**。我们可以把那些小类的样本作为异常点(outliers)，因此该问题便转化为异常点检测(anomaly detection)与变化趋势检测问题(change detection)。

   异常点检测即是对那些罕见事件进行识别。如通过机器的部件的振动识别机器故障，又如通过系统调用序列识别恶意程序。这些事件相对于正常情况是很少见的。

   变化趋势检测类似于异常点检测，不同在于其通过检测不寻常的变化趋势来识别。如通过观察用户模式或银行交易来检测用户行为的不寻常改变。

   

   

   **Sampling methods(采样方法)** 

​           增加偏少的类别 - **OverSampling**过采样

​            ① 简单随机重复。

​            ② SMOTE。在相同边界内，人工造数据。

​           减少偏多的类别 - **UnderSampling**欠采样

​            ① 简单随机抽样。

​            ② 带边界清理。尽量保留分布信息。

  

1. **引入不同的评价指标**

 

由于正确率太过片面。可以通过G-Mean指标，特别是ROC曲线（接受者    工作特征曲线-Receiver Operating Characteristic Curve，简称ROC曲线）和AUC曲线下面积。

  

1. **Cost-sensitive methods(代价敏感学习方法)**

代价敏感学习方法的核心要素是代价矩阵，我们注意到在实际的应用中不同类型的误分类情况导致的代价是不一样的，例如在医疗中，“将病人误疹为健康人”和“将健康人误疹为病人”的代价不同；在信用卡盗用检测中，将盗用误认为正常使用”与“将正常使用识破认为盗用”的代价也不相同。

​         ![img](https://uploader.shimo.im/f/nOuK3nQyizA44c8g.png!thumbnail)

 还是以医疗为例， 病人诊断为病人可以带来100的收益，健康的诊断为健康是10收益；但是错误的将病人诊断为健康的或者将健康的诊断为病人，有时可能会出现致命的情况，所以将这两种收益设置为-100000。通过设置代价矩阵就可以一定程度矫正模型的偏向。

1. **采用集成学习思想**。

把多数类进行划分，然后和少数类组合成多个小的训练集，然后生成学习器，最后再集成。

​       

Sources：

1. 英文版论坛-八大策略处理数据不平衡问题    <https://machinelearningmastery.com/tactics-to-combat-imbalanced-classes-in-your-machine-learning-dataset/>

2. 中文版论坛  八大策略处理数据不平衡问题  <https://blog.csdn.net/heyongluoyao8/article/details/49408131>

3. 大神论文 Learning from Imbalanced      Data    <http://www.ele.uri.edu/faculty/he/research/ImbalancedLearning/ImbalancedLearning_lecturenotes.pdf>
4. SMOTE论文<http://www.cs.cmu.edu/afs/cs.cmu.edu/project/jair/pub/volume16/chawla02a.pdf>

 

