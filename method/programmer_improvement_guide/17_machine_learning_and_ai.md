# 《程序员练级攻略》分析笔记

## 第17章 机器学习和人工智能

### Q1：这一章的内容属于哪一类别？

计算机/方法论。

### Q2：这一章的内容是什么？

### Q3：这一章的大纲是什么？

- 入门资料
- 相关课程
- 相关图书
- 相关文章
- 相关算法
- 相关资源

### Q4：作者想要解决什么问题？

### Q5：这一章的关键词是什么？

### Q6：这一章的关键句是什么？

#### 入门资料

- [Machine Learning is Fun!][1]（[中文翻译版][2]）
  - 这篇文章恐怕是全世界最简单的入门资料了。

- Data Science Simplified 
  - [Data Science Simplified Part 1: Principles and Process][3]
  - [Data Science Simplified Part 2: Key Concepts of Statistical Learning][4]
  - [Data Science Simplified Part 3: Hypothesis Testing][5]
  - [Data Science Simplified Part 4: Simple Linear Regression Models][6]
  - [Data Science Simplified Part 5: Multivariate Regression Models][7]
  - [Data Science Simplified Part 6: Model Selection Methods][8]
  - [Data Science Simplified Part 7: Log-Log Regression Models][9]
  - [Data Science Simplified Part 8: Qualitative Variables in Regression Models][10]
  - [Data Science Simplified Part 9: Interactions and Limitations of Regression Models][11]
  - [Data Science Simplified Part 10: An Introduction to Classification Models][12]
  - [Data Science Simplified Part 11: Logistic Regression][13]

#### 相关课程

- 数据分析教程
  - [UC Berkeley’s Data 8: The Foundations of Data Science][14] 和电子书 [Computational and Inferential Thinking][15]
    - 讲述数据科学方面非常关键的概念，会教你在数据中找到数据的关联、预测和相关的推断。
  - [Learn Data Science][16]
    - 这是 GitHub 上的一本电子书，主要是一些数据挖掘的算法，比如线性回归、逻辑回归、随机森林、K-Means 聚类的数据分析。
  - [donnemartin/data-science-ipython-notebooks][17]
    - 这个代码仓库中用 TensorFlow、scikit-learn、Pandas、NumPy、Spark 等把这些经典的例子实现了个遍。

- 机器学习入门课程
  - [Machine Learning (by Andrew Ng)][19]
  - [Deep Learning Specialization (by Andrew Ng)][20]
  - [Deep Learning by Google][21]
    - Google 的一个关于深度学习的在线免费课程，其支持中英文。
    - 这门课会教授你如何训练和优化基本神经网络、卷积神经网络和长短期记忆网络。你将通过项目和任务接触完整的机器学习系统 TensorFlow。
  - 卡内基梅隆大学汤姆·米切尔（Tom Mitchell）的机器学习 [英文原版视频与课件 PDF][22]。
  - 2013 年加利福尼亚理工学院亚瑟·阿布 - 穆斯塔法（Yaser Abu-Mostafa）的 [Learning from Data 课程视频及课件 PDF][23]，内容更适合进阶。
  - [Neural networks class - Université de Sherbrooke][24]
    - YouTube 上非常火的一个课程视频，由宾夕法尼亚大学的雨果·拉罗歇尔（Hugo Larochelle）出品的教学课程。

- 其他在线大学课程
  - 斯坦福大学的《[统计学学习][25]》、《[机器学习][26]》、《[卷积神经网络][27]》、《[深度学习之自然语言处理][28]》等。
  - 麻省理工大学的《[神经网络介绍][29]》、《[机器学习][30]》、《[预测][31]》等。

- 机器学习资源列表
  - [Awesome Machine Learning Courses][32]

#### 相关图书

- [《Pattern Recognition and Machine Learning][33]
  - 这本书是机器学习领域的圣经之作。这本书很经典，但并不适合入门来看。

- 两本经典电子书，其中讲了很多机器学习的知识，可以当做手册或字典。
  - [《Understanding Machine Learning: From Theory to Algorithms》][34]
  - [《The Elements of Statistical Learning - Second Edition》][35]

- [《Deep Learning: Adaptive Computation and Machine Learning series》][36]
  - 深度学习领域奠基性的经典教材
  - 官网：[“deeplearningbook.org”][37]
  - 中文翻译：[《Deep Learning 中文翻译》][38]

- [《Neural Networks and Deep Learning》][39]（[中文翻译版][40]）
  - 这是一本非常不错的神经网络的入门书。虽然有很多数学公式，但是有代码相助。

