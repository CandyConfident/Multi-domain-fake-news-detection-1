#代码说明文件
1.第一步 code/lgb_cat_blend_lb9546.py  提取tfidf文本特征+dense net121提取的图像特征+用户特征 分别给lgb和catboost训练 然后融合 得到对的test集的预测结果，取概率大于0.9的结果和概率小于0.1的结果 生成伪标签数据pesudo_data.csv 用来做数据增强。

2. 第二步 code/bert_final.py 使用第一步生成通过对test的预测构造的伪标签数据+原来的训练数据作为新的训练数据 通过交叉验证训练5个bert模型保存到 model目录下，这个作为最终进行预测的模型。


#运行说明
1.sh req.sh #用来安装复现的Python环境包
2.sh train.sh #训练模型 生成模型文件保存在model目录下
2.sh test.sh #预测 通过调用生成的模型对test集预测 结果保存在submit目录下面


#model下预训练模型文件说明

1.model/tf_bert_model 是chinese_wwwm_ex的bert预训练bert模型的权重，再使用train和test集的text字段数据进行finetune得到的bert预训练模型权重。
2.model/DenseNet-BC-121-32-no-top.h5  来自keras官方给出的 Densenet121的预训练模型权重



