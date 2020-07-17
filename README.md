# AdversialNLP

### FGM

NLP的对抗训练，这里实现的是对embedding的attack，没有生成新数据；方法一般有FGM和PGD两种，我这里实现的是FGM，PGD也很好改，
介绍见https://zhuanlan.zhihu.com/p/91269728，基于tensorflow estimator BERT实现

### 实现思路

汗颜，其实我也不敢保证实现的没问题，因为我对tensorflow特别是estimator也不熟悉，这里我是魔改了model_fn的train part，用dependency control控制执行的先后顺序：

1、正常计算梯度->2、用1的梯度去攻击embedding层，参数+梯度->3、计算attack后的梯度->4、恢复embedding层参数，参数-梯度->5、将1和2的梯度进行累计->6、更新参数，loop结束

### 效果

FGM指标提高了1%-2%，因为数据保密就不说了，后面有机会各个数据集做一个对比。

embedding方面，Bert有word embeddings，token embeddings和position embedding，目前尝试了攻击word embeddings和全部都攻击，在我的语义匹配
任务上，攻击word embedding要比全攻击好不少。这个是根据任务尝试的，毕竟语义匹配任务更关注word embeddings，而不是position embeddings
如果是命名实体识别的话，说不定攻击position embedding会有效，因为实体识别跟位置信息强相关。