- [《Introduction to Machine Learning with Python][41]
  - 一本不错的入门书，也是本比较易读的英文书。
  - 此书以 Scikit-Learn 框架来讲述。

- [《Hands-On Machine Learning with Scikit-Learn and TensorFlow》][42]
  - 这是一门以 TensorFlow 为工具的入门书。

#### 相关文章

- [Machine Learning Recipes with Josh Gordon ][43]
  - YouTube 上的 Google Developers 的 9 集视频，每集不到 10 分钟，从 Hello World 讲到如何使用 TensorFlow，非常值得一看。

- [Practical Machine Learning Tutorial with Python Introduction][44]
  - 一系列的用 Python 带着你玩 Machine Learning 的教程。

- [Medium 上的 Machine Learning - 101][45]
  - 讲述了好些我们上面提到过的经典算法。

- [Medium 上的 Marchine Learning for Humans][46]

- [Dr. Jason Brownlee 的博客][47]
  - 其中好多的 “How-To”，会让你有很多的收获。

- [Rules of Machine Learning: Best Practices for ML Engineering][48]
  - 一些机器学习相关的最佳实践。

- [i am trask][49]
  - 一个很不错的博客。

- [Neural Networks][50]
  - YouTube 关于神经网络的介绍视频 。

- [麻省理工学院的电子书 Deep Learning][51]

- [Natural Language Processing with Python][52]

- [Machine Learning & Deep Learning Tutorials。][53]
  - Machine Learning 和 Deep Learning 的相关教程列表

- 一些和神经网络相关的文章
  - [The Unreasonable Effectiveness of Recurrent Neural Networks][54]
    - 这是一篇必读的文章 ，告诉你为什么要学 RNN，以及展示了最简单的 NLP 形式。
  - [Neural Networks, Manifolds, and Topology][55]
    - 这篇文章可以帮助你理解神经网络的一些概念。
  - [Understanding LSTM Networks][56]
    - 解释了什么是 LSTM 的内在工作原理。
  - [Attention and Augmented Recurrent Neural Networks][57]
    - 用了好多图来说明了 RNN 的 attention 机制。
  - [Recommending music on Spotify with deep learning][58]
    - 一个在 Spotify 的实习生分享的音乐聚类的文章。

#### 相关算法

- 对于监督式学习，有如下经典算法。
  - [决策树（Decision Tree][59]
    - 比如自动化放贷、风控。
  - [朴素贝叶斯分类器（Naive Bayesian classifier][60]
    - 可以用于判断垃圾邮件、对新闻的类别进行分类，比如科技、政治、运动、判断文本表达的感情是积极的还是消极的、人脸识别等。
  - [最小二乘法（Ordinary Least Squares Regression][61]
    - 是一种线性回归。
  - [逻辑回归（Logisitic Regression][62]
    - 一种强大的统计学方法，可以用一个或多个变量来表示一个二项式结果。
    - 可以用于信用评分，计算营销活动的成功率，预测某个产品的收入。
  - [支持向量机（Support Vector Machin][63]
    - SVM），可以用于基于图像的性别检测、图像分类等。
  - [集成方法（Ensemble methods][64]
    - 通过构建一组分类器，然后通过它们的预测结果进行加权投票来对新的数据点进行分类。
      原始的集成方法是贝叶斯平均，但最近的算法包括纠错输出编码、Bagging 和 Boosting。

- 对于无监督式的学习，有如下经典算法。
  - [聚类算法（Clustering Algorithms）][65]
    聚类算法有很多，目标是给数据分类。
    有 5 个比较著名的聚类算法你必需要知道：[K-Means][82]、[Mean-Shift][83]、[DBSCAN][84]、[EM/GMM][85]、和 [Agglomerative Hierarchical][86]。
  - [主成分分析（Principal Component Analysis，PCA）][66]
    - PCA 的一些应用包括压缩、简化数据便于学习、可视化等。
  - [奇异值分解（Singular Value Decomposition，SVD）][67]
    - 实际上，PCA 是 SVD 的一个简单应用。
    - 在计算机视觉中，第一个人脸识别算法使用 PCA 和 SVD 来将面部表示为"特征面"的线性组合，进行降维，然后通过简单的方法将面部匹配到身份。
    - 虽然现代方法更复杂，但很多方面仍然依赖于类似的技术。
  - [独立成分分析（Independent Component Analysis，ICA）][68]
    - ICA 是一种统计技术，主要用于揭示随机变量、测量值或信号集中的隐藏因素。

