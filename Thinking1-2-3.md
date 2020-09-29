### XGBoost与GBDT的区别是什么？
GBDT = Gradient Boosting Decision Tree ， 也叫MART = Multiple Additvie Regression Tree
XGBoost = Extreme Gradient Boosting,
* 一般GBDT以CART作为基分类器，xgboost却可以支持线性分类器，xgboost相当于Logistical Regression（分类问题）或者Linear Regression（回归问题）
* xgboost，可以带L1和L2正则化项，防止过拟合
* GBDT一般只支持一阶导，xgboost支持一阶和二阶导，并使用二阶泰勒展开公式
* xgboost能支持column sub sample,也就是列抽样，能降低过拟合，也能减少计算。
* xgboost是gbdt的工程版本，更能泛化。

### 举一个你之前做过的预测例子（用的什么模型，解决什么问题，比如我用LR模型，对员工离职进行了预测，效果如何... 请分享到课程微信群中）
目前正在做海上反走私的船编队船舶识别模型。
* 这个项目基于目前每天大概有大小不同吨位的船舶5000多条，有近1年的防控圈内雷达、光电、AIS、北斗、遥感影像等船舶运行轨迹数据，
* 通过研究历史编队船舶的航路习惯与海上通信数据，总结编队船舶的行为特征，运用LR挖掘算法，
* 由于特征众多，因此分别采用Pearson、Spearman秩相关系数、kendall等级相关系数去测算不同变量间的相关性系数,
* 最后预测出海上航行船舶可能是编队协作的概率，目前的Accuracy不是很高，正在做一个特殊的L2正则化项，希望为今后制定编队船舶个性化的通信设备部署方案，增强编队船舶的互通协作能力。

### 请你思考，在你的工作中，需要构建哪些特征（比如用户画像，item特征...），这些特征都包括哪些维度（鼓励分享到微信群中，进行交流）
答：目前海上反走私的项目，有很多个特征。
* 船舶运行轨迹。（节数，AIS上报，北半定位的经纬度，remote sensor等）
* 船舶历史事故. (碰撞的位置，材料，时间，金额等)
* 船舶违法信息。（禁行的区域，违法的种类等）
* 船舶基础数据（等级、类型、材质、功率等）
* 海图信息
* 船舶异常停航和接驳
* 船舶昼伏夜出

### Action1分享经验

* 最好是使用原生的xgboost
* 在做accuray_score之前，需要对预测结果进行处理成0,1，否则accuracy_score会报错
* early_stopping_rounds并不是越大越好。当设置为40时，比30的accruacy_score要低。
* 调整subsample为0.8会让accurayc_socre提高。

目前，我的得分是:0.9823232323232324
0.9823232323232324