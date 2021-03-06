把自己找到的语料和语言资源整理一下，避免以后需要的时候又浪费时间去收集（长期坑位）。

目录：

- [1. 中文语料](#1)
	- [1.1 生语料](#1.1)
	- [1.2 结构化数据](#1.2)
	- [1.3 文本分类数据集](#1.3)
	- [1.4 序列标注数据集（分词、命名实体识别、词性标注等）](#1.4)
- [2. 外语语料](#2)
 	- [2.1 生语料](#2.1)
	- [2.2 结构化数据](#2.2)
	- [2.3 文本分类数据集](#2.3)
	- [2.4 序列标注数据集（分词、命名实体识别、词性标注等）](#2.4)
- [3. 语言资源](#3)
	- [3.1 实体类](#3.1)
	- [3.2 词典类](#3.2)


<h1 id='1'>1. 中文语料</h1>

<h2 id='1.1'>1.1 生语料</h2>

<h3 id='1.1.1'>1.1.1 人民日报新闻数据</h3>

包含1946年-2003年人民日报全部数据以及文革网（2005-2008）全部图文数据库。原始发布地址不详，只找到转载的[页面](http://www.360doc.com/content/10/0415/14/257553_23177268.shtml)，作者邮箱应该是 bjdjssgmzsf@yahoo.com ，联系过，没收到回复。原始数据是图文数据库，我将其转存[百度网盘](https://pan.baidu.com/s/1YJ6vVfJQVVLGavs1hAdSuQ)，然后单独整理了一个sql文件方便使用和查询。大多数情况下，只需要考虑文本内容，我写了一个脚本[rmrb.py](./Chinese/raw_corpus/rmrb.py)将所有新闻导出到txt文件中，方便使用。新闻一共有137万多条。

---

<h2 id='1.2'>1.2 结构化数据</h2>

<h3 id='1.2.1'>1.2.1 中国古代人物传记数据库（CBDB）</h3>

[中国历代人物传记数据库](https://projects.iq.harvard.edu/cbdb)（The China Biographical Database, CBDB）是一个线上关系型数据库，其远期目标在于系统性地收入中国历史上所有重要的传记资料，其内容无限制地、免费地提供学术研究。截止2018年9月为止，该数据库一共收录了422,600人的传记资料，这些人主要出自七世纪至十九世纪，该数据库目前致力于增录更多的唐代和明清的人物传记资料。

CBDB的数据是用access和sqlite两种数据库进行存储，我转了一个mysql的[版本](https://pan.baidu.com/s/1olG3Fnn6gCqyo9lgNKYhrw)，表格和字段的具体说明请参考官网。由于数据是不断更新的，需要最新数据的请到官网下载。脚本[cbdb.py](./Chinese/structural_data/cbdb.py)是将sqlite中的数据导入mysql中，如果数据库表格发生改变，可能需要更新一下脚本。

<h2 id='1.3'>1.3 文本分类数据集</h2>

<h3 id='1.3.1'>1.3.1 2017知乎看山杯数据</h3>

该数据集用于评测多标签文本分类（multi-label classification），任务请参考[比赛官网](https://www.biendata.com/competition/zhihu/data/)，数据集格式参考本项目[zhihu_detail.txt](./Chinese/classification/zhihu_detail.txt)文件。由于数据是经过脱敏处理，不包含真实文字，可能使用场景有限，比较适合多标签分类任务的练习和模型验证。

- [ieee_zhihu_cup.des3](https://pan.baidu.com/s/1-EiRzcv0FfYnR_sqyMGVOw)：为Linux/Mac下的压缩文件，数据集解压命令，dd if=ieee_zhihu_cup.des3 |openssl des3 -d -k Pg5EnkJP7iYyRBt5|tar zxf -
- [ieee_zhihu_cup.rar]()：为windows下的rar格式压缩文件（官网取消了文件分享，我只保留了Linux压缩包，有知道的朋友可以说一下，我加进来）。

---

<h3 id='1.3.2'>1.3.2 SMP2017中文人机对话评测数据</h3>

包含了两个任务的[数据集](https://github.com/HITlilingzhi/SMP2017ECDT-DATA)：用户意图领域分类，特定域任务型人机对话在线评测。第一个数据集用得比较多。用户意图领域分类包含闲聊类、任务垂直类共三十一个类别，属于短文本分类的一个范畴。

---

<h2 id='1.4'>1.4 序列标注数据集（分词、命名实体识别、词性标注等）</h2>

<h3 id='1.4.1'>1.4.1 1998年1月-6月人民日报标注语料</h3>

1300W字的新闻[标注语料](https://pan.baidu.com/s/17djsvYfpYUXrazL0H_mtoA)，该语料可用于分词、NER、POS等任务。标记和格式请参考此[文章](https://cloud.tencent.com/developer/article/1091906)。

<h1 id='2'>2. 外语语料</h1>

<h2 id='2.1'>2.1 生语料</h2>

<h2 id='2.2'>2.2 结构化数据</h2>

<h2 id='2.3'>2.3 文本分类数据集</h2>

<h2 id='2.4'>2.4 序列标注数据集（分词、命名实体识别、词性标注等）</h2>

<h1 id='3'>3. 语言资源</h1>

实验室10年爬过百科，全部数据太大就不放出来了，只抽取一些可能有用的词汇。根据当时百科页面的标签来筛选实体类型（人名、地名），存在一定噪音，酌情使用。

<h2 id='3.1'>3.1 实体类（人名、地名等）</h2>

<h3 id='3.1.1'>3.1.1 地名（抽于2010年的百度百科）</h3>

95433个[地名](https://pan.baidu.com/s/1CpIr1qPAUen2pfisWXMxqQ)

<h3 id='3.1.2'>3.1.2 人名（抽于2010年的百度百科）</h3>

278577个[人名](https://pan.baidu.com/s/1OuKC3ax9Qk5krL_vH10-kg)

<h3 id='3.1.3'>3.1.3 人名（抽于2017年的CBDB）</h3>

227266个[人名](https://pan.baidu.com/s/1YMLxdAgKNrviaYC1cqod4Q)

<h2 id='3.2'>3.2 词典类</h2>

<h3 id='3.2.1'>3.2.1 百科词条名（抽于2010年的百度百科）</h3>

一千万个[词条名](https://pan.baidu.com/s/1DkgtFmhpxxq6Qx67PgU10A)

<h3 id='3.2.2'>3.2.2 360万中文词库（包含词性和词频）</h3>

该[资源](https://pan.baidu.com/s/11T4CNHAQ30EHj456-gJVwQ)作者为刘邵博，由其综合多本词典整合的一个大词典，词典共有词汇3669216个词汇。词典结构为：词语\t词性\t词频。词频是用ansj分词对270G新闻语料进行分词统计词频获得。