- [List of Machine Learning Algorithms][69]
  - Wikipedia 的机器学习算法列表。

- [A Tour of Machine Learning Algorithms][70]
  - 这篇文章带你概览了一些机器学习算法，其中还有一个"脑图"可以下载，并还有一些 How-To 的文章供你参考。

- [SciKit-Learn][71] 的一些参考文档
  - [1. Supervised learning][72]
  - [2.3. Clustering][73]
  - [2.5. Decomposing signals in components (matrix factorization problems)][74]
  - [3. Model selection and evaluation][75]
  - [4.3. Preprocessing data][76]

#### 相关资源

- [8 Fun Machine Learning Projects for Beginners][77]
  - 其中为初学者准备了 8 个很有趣的项目

- [《Awesome Public Datasets》][78]
  - 这里有一个列表给你足够多的公共数据。
  - 其中包括农业、生物、天气、计算机网络、地球科学、经济、教育、金融、能源、政府、健康、自然语言、体育等。

- GitHub 上的一些 Awesome 资源列表。
  - [Awesome Deep Learning][79]
  - [Awesome - Most Cited Deep Learning Papers][80]
  - [Awesome Deep learning papers and other resources][81]

### Q7：作者是怎么论述的？

### Q8：作者解决了什么问题？

### Q9：我有哪些疑问？

### Q10：这一章说得有道理吗？为什么？

### Q11: 这一章讨论的知识的本质是什么？

### Q12: 这一章讨论的知识的第一原则是什么？

### Q13：这一章讨论的知识的结构是怎样的？

### Q14：这一章讨论的知识为什么是这样的？为什么发展成这样？为什么需要它？

### Q15：有哪些相似的知识？它们之间的联系是什么？

### Q16：其他领域/学科有没有相关的知识？日常生活中有没有类似的现象？

### Q17: 这一章对我有哪些用处/帮助/启示？

