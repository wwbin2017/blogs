---
title: 机器学习 主题模型 LDA
date: 2018-05-01 15:12:14
tags: Machine Learning
---

#### LDA主题模型原理

LDA的数学推导还是很复杂的，但是最后的结果却是非常美观，解释比较容易。这里简单介绍一下LDA的一个过程，有时间会详细推导一遍（当然 ‘LDA数学八卦’ 就解释的很详细了）。
LDA涉及到的一些数学知识点有：
* 先验概率，后验概率（贝叶斯学派），似然函数， 共轭分布
* 二项分布，多项分布;Beta分布，Dirichlet分布 （涉及到伪计数）
* gibbs采样，变分推导
* 常见的库有sklearn ，gensim， pLDA， LightLDA（python推荐gensim非常好用，速度也特别给力）

![LDA网络结构](机器学习-主题模型-LDA/LDA)  

* 假设共有m篇文章,一共涉及了K个主题（人为设置）;
* 每篇文章(长度为Nm)都有各自的主题分布,主题分布是多项分布,该多项分布的参数服从Dirichlet分布,该Dirichlet分布的参数为α;
* 每个主题都有各自的词分布,词分布为多项分布,该多项分布的参数服从Dirichlet分布,该Dirichlet分布的参数为β;
* 因此，整个文档的参数过程为：对于某篇文章中的第n个词,首先从该文章的主题分布中采样一个主题,然后在这个主题对应的词分布中采样一个词。不断重复这个随机生成过程,直到m篇文章全部完成上述过程。

LDA 总结
* 由于在词和文档之间加入的主题的概念,可以较好的解决一词多义和多词一义的问题。
* LDA可能对短文本的效果不是很好，可以把短文本连接成长文本
* LDA可以和其他算法相结合。首先使用LDA将长度为N的文档降维到K维(主题的数目),同时给出每个主题的概率(主题分布)，有点类似于降维。然后使用其他算法分析文本。
************
```python
def lda_gibbs(doc_word, words_id, k, alpha, beta, iter_num):
    """
    LDA模型
    :param doc_word: [[word_id word_id] [word_id word_id]]
    :param words_id: {word:id}
    :param k:  主题数
    :param alpha: 文档主题参数服从dirichlet分布的参数
    :param beta:    主题词参数服从dirichlet分布的参数
    :param iter_num: 迭代次数
    :return: theta 文档主题分布, phi 主题词分布
    """
    doc_topic_count, topic_words_count, doc_word_count = init_param_lda(doc_word, words_id, k)
    for i in range(iter_num):
        gibbs_sampling(doc_topic_count, topic_words_count, doc_word, doc_word_count, k, alpha, beta)
    theta = calc_theta(doc_topic_count, alpha)
    phi = calc_phi(topic_words_count, beta)
    save_model(theta, phi)
    return theta, phi


def calc_theta(doc_topic_count, alpha):
    """
    计算文档主题分布
    :param doc_topic_count: np.array dim=[document, topic]
    :param alpha:
    :return: theta np.array dim=[document, topic]
    """
    dim = doc_topic_count.shape
    theta = np.zeros(dim)
    for i in range(dim[0]):
        sum_i = sum(doc_topic_count[i, :]) + dim[1]*alpha
        for j in range(dim[1]):
            theta[i, j] = (doc_topic_count[i, j] + alpha)*1.0/sum_i
    return theta


def calc_phi(topic_words_count, beta):
    """
    计算主题词分布
    :param topic_words_count: np.array [topic, word]
    :param beta:
    :return: phi np.array [topic, word]
    """
    dim = topic_words_count.shape
    phi = np.zeros(dim)
    for i in range(dim[0]):
        sum_i = sum(topic_words_count[i, :]) + dim[1] * beta
        for j in range(dim[1]):
            phi[i, j] = (topic_words_count[i, j] + beta) * 1.0 / sum_i
    return phi


def gibbs_sampling(doc_topic_count, topic_words_count, doc_word, doc_word_topic, k, alpha, beta):
    doc_len = len(doc_word_topic)
    for i in range(doc_len):
        for j in range(len(doc_word[i])):
            doc_topic_count[i, doc_word_topic[i][j]] -= 1
            topic_words_count[doc_word_topic[i][j], doc_word[i][j]] -= 1
            p = np.zeros(k)
            for t_n in range(k):
                p[t_n] = ((doc_topic_count[i, t_n] + alpha)*1.0/(sum(doc_topic_count[i])+k*alpha))\
                         *((topic_words_count[t_n, doc_word[i][j]] + beta)*1.0/(sum(topic_words_count[t_n, :]) + k*beta))
                if t_n > 0:
                    p[t_n] += p[t_n-1]
            gs = random.random()*p[k-1]
            new_topic = 0
            while new_topic < k:
                if p[new_topic] > gs:
                    break
                new_topic += 1
            doc_topic_count[i, new_topic] += 1
            topic_words_count[new_topic, doc_word[i][j]] += 1
            # 不要忘记更新这个， 否则会出现负数
            doc_word_topic[i][j] = new_topic

```
