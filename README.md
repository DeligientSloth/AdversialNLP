# AdversialNLP

NLP的对抗训练，这里实现的是对embedding的attack，没有生成新数据；方法一般有FGM和PGD两种，我这里实现的是FGM，PGD也很好改，
介绍见https://zhuanlan.zhihu.com/p/91269728，基于tensorflow estimator BERT实现

# 效果

FGM指标提高了1%-2%，因为数据保密就不说了，后面有机会各个数据集做一个对比
