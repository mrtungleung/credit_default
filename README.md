# credit_default

## 信用卡违约率分析：
针对台湾某银行信用卡的数据，构建一个分析信用卡违约率的分类器。采用Random Forest算法，信用卡违约率识别率在80%左右。

这个数据集是台湾某银行 2005 年 4 月到 9 月的信用卡数据，数据集一共包括 25 个字段，具体含义如下：

![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.12.24.png)

现在我们的目标是要针对这个数据集构建一个分析信用卡违约率的分类器。具体选择哪个分类器，以及分类器的参数如何优化，我们可以用 GridSearchCV 这个工具跑一遍。
先梳理下整个项目的流程：

![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.12.47.png)

1. 加载数据；
2. 准备阶段：探索数据，采用数据可视化方式可以让我们对数据有更直观的了解，比如我们想要了解信用卡违约率和不违约率的人数。因为数据集没有专门的测试集，我们还需要使用train_test_split 划分数据集。
3. 分类阶段：之所以把数据规范化放到这个阶段，是因为我们可以使用 Pipeline 管道机制，将数据规范化设置为第一步，分类为第二步。因为我们不知道采用哪个分类器效果好，所以我们需要多用几个分类器，比如 SVM、决策树、随机森林和 KNN。然后通过 GridSearchCV 工具，找到每个分类器的最优参数和最优分数，最终找到最适合这个项目的分类器和该分类器的参数。
基于上面的流程，具体代码如下：

![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.14.19.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.14.35.png)

运行结果：

![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.16.09.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.17.21.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.17.37.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.17.44.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-09-10%20%E4%B8%8A%E5%8D%8811.17.52.png)
![image](https://github.com/mrtungleung/credit_default/blob/master/images/3.png)

从结果中，我们能看到 SVM 分类器的准确率最高，测试准确率为 0.8172。
在决策树分类中，我设置了 3 种最大深度，当最大深度 =6 时结果最优，测试准确率为0.8113；
在随机森林分类中，我设置了 3 个决策树个数的取值，取值为 6 时结果最优，测试准确率为 0.7994；
在 KNN 分类中，我设置了 3 个 n 的取值，取值为 8 时结果最优，测试准确率为 0.8036。
