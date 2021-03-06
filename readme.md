# RNN



# 一、语义分割

* word embedding的理解：

word embedding的意思是：给出一个文档，文档就是一个单词序列比如 “A B A C B F G”, 希望对文档中每个不同的单词都得到一个对应的向量(往往是低维向量)表示。比如，对于这样的“A B A C B F G”的一个序列，也许我们最后能得到：A对应的向量为[0.1 0.6 -0.5]，B对应的向量为[-0.2 0.9 0.7]  （此处的数值只用于示意）之所以希望把每个单词变成一个向量，目的还是为了方便计算，比如“求单词A的同义词”，就可以通过“求与单词A在cos距离下最相似的向量”来做到。如果Vec（w1) - Vec (w2) = Vec（w3) - Vec (w4), 则w1,w2之间的关系类似于w3,w4之间的关系，dist[Vec（w1) - Vec (w2)]越小，表明w1和w2之间关系更密切或者意思更相近。

* word embading的内容

![Image text](https://github.com/jhyehuang/w11-huangzhijie-107158044/blob/master/tsne.png)


​      同类型的词：二三四五六八九十百千万

​      有相关性的词：“日朝夕夜” ,“长短平”，“烛灯”可以看出其向量比较接近  


# 二、RNN训练部分

  train.py中写了feed_dict的内容，用sess.run执行了模型参数。

  utils.py中实现了函数def get_train_data(vocabulary, batch_size, num_steps)，函数根据数据集内容vocabulary、字典dictionary、batch_size、num_steps生成data和target。

  model.py中实现了rnn_cell的结构和softmax的计算。

# 三、结果

训练日志

![Image text](https://github.com/jhyehuang/w11-huangzhijie-107158044/blob/master/train_log.png)


结果日志

![Image text](https://github.com/jhyehuang/w11-huangzhijie-107158044/blob/master/result_sample_log.png)

# 四、RNN理解

全连接神经网络和卷积神经网络他们都只能单独的取处理一个个的输入，前一个输入和后一个输入是完全没有关系的。但是，某些任务需要能够更好的处理序列的信息，即前面的输入和后面的输入是有关系的。比如，当我们在理解一句话意思时，孤立的理解这句话的每个词是不够的，我们需要处理这些词连接起来的整个序列；当我们处理视频的时候，我们也不能只单独的去分析每一帧，而要分析这些帧连接起来的整个序列，这样我们就用到了循环神经网络(Recurrent Neural Network)。

# 五、心得体会

有点像小时候，做的选词天空，现在由RNN来完成这个过程。

[code]   我昨天上学迟到了，老师批评了____。 [/code]

给定一个一句话前面的部分，预测接下来最有可能的一个词是什么。是计算机理解人类的一个进步
