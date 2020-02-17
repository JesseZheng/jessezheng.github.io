---
title: Machine Learning Notes
date: 2019-11-07 13:19:00
tags:
- Machine Learning
categories: AI
---
### Type of tasks
- **classification**: face recognization
- **regression**: prediction
- **clustering**: [一篇文章透彻解读聚类分析](https://zhuanlan.zhihu.com/p/37856153)

<!-- more -->

### Classifier
- **Scoring classifier**: outputs a vector of scores instead of a class label
- **Ranking classifier**: ???
- **Probability estimation classifier**: 

### Evaluation of classifier performance
- True Positive （真正, TP）被模型预测为正的正样本；
- True Negative（真负 , TN）被模型预测为负的负样本 ；
- False Positive （假正, FP）被模型预测为正的负样本；
- False Negative（假负 , FN）被模型预测为负的正样本；
- True Positive Rate（真正率 , TPR）或灵敏度（sensitivity, recall） 
TPR = TP /（TP + FN） 
正样本预测结果数 / 正样本实际数
- True Negative Rate（真负率 , TNR）或特指度（specificity） 
TNR = TN /（TN + FP） 
负样本预测结果数 / 负样本实际数 
- False Positive Rate （假正率, FPR） 
FPR = FP /（FP + TN） 
被预测为正的负样本结果数 /负样本实际数 
- False Negative Rate（假负率 , FNR） 
FNR = FN /（TP + FN） 
被预测为负的正样本结果数 / 正样本实际数

### F-measure and precision
- precision(精确度) = TP/(TP+FP)
- F-measure = 2\*precision\*sensitivity/(precision+senstivity)

### Linear regression

