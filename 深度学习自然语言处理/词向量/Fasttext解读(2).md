
这个文章主要是谈一下Enriching Word Vectors with Subword Information 这个论文。

有了上一个文章的打底，（[上一个文章点击这里](https://mp.weixin.qq.com/s?__biz=MzIyNTY1MDUwNQ==&mid=2247483925&idx=1&sn=9b980a4fb55fd55f92684e403188f024&chksm=e87d3033df0ab925e1ebdc3c89637974645698f1680fd1ad25e23db05903e2061ef8242f16a1&token=509904673&lang=zh_CN#rd)）这个论文理解起来就比较简单，所以我写的也比较短。

 对于这个论文，我先给出它最核心的部分： 使用负采样的skip-gram的基础上，将每个中心词视为子词的集合，并学习子词的词向量。 

这句话涉及到的一个最关键的部分就是子词subword，也是这个论文的核心。

 举个例子，现在我们的中心词是"where"，设定子词大小为3，那么子词集合分为两个部分，注意是两个部分。

 第一部分形如这样：“<wh”，“whe”，“her”，“ere”，“re>”，第二部分就是特殊子词，也就是整词“<where>”。 

那么对应到模型是，原来我的输入是“where”的词向量，现在在Fasttext就是所有子词的词向量的和。

 注意哦，这里是所有子词，是包含特殊子词，也就是整词的。

对于背景词，直接使用整词就可以。

 简单来说，就是输出层使用子词（普通子词加上整词），输出层使用整词。

 如果遇到了OOV怎么办？使用普通子词的向量和来表示就可以。

 其实这里的子词，在名字上和上一个文章的ngram很类似，不过，这里使用的是就char的n-gram，缓解的问题并不是语序，而是利用了词序形态的规律。

对应到中文，其实就是偏旁部首。 我记得阿里好像有发一个关于fasttext的中文版本，训练的就是偏旁部首。大家有兴趣可以去看一看。

写完了，我对两个文章做个小总结，顺便对文章开头的问题做个回答: fasttext 训练词向量的时候一般是使用Skip-gram模型的变种。在用作文本分类的时候，一般是使用CBOW的变种。

在这里，我想要强调一下，上一段我说的是一般情况，是为了方便大家了解，并不代表说CBOW架构不能训练词向量，skip-gram不能用作文本分类，需要注意这一点哦。

