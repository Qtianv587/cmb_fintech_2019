# cmb_fintech_2019
招银竞赛题目三：短文本分析排名第一方案
A榜 66.9分
B榜 82.3分

A榜B榜的阈值相差较大，a榜的高分参数在b榜数据上只有70分左右。

主要思路：提取文本特征 + 聚类
1. 比赛有第三方库和时间的限制，不考虑词向量，选择基础的tfidf特征。
2. 由于词表与段落数较少，对idf部分进行改进：在去停用词的基础上，能够同时出现在两个段落中的词更能够体现两个段落的相似性，因此放弃idf而是使用了df值的平方根作为权重。
3. 对于出现在段落靠前位置的词进行了权重增强：对于每一段位于前15%的单词，乘上一个固定的权重5（参数通过调参确定，这个方案简单粗暴但是比较有效）。
4. 对于类似'cmb'的缩写进行了补全
5. 实现了使用余弦相似度的层次聚类，尽可能的规避较多的参数（kmeans需要提前设置k，dbscan有2个超参）
6. 尝试使用轮廓系数与ch分数来动态调整阈值，但是效果并不好，没有应用。
7. 可以考虑使用投票的方法来动态调整参数。

最终参数设置 a榜 0.17左右， b榜0.04左右
