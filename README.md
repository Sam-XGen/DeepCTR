# 机器学习模型库说明文档
## 依赖环境
 - python3
 - tensorflow
 - numpy
 - sklearn
## 设计说明
`base`基类仿照`keras`模型实现以下公有方法，包括
- save_model 保存模型
- load_mdel 加载模型
- train_on_batch 小批量训练
- fit 全量训练
- test_on_batch 小批量评估
- evaluate 模型评估
- predict_on_batch 小批量预测
- predict 全量预测

同时设计了若干抽象方法
- _get_data_loss
- _get_input_target
- _get_out_put_target
- _get_data_loss
- _get_optimizer
- _build_graph

要求子类在`__init__`方法的最后调用`self._build_graph()`构建计算图。
## DeepFM
参考论文
>DeepFM: A Factorization-Machine based Neural Network for CTR Prediction [link](https://arxiv.org/abs/1703.04247)
## DeepCrossNetwork
> Deep & Cross Network for Ad Click Predictions [link](https://arxiv.org/abs/1708.05123)

实现和论文的区别
- embedding_size  
论文里提出每个field根据cardinality的不同来设置。这里用的是所有field具有相同embedding_size的实现，所以feature的编码是global的。
- Batch normalization  
论文在Deep Network部分采用了BN
- gradient clip  
论文采用了梯度截断，范数设置为100
- 其他
论文采用512batch size，并提出使用早停来防止过拟合，L2和dropout正则效果一般。