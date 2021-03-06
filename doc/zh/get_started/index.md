# 开始使用 XGBoost

这里是一个快速入门的教程, 它展示了让你快速在示例数据集上进行二元分类任务时的 xgboost 的代码片段.

## Links to Helpful Other Resources
- 请参阅 [安装指南](../build.md) 以了解如何去安装 xgboost.
- 请参阅 [入门指引](../how_to/index.md) 以了解有关使用 xgboost 的各种技巧.
- 请参阅 [学习教程](../tutorials/index.md) 以了解有关特定任务的教程.
- 请参阅 [通过例子来学习使用 XGBoost](../../demo) 以了解更多代码示例.

## Python

```python
import xgboost as xgb
# 读取数据
dtrain = xgb.DMatrix('demo/data/agaricus.txt.train')
dtest = xgb.DMatrix('demo/data/agaricus.txt.test')
# 通过 map 指定参数
param = {'max_depth':2, 'eta':1, 'silent':1, 'objective':'binary:logistic' }
num_round = 2
bst = xgb.train(param, dtrain, num_round)
# 预测
preds = bst.predict(dtest)
```

## R

```r
# 加载数据
data(agaricus.train, package='xgboost')
data(agaricus.test, package='xgboost')
train <- agaricus.train
test <- agaricus.test
# 拟合模型
bst <- xgboost(data = train$data, label = train$label, max.depth = 2, eta = 1, nround = 2,
               nthread = 2, objective = "binary:logistic")
# 预测
pred <- predict(bst, test$data)

```

## Julia

```julia
using XGBoost
# 读取数据
train_X, train_Y = readlibsvm("demo/data/agaricus.txt.train", (6513, 126))
test_X, test_Y = readlibsvm("demo/data/agaricus.txt.test", (1611, 126))
# 拟合模型
num_round = 2
bst = xgboost(train_X, num_round, label=train_Y, eta=1, max_depth=2)
# 预测
pred = predict(bst, test_X)
```

## Scala

```scala
import ml.dmlc.xgboost4j.scala.DMatrix
import ml.dmlc.xgboost4j.scala.XGBoost

object XGBoostScalaExample {
  def main(args: Array[String]) {
    // 读取 xgboost/demo/data 目录中可用的训练数据
    val trainData =
      new DMatrix("/path/to/agaricus.txt.train")
    // 定义参数
    val paramMap = List(
      "eta" -> 0.1,
      "max_depth" -> 2,
      "objective" -> "binary:logistic").toMap
    // 迭代次数
    val round = 2
    // train the model
    val model = XGBoost.train(trainData, paramMap, round)
    // 预测
    val predTrain = model.predict(trainData)
    // 保存模型至文件
    model.saveModel("/local/path/to/model")
  }
}
```
