---
layout: base
title: 使用rstanarm进行贝叶斯logistic regression
---

[Bayesian Logistic Regression with rstanarm](https://www.kaggle.com/avehtari/bayesian-logistic-regression-with-rstanarm)

CRAN vignette: A vignette is a long-form guide to your package. A vignette is like a book chapter or an academic pater: it can describe the problem that your package is designed to solve, and then show the reader how to solve it. A vignette should divide functions into useful categories, and demonstrate how to coordinate multiple functions to solve problems. ... For example, if you have implemented a complex statistical algorithm, you might want to describe all the details in a vignette so that users of your package can understand what's going on under the hood, and be confident that you've implemented the algorithm correctly.

# Introduction

介绍了怎样利用rstanarm package中的 stan_gml 函数来估计generalized linear models (GLMs) （广义线性模型）for 二项式（伯努利）响应变量。

Stan是一个开源的统计建模、计算平台。它开放了R, python接口（RStan, PyStan, ScalaStan）。RStanArm又是一个其上的Higer level interface.

线性回归和逻辑回归都是GLM的一种特殊形式。线性回归中我们假设 \theta 服从正态分布，逻辑回归中我们假设 \theta 服从不努力分布。有了广义线性模型，我们只需要把符合指数分布的一般模型的参数转换成它对应的广义线性模型参数，然后按照广义线性模型的求解步骤，即可轻松求解问题。

贝叶斯分析的4步
* 定义输出与所有未知变量的联合分布，一般形式为未知变量的边际先验分布，乘以输出相对于未知变量的条件分布。该联合分布，与未知变量相对于观察数据的后验分布成比例。
* 使用 markov chain monte carlo，按照后验分布掷骰子。
* 评估模型与数据的匹配程度，可能会调整模型
* 根据输出量的后验预测分布，基于预测因子的有特点的值，以便可视化对预测因子的操纵如何影响输出量。