### Q18: 我如何应用这一章的知识去解决问题？

  [1]: https://medium.com/@ageitgey/machine-learning-is-fun-80ea3ec3c471
  [2]: https://zhuanlan.zhihu.com/p/24339995
  [3]: https://becominghuman.ai/data-science-simplified-principles-and-process-b06304d63308
  [4]: https://towardsdatascience.com/data-science-simplified-key-concepts-of-statistical-learning-45648049709e
  [5]: https://towardsdatascience.com/data-science-simplified-hypothesis-testing-56e180ef2f71
  [6]: https://towardsdatascience.com/data-science-simplified-simple-linear-regression-models-3a97811a6a3d?gi=23acf9145aec
  [7]: https://towardsdatascience.com/data-science-simplified-part-5-multivariate-regression-models-7684b0489015
  [8]: https://towardsdatascience.com/data-science-simplified-part-6-model-selection-methods-2511cbdf7cb0
  [9]: https://towardsdatascience.com/data-science-simplified-part-7-log-log-regression-models-499ecd1495f0
  [10]: https://towardsdatascience.com/data-science-simplified-part-8-qualitative-variables-in-regression-models-d1817d56245c
  [11]: https://towardsdatascience.com/data-science-simplified-part-9-interactions-and-limitations-of-regression-models-4702dff03820
  [12]: https://towardsdatascience.com/data-science-simplified-part-10-an-introduction-to-classification-models-82490f6c171f
  [13]: https://towardsdatascience.com/data-science-simplified-part-11-logistic-regression-5ae8d994bf0e?gi=b55560d8cc14
  [14]: http://data8.org/
  [15]: https://inferentialthinking.com/chapters/intro.html
  [16]: https://github.com/nborwankar/LearnDataScience
  [17]: https://github.com/donnemartin/data-science-ipython-notebooks#scikit-learn
  [19]: https://open.163.com/newview/movie/courseintro?newurl=IEU2H8NIJ
  [20]: https://mooc.study.163.com/smartSpec/detail/1001319001.htm
  [21]: https://www.udacity.com/course/intro-to-tensorflow-for-deep-learning--ud187
  [22]: http://www.cs.cmu.edu/~tom/10701_sp11/lectures.shtml
  [23]: https://home.work.caltech.edu/lectures.html
  [24]: https://www.youtube.com/playlist?list=PL6Xpj9I5qXYEcOhn7TqghAJ6NAPrNmUBH
  [25]: https://online.stanford.edu/lagunita-learning-platform
  [26]: http://cs229.stanford.edu/
  [27]: http://cs231n.stanford.edu/
  [28]: http://cs224d.stanford.edu/
  [29]: https://ocw.mit.edu/courses/9-641j-introduction-to-neural-networks-spring-2005/
  [30]: https://ocw.mit.edu/courses/6-867-machine-learning-fall-2006/
  [31]: https://ocw.mit.edu/courses/15-097-prediction-machine-learning-and-statistics-spring-2012/
  [32]: https://github.com/RatulGhosh/awesome-machine-learning
  [33]: https://book.douban.com/subject/2061116/
  [34]: https://www.cs.huji.ac.il/~shais/UnderstandingMachineLearning/understanding-machine-learning-theory-algorithms.pdf
  [35]: https://web.stanford.edu/~hastie/Papers/ESLII.pdf
  [36]: https://book.douban.com/subject/27087503/
  [37]: https://www.deeplearningbook.org/
  [38]: https://github.com/exacity/deeplearningbook-chinese
  [39]: http://neuralnetworksanddeeplearning.com/
  [40]: https://tigerneil.gitbooks.io/neural-networks-and-deep-learning-zh/content/
  [41]: https://book.douban.com/subject/26279609/
  [42]: https://book.douban.com/subject/26840215/
  [43]: https://www.youtube.com/playlist?list=PLOU2XLYxmsIIuiBfYad6rFYQU_jL2ryal
  [44]: https://pythonprogramming.net/machine-learning-tutorial-python-introduction/
  [45]: https://medium.com/machine-learning-101
  [46]: https://medium.com/machine-learning-for-humans
  [47]: https://machinelearningmastery.com/blog/
  [48]: https://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf
  [49]: http://iamtrask.github.io/
  [50]: https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi
  [51]: https://www.deeplearningbook.org/
  [52]: https://www.nltk.org/book/
  [53]: https://github.com/ujjwalkarn/Machine-Learning-Tutorials
  [54]: http://karpathy.github.io/2015/05/21/rnn-effectiveness/
  [55]: http://colah.github.io/posts/2014-03-NN-Manifolds-Topology/
  [56]: http://colah.github.io/posts/2015-08-Understanding-LSTMs/
  [57]: https://distill.pub/2016/augmented-rnns/
  [58]: https://benanne.github.io/2014/08/05/spotify-cnns.html
  [59]: https://en.wikipedia.org/wiki/Decision_tree
  [60]: https://en.wikipedia.org/wiki/Naive_Bayes_classifier
  [61]: https://en.wikipedia.org/wiki/Ordinary_least_squares
  [62]: https://en.wikipedia.org/wiki/Logistic_regression
  [63]: https://en.wikipedia.org/wiki/Support-vector_machine
  [64]: https://en.wikipedia.org/wiki/Ensemble_learning
  [65]: https://en.wikipedia.org/wiki/Cluster_analysis
  [66]: https://en.wikipedia.org/wiki/Principal_component_analysis
  [67]: https://en.wikipedia.org/wiki/Singular_value_decomposition
  [68]: https://en.wikipedia.org/wiki/Independent_component_analysis
  [69]: https://en.wikipedia.org/wiki/Outline_of_machine_learning#Machine_learning_algorithms
  [70]: https://machinelearningmastery.com/a-tour-of-machine-learning-algorithms/
  [71]: https://scikit-learn.org/stable/
  [72]: https://scikit-learn.org/stable/supervised_learning.html#supervised-learning
  [73]: https://scikit-learn.org/stable/modules/clustering.html#clustering
  [74]: https://scikit-learn.org/stable/modules/decomposition.html#decompositions
  [75]: https://scikit-learn.org/stable/model_selection.html#model-selection
  [76]: https://scikit-learn.org/stable/modules/preprocessing.html#preprocessing
  [77]: https://elitedatascience.com/machine-learning-projects-for-beginners
  [78]: https://github.com/awesomedata/awesome-public-datasets
  [79]: https://github.com/ChristosChristofidis/awesome-deep-learning
  [80]: https://github.com/terryum/awesome-deep-learning-papers
  [81]: https://github.com/endymecy/awesome-deeplearning-resources
  [82]: https://en.wikipedia.org/wiki/K-means_clustering
  [83]: https://en.wikipedia.org/wiki/Mean_shift
  [84]: https://en.wikipedia.org/wiki/DBSCAN
  [85]: https://en.wikipedia.org/wiki/Expectation%E2%80%93maximization_algorithm
  [86]: https://en.wikipedia.org/wiki/Hierarchical_clustering
