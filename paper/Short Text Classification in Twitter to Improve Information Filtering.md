# Short Text Classification in Twitter to Improve Information Filtering

***
2010年twitter的一篇短文本分类研究。600+引用。据说效果特别好，非常适合工业应用。简单翻译一下。
***
## 1、简介
Twitter是一个社交网络，它允许用户发表任意主题的微博。
**用户**会和他的**跟随者**产生联系。用户所发的twitter被认为是一个微博，因为Twitter的字数被限制在140个以内。这就使用户要在很短的字符数内表达他们所要表达的信息，用户也可以发布相关的链接来补充详细的信息。为了使用户不被大量原始数据文本所淹没，我们的任务就是将来的Twitter进行分类。

现存的短文本分类方法的研究主要是使用信息源比如维基百科或词网（WordNet）的元信息来整合消息[2,3]。Sankaranarayanan et al [6]介绍了TweetStand把Twitter分类为新闻和非新闻。通过利用大规模数据集扩充元信息或短文本的方式,自动文本分类和隐主题抽取[5]的方法同样表现很好。

我们提出了一种简单的分类方法，并且提出一组关注用户意图的特征集如每天的闲聊、对话、分享的信息/urls和新闻报道。相比于TweetStand，我们的方法更加通用。它能够根据作者的信息和作者发的Twitter的特征，把新来的Twitter分类为News (N), Events (E), Opinions (O), Deals (D), and Private Messages (PM)。经试验，结果显示我们的分类准确率在不利用元信息的情况下依然很高，同时比传统的词袋模型效果要好。

实验显示，作者身份在分类过程中起到重要的作用。作者通常附着于某些特定的Twitter模式，比如同一个作者的大量Twitter倾向于使用几种有限的模式。
## 2、特征选择
选择特征对于建立一个健壮的模型很重要。我们提出了一个8个特征的特征集，其中1个名词性的特征（作者），7个二分特征（是否包含单词的简写或哩语、是否有时间-时间的短语、是否有观点性的词语、是否有强调式的短语、是否有金钱或百分比的符号、有没有@某人在Twitter的开头、有没有@某人在Twitter中）。在分类阶段，模型就这些特征进行训练。现在我们讨论一下为什么这些特征可能代表某些类别。

把Twitter分为多个类别需要信息源的知识。因此我们选择了作者信息作为我们的基本特征。企业的Twitter和个人的Twitter的动机不同。前者倾向于使用很干净的形式来发表一些新闻；而后者经常使用一些短语、表情、哩语来表达个人。所以这些特征可以用来区分企业Twitter和个人Twitter。

如果我们定义一个事件是“某事在某个时间某个地点发生”的话，那么文本中是否存在参与者、地点、时间信息就能决定这个文本是否在描述一件事。因此，我们抽取我们收集到的Twitter中包含的时间信息和时间-事件的短语。参与者信息通过是否存在@某人来判断。

观点信息的存在与否，我们是通过查一个包含3000词的词表来判断的。

我们也抽取了强调词，比如大写词。另一种方法是看词语是否有重复的字母，比如（veeery）.

关键词deal和一些特殊的词比如金融符号或百分比符号都是很好的Deals类的特征。

Twitter允许用户通过在开始的位置@某人的方式给某人发私信（PM类）。
## 3、实验结果
### 3.1实验步骤
我们选择随机用户下载他们近期的Twitter，去掉了非英文的、单词数太少的（少于3个）、除了问候词外单词数少的、只有URL的、除了URL单词数太少的。最后得到了来自684个用户的5407条Twitter。这些Twitter被手动分类为合适的类别（比如：2107 N, 625 O, 1100 D, 1057 E, and 518 PM）。去掉停用词后，有6747个词。实验使用的是朴素贝叶斯算法，用5折交叉验证。
### 3.2性能评估
![image.png](https://upload-images.jianshu.io/upload_images/3007300-d659f1b8de957145.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/3007300-50fe51230be37364.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


表1和表2，分别是BOW、BOW, BOW-A, and 8F refer to Bag-Of-Words, BOW without the author feature, and our approach。
在数据集中发现，作者的特征非常有区分性。BOW-A（使用作者信息）比BOW要好18.3%，甚至比7F+BOW都要好3.7%。

表2显示，8F比任意其他方法都好。甚至8F的时间都比其他要提高一个量级。bow37.2秒，8F0.8秒。
## 4、总结
特征工程很重要啊！
