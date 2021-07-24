<a name="Y7JV2"></a>
# 一、概述
ElasticSearch是一个分布式、RESTful风格的搜索和数据分析引擎，能够解决不断涌现出的各种用例。作为Elastic Stack的核心，它集中存储您的数据，帮助您发现意料之中及意料之外的情况。<br />The Elastic Stack,包括ElasticSearch、Kibana（展示）、Beats（采集）和Logstash（传输）（也称为ELK Stack）能够安全可靠的获取任何来源、任何格式的数据，然后实时的对数据进行搜索、分析和可视化。ElasticSearch，简称ES，ES是一个开源的高扩展的分布式全文搜索引擎，是整个ElasticStack技术栈的核心。它可以近乎实时的存储、检索数据；本身扩展性很好，可以扩展到上百台服务器，处理PB级别的数据。

| 特征 | Solr/SolrCloud | Elasticsearch |
| --- | --- | --- |
| 社区和开发者 | Apache软件基金和社区支持 | 单一商业实体及其员工 |
| 节点发现 | Apache Zookeeper，在大量项目中成熟且经过实战测试 | Zen内置于Elasticsearch本身，需要专用的主节点才能进行分裂脑保护 |
| 碎片放置 | 本质上是静态，需要手动工作来迁移分片，从Solr7开始-Autoscaling Api允许一些动态操作 | 动态，可以根据群集状态按需移动分片 |
| 高速缓存 | 全局，每个段更改无效 | 每段，更适合动态更改数据 |
| 分析引擎性能 | 非常适合精确计算的静态数据 | 结果的准确性取决于数据放置 |
| 全文搜索功能 | 基于Lucene的语言分析，多建议，拼写检查，丰富的高亮显示支持 | 基于Lucene的语言分析，单一建议API实现，高亮显示重新计算 |
| 技术支持 | 尚未完全，但即将到来 | 非常好的API |
| 非平面数据处理 | 嵌套文档和父-子支持 | 嵌套和对象类型的自然支持允许几乎无限的嵌套和父-子支持 |
| 查询DSL | JSON（有限），XML（有限）或URL参数 | JSON |
| 索引/收集领导控制 | 领导者安置控制和领导者重新平衡甚至可以节点上的负载 | 不可能 |
| 机器学习 | 内置-在流聚合之上，专注于逻辑回归和学习排名贡献模块 | 商业功能，专注与异常和异常值以及时间序列数据 |

<a name="OkoLE"></a>
# 二、安装
<a name="ldjRd"></a>
## 官网：[https://www.elastic.co/cn/](https://www.elastic.co/cn/)
学习使用下载安装较为简便的windows版本，解压运行elasticsearch.bat即可启动ES服务。<br />**注意：**<br />9300端口为Elasticsearch集群间组件的通信端口，9200端口为浏览器访问的http协议RESTful端口<br />运行完成后可访问localhost:9200，出现如下界面代表ES启动成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625219745803-82f2523c-9586-430b-ba87-4360a7057ce9.png#clientId=uab2bb77f-ab06-4&from=paste&height=311&id=uda93ae34&margin=%5Bobject%20Object%5D&name=image.png&originHeight=311&originWidth=473&originalType=binary&ratio=1&size=13504&status=done&style=none&taskId=u0de5a3f3-7f54-47c1-8616-d1470fbb826&width=473)
<a name="mnQki"></a>
## 问题解决：
1、ES是使用java开发的，需要JDK版本18.以上，默认安装包带有jdk环境，如果系统配置JAVA_HOME，那么使用系统默认的JDK，如果没有配置则使用自带的JDK，一般建议使用系统的JDK。<br />2、双击启动窗口闪退没通过路径访问追踪错误，如果是“空间不足”，请修改config/jvm.options配置文件
<a name="spi4N"></a>
# 三、入门 RESTful & JSON
JSON字符串：网络中传递的字符串格式符合JSON格式<br />ES的数据存储格式就是用的JSON
<a name="u7DdW"></a>
# 四、数据格式
ElasticSearch是面向文档型数据库，一条数据在这里就是一个文档。下图为ElasticSearch存储的文档数据和关系型数据库MySQL存储数据的概念进行一个类比<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625225467602-64f9ea85-febd-4b6c-b958-5beecc3ceeeb.png#clientId=uab2bb77f-ab06-4&from=paste&height=163&id=u5ba906f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=163&originWidth=623&originalType=binary&ratio=1&size=45153&status=done&style=none&taskId=u0a7ae87d-d169-4a5a-af74-5cb0436e5a1&width=623)<br />ES里的Index可以看做一个库，而Types相当于表，Documents则相当于表的行。这里Types的概念已经被逐渐弱化，ElasticSearch6.X中，一个index下已经只能包含一个type，ElasticSearch7.X中，Type的概念已经被删除
<a name="pCQed"></a>
## 倒排索引
**将关键字与文章ID关联，通过关键字查询到文章ID，再通过文章ID查询到整个文章。**<br />Elasticsearch使用一种称为倒排索引的结构，它适用于快速的全文搜索。<br />见其名，知其意，有倒排索引，肯定会对应有正向索引。正向索引（forward index），反向索引（inverted index）更熟悉的名字是倒排索引。<br />所谓的正向索引，就是搜索引擎会将待搜索的文件都对应一个文件ID，搜索时将这个ID和搜索关键字进行对应，形成K-V对，然后对关键字进行统计计数。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625639509438-9208d422-4eee-4378-81bc-62e6d7b81d0f.png#clientId=u389ce190-0009-4&from=paste&id=uf7a69d55&margin=%5Bobject%20Object%5D&name=image.png&originHeight=280&originWidth=639&originalType=url&ratio=1&size=142379&status=done&style=none&taskId=u4426ee23-483b-4530-bfe0-bcc5d6ffef0)<br />但是互联网上收录在搜索引擎中的文档的数目是个天文数字，这样的索引结构根本无法满足实时返回排名结果的要求。所以，搜索引擎会将正向索引重新构建为倒排索引，即把文件ID对应到关键词的映射转换为关键词到文件ID的映射，每个关键词都对应着一系列的文件，这些文件中都出现这个关键词。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625639530459-d67e44c9-175e-495c-b81d-e76690e56029.png#clientId=u389ce190-0009-4&from=paste&id=u398a7b00&margin=%5Bobject%20Object%5D&name=image.png&originHeight=311&originWidth=638&originalType=url&ratio=1&size=139450&status=done&style=none&taskId=u1bdff1e7-1927-4710-9fb8-2a4ef1a8407)
<a name="e03DP"></a>
### 分词器的作用
就是把一句话分成一个一个的词。这个概念在搜索中很重要，比如 This is a banana. 如果按照普通的空格来分词，分成this,is,a,banana，的出来的a其实对我们并没有什么用处。因此需要注意下面的问题：

- 1 区分停顿词（a,or,and这种都属于停顿词）
- 2 大小写转换(Banana与banana)
- 3 时态的转换....

具体的算法可以参考[http://tartarus.org/~martin/PorterStemmer/](http://tartarus.org/~martin/PorterStemmer/)，对照的词语可以参考这里[http://snowball.tartarus.org/algorithms/porter/diffs.txt](http://snowball.tartarus.org/algorithms/porter/diffs.txt)<br />相比中文，就复杂多了。因为中文不能单纯的依靠空格，标点这种进行分词。就比如中华人民共和国国民，不能简单的分成一个词，也不能粗暴的分成中华人民共和国和国民，人民、中华这些也都算一个词！<br />因此常见的分词算法就是拿一个标准的词典，关键词都在这个词典里面。然后按照几种规则去查找有没有关键词，比如:

- 正向最大匹配(从左到右)
- 逆向最大匹配(从右到左)
- 最少切分
- 双向匹配（从左扫描一次，从右扫描一次）

IK，elasticsearch-analysis-ik提供了两种方式,ik_smart就是最少切分，ik_max_word则为细粒度的切分（可能是双向，没看过源码
<a name="Bd2uZ"></a>
### 倒排索引举例
**一个倒排索引由文档中所有不重复词的列表构成，对于其中每个词，有一个包含它的文档列表。例如，假设我们有两个文档，每个文档的内容域包含如下内容：**

- The quick brown fox jumped over the lazy dog
- Quick brown foxes leap over lazy dogs in summer

为了创建倒排索引，我们首先将每个文档的内容域拆分成单独的词（它们称之为词条或tokens )，创建一个包含所有不重复词条的排序列表，然后列出每个词条出现在哪个文档。结果如下所示：<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625641823081-06693b05-9e3a-4f3d-af1b-7a3c0e6c2b2a.png#clientId=u389ce190-0009-4&from=paste&id=u008467e1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=430&originWidth=243&originalType=url&ratio=1&size=9826&status=done&style=none&taskId=u6bc6a0db-13a3-4871-ae70-f1cbe41e45e)<br />如果想搜索 quick brown ，我们只需要查找包含每个词条的文档：<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625641874671-97d45f20-9de7-40bf-9e85-0a0560fdf9cd.png#clientId=u389ce190-0009-4&from=paste&id=u4dd6e952&margin=%5Bobject%20Object%5D&name=image.png&originHeight=153&originWidth=233&originalType=url&ratio=1&size=3473&status=done&style=none&taskId=ue313ec4f-dc82-4ad9-a6cf-dd2f2060cca)
<a name="WV3Ep"></a>
### IK中文分词器
尽可能多分词模式
```json
#原词：
中华人民共和国国歌
#分词
中华人民共和国
中华人民
中华
华人
人民共和国
人民
共和国
共和
国
国歌
歌
```
少分词模式
```json
#原词：
中华人民共和国国歌
#分词
中华人民共和国
国歌
```
<a name="I4Gp4"></a>
### elasticsearch-analysis-pinyin分词器
pinyin分词器可以让用户输入拼音，就能查找到相关的关键词。比如在某个商城搜索中，输入shuihu，就能匹配到水壶。这样的体验还是非常好的。<br />pinyin分词器的安装与IK是一样的，这里就省略掉了。下载的地址[参考github](https://github.com/medcl/elasticsearch-analysis-pinyin).<br />这个分词器在1.8版本中，提供了两种分词规则：

- pinyin,就是普通的把汉字转换成拼音；
- pinyin_first_letter，提取汉字的拼音首字母
<a name="JOVec"></a>
## 不可改变的倒排索引
早期的全文检索会为整个文档集合建立一个很大的倒排索引并将其写入到磁盘。 一旦新的索引就绪，旧的就会被其替换，这样最近的变化便可以被检索到。<br />**倒排索引被写入磁盘后是不可改变的：它永远不会修改。**<br />1、不需要锁。如果你从来不更新索引，你就不需要担心多进程同时修改数据的问题。<br />2、一旦索引被读入内核的文件系统缓存，便会留在哪里，由于其不变性。只要文件系统缓存中还有足够的空间，那么大部分读请求会直接请求内存，而不会命中磁盘。这提供了很大的性能提升。<br />3、其它缓存(像filter缓存)，在索引的生命周期内始终有效。它们不需要在每次数据改变时被重建，因为数据不会变化。<br />4、写入单个大的倒排索引允许数据被压缩，减少磁盘IO和需要被缓存到内存的索引的使用量。
<a name="SOcpt"></a>
## 动态更新索引
**如何在保留不变性的前提下实现倒排索引的更新？**<br />答案是：用更多的索引。通过增加新的补充索引来反映新近的修改，而不是直接重写整个倒排索引。每一个倒排索引都会被轮流查询到,从最早的开始查询完后再对结果进行合并。<br />Elasticsearch基于Lucene，这个java库引入了按段搜索的概念。每一段本身都是一个倒排索引，但索引在 Lucene 中除表示所有段的集合外，还增加了提交点的概念—一个列出了所有已知段的文件。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625643128551-9dd8e2d0-ac35-4cfb-ab07-4c8633c6855c.png#clientId=u389ce190-0009-4&from=paste&id=u6cbde811&margin=%5Bobject%20Object%5D&name=image.png&originHeight=363&originWidth=617&originalType=url&ratio=1&size=84538&status=done&style=none&taskId=u7117312d-a986-45cc-9dcf-d583e857b94)<br />按段搜索会以如下流程执行：<br />一、新文档被收集到内存索引缓存。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625643247615-04dec443-81cb-458a-99e4-e28608052b35.png#clientId=u389ce190-0009-4&from=paste&id=u2074058e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=365&originWidth=506&originalType=url&ratio=1&size=83606&status=done&style=none&taskId=u62083aa1-0896-4250-805f-ae953ff88db)<br />二、不时地, 缓存被提交。<br />一个新的段，一个追加的倒排索引，被写入磁盘。<br />一个新的包含新段名字的提交点被写入磁盘。<br />磁盘进行同步，所有在文件系统缓存中等待的写入都刷新到磁盘，以确保它们被写入物理文件<br />三、新的段被开启，让它包含的文档可见以被搜索。<br />四、内存缓存被清空，等待接收新的文档。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625643398199-229d2a86-8663-466e-826b-0056a3ac2dd2.png#clientId=u389ce190-0009-4&from=paste&id=ud39acd32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=359&originWidth=490&originalType=url&ratio=1&size=85088&status=done&style=none&taskId=ucae3d2fb-fb62-42e0-8b39-43ee82da5a4)<br />当一个查询被触发，所有已知的段按顺序被查询。词项统计会对所有段的结果进行聚合，以保证每个词和每个文档的关联都被准确计算。这种方式可以用相对较低的成本将新文档添加到索引。<br />段是不可改变的，所以既不能从把文档从旧的段中移除，也不能修改旧的段来进行反映文档的更新。取而代之的是，每个提交点会包含一个.del 文件，文件中会列出这些被删除文档的段信息。<br />**当一个文档被“删除”时，它实际上只是在 .del 文件中被标记删除。一个被标记删除的文档仍然可以被查询匹配到，但它会在最终结果被返回前从结果集中移除**。<br />文档更新也是类似的操作方式:当一个文档被更新时，旧版本文档被标记删除，文档的新版本被索引到一个新的段中。可能两个版本的文档都会被一个查询匹配到，但被删除的那个旧版本文档在结果集返回前就已经被移除。<br />

<a name="EdcTy"></a>
# 五、ES基本使用
<a name="w4c2F"></a>
## 创建索引
对比关系型数据库，创建索引就等同于创建数据库<br />在Postman中，向ES服务器发PUT请求：http://127.0.0.1:9200/shopping，发送PUT请求代表创建索引，上面代表创建一个名为shopping的索引
```json
返回相应结果代表创建成功
{
    "acknowledged": true,
    "shards_acknowledged": true,
    "index": "shopping"
}
```
<a name="fwVa8"></a>
## 索引查询
发送HTTP GET请求[http://127.0.0.1:9200/shopping](http://127.0.0.1:9200/shopping)，代表查询shopping的相关信息
```json
{
    "shopping": {
        "aliases": {},
        "mappings": {},
        "settings": {
            "index": {
                "routing": {
                    "allocation": {
                        "include": {
                            "_tier_preference": "data_content"
                        }
                    }
                },
                "number_of_shards": "1",
                "provided_name": "shopping",
                "creation_date": "1625226385790",
                "number_of_replicas": "1",
                "uuid": "sC3uGD5MQDu-eOAa7TZt1g",
                "version": {
                    "created": "7130299"
                }
            }
        }
    }
}
```
发送GET请求http://127.0.0.1:9200/_cat/indices?v查询所有索引的详细信息，非详细信息可以不带v
```json
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   shopping sC3uGD5MQDu-eOAa7TZt1g   1   1          0            0       208b           208b
```
<a name="vcmO4"></a>
## 索引删除
发送HTTP DELETE请求：[http://127.0.0.1:9200/shopping](http://127.0.0.1:9200/shopping) 删除shopping索引
```json
{
    "acknowledged": true
}
```
<a name="vaYty"></a>
## 文档操作
<a name="lzsFe"></a>
### 创建文档
向ES服务器发送POST/PUT请求：http://127.0.0.1:9200/shopping/_doc<br />自定义ES生成的ID格式发送POST/PUT请求：http://127.0.0.1:9200/shopping/_doc/1001，这样返回结果中的ID就不是ES自己生成的ID而是1001<br />当把_doc改为_create代表这是一个新增操作<br />请求体为
```json
{
  "title":"小米手机",
  "category":"小米",
  "images":"http://www.gulixueyuan.com/xm.jpg",
  "price":3999.00
}
```
成功返回
```json
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "rk4bZ3oB2CCwlznO9qWq",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 0,
    "_primary_term": 1
}


{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1001",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 1,
    "_primary_term": 1
}
```
<a name="J91PN"></a>
### 主键查询
HTTP GET请求 [http://127.0.0.1:9200/shopping/_doc/1001](http://127.0.0.1:9200/shopping/_doc/1001)，查询1001关联的文档信息<br />返回
```json
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1001",
    "_version": 1,
    "_seq_no": 1,
    "_primary_term": 1,
    "found": true,
    "_source": {
        "title": "小米手机",
        "category": "小米",
        "images": "http://www.gulixueyuan.com/xm.jpg",
        "price": 3999
    }
}
```
<a name="w3kga"></a>
### 全查询
发送HTTP GET请求[http://127.0.0.1:9200/shopping/](http://127.0.0.1:9200/shopping/)_search<br />返回
```json
{
    "took": 55,//耗费的时间
    "timed_out": false,//是否超时
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": 1,
        "hits": [ //命中的结果
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "rk4bZ3oB2CCwlznO9qWq",
                "_score": 1,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "images": "http://www.gulixueyuan.com/xm.jpg",
                    "price": 3999
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "images": "http://www.gulixueyuan.com/xm.jpg",
                    "price": 3999
                }
            }
        ]
    }
}
```
<a name="abqFP"></a>
### 全量修改
发送HTTP PUT请求[http://127.0.0.1:9200/shopping/_](http://127.0.0.1:9200/shopping/_search)doc/1001，请求体
```json
{
  "title":"小米手机",
  "category":"小米",
  "images":"http://www.gulixueyuan.com/xm.jpg",
  "price":4999.00
}
```
```json
修改成功结果
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1001",
    "_version": 2,
    "result": "updated",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 2,
    "_primary_term": 2
}
再次查询价格已变为4999
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1001",
    "_version": 7,
    "_seq_no": 7,
    "_primary_term": 2,
    "found": true,
    "_source": {
        "title": "小米手机",
        "category": "小米",
        "images": "http://www.gulixueyuan.com/xm.jpg",
        "price": 4999
    }
}
```
<a name="dWBnE"></a>
### 局部修改
局部修改操作不涉及到幂等性所以不能用PUT，要发送HTTP POST请求<br />[http://127.0.0.1:9200/shopping/_update/1001](http://127.0.0.1:9200/shopping/_doc/1001)
```json
请求体
{
  "doc" :{
		"title": "哈哈手机"
	}
}
结果，以前的数据不见了，可能是7.13.2版本该命令直接替换原有内容
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1001",
    "_version": 9,
    "_seq_no": 9,
    "_primary_term": 2,
    "found": true,
    "_source": {
        "doc": {
            "title": "哈哈手机"
        }
    }
}
```
<a name="zuamM"></a>
### 删除
发送HTTP DELETE请求[http://127.0.0.1:9200/shopping/_doc/100](http://127.0.0.1:9200/shopping/_doc/1001)2
```json
删除成功
{
    "_index": "shopping",
    "_type": "_doc",
    "_id": "1002",
    "_version": 3,
    "result": "deleted",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 12,
    "_primary_term": 2
}
```
<a name="NdNT0"></a>
### 条件查询
发送HTTP GET请求[http://127.0.0.1:9200/shopping/_](http://127.0.0.1:9200/shopping/_doc/1002)search?q=category:小米，q的意思代表查询，然后文档中category属性为小米的文档<br />或使用POST请求[http://127.0.0.1:9200/shopping/_search](http://127.0.0.1:9200/shopping/_search)
```json
请求体
{
  "query": {
    "match":{//match_phrase 精确匹配
      "category":"小米"
    	}
	},
  "from":2,//分页起始页
  "size":2,//分页每页多少条
  "_source":["title"],
  "sort":{//排序
  		"price":{//排序字段
      		"order":"desc"//升序降序	
      }
  }
}
```
```json
查询结果，并不是精准查询出小米，应该是根据米分词了
{
    "took": 656,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 3,
            "relation": "eq"
        },
        "max_score": 0.9343092,
        "hits": [
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "rk4bZ3oB2CCwlznO9qWq",
                "_score": 0.9343092,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "images": "http://www.gulixueyuan.com/xm.jpg",
                    "price": 3999
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1003",
                "_score": 0.24116206,
                "_source": {
                    "title": "大米手机",
                    "category": "大米",
                    "images": "http://www.gulixueyuan.com/xm.jpg",
                    "price": 3999
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1004",
                "_score": 0.24116206,
                "_source": {
                    "title": "红米手机",
                    "category": "红米",
                    "images": "http://www.gulixueyuan.com/xm.jpg",
                    "price": 3999
                }
            }
        ]
    }
}
```
<a name="wMUjp"></a>
### 多条件查询
HTTP POST,[http://127.0.0.1:9200/shopping/_search](http://127.0.0.1:9200/shopping/_search)
```json
请求体
{
	"query":{ //查询
		"bool":{//条件
			"must":[//多个条件同时成立
              {
				"match":{//匹配条件
					"category":"小米"
				}
              },{
              "match":{
                  "price":5999
                	}
              }
			]
		}
	}
}
```
<a name="lvEAc"></a>
# 六、ES的集群部署
<a name="ONxfj"></a>
## 概述
       单台ES服务器提供服务，往往都有最大的负载能力，超过这个阈值，服务器性能就会大大降低甚至不可用，所以生成环境中，一般都是运行在指定服务器集群中。<br />除了负载能力，单点服务器也存在其他问题：<br />存储容量有限<br />单独故障后服务瘫痪，无法实现高可用<br />并发处理能力有限<br />配置服务器集群时，集群中节点数量没有限制，大于等于2个节点就可以看做是集群了。一般出于高性能及高可用方面来考虑集群中节点数量都是3个以上
<a name="HOP5A"></a>
## 集群Cluster
一个集群就是由一个或多个服务器节点组织在一起，共同持有整个的数据，并一起提供索引，和搜索功能。一个ES集群有一个唯一的名字标识，这个名字默认就是"elasticsearch"。这个名字是重要的，因为一个节点只能通过指定某个集群的名字，来加入这个集群。
<a name="JVSsI"></a>
## 节点
集群中包含很多服务器，一个节点就是其中的一个服务器。作为集群的一部分，它存储数据，参与集群的索引和搜索功能。<br />一个节点也是由一个名字来标识的，默认情况下，这个名字是一个随机的漫威漫画角色的名字，这个名字会在启动的时候赋予节点。这个名字对于管理工作来说挺重要，因为在这个管理过程中，你会确定网络中的哪些服务器对应与Elasticsearch集群中的哪些节点。<br />一个节点可以通过配置集群名称的方式来加入一个指定的集群。默认情况下，每个节点都会被安排加入到一个叫做"elasticsearch"的集群中，这意味如果你在网络中启动了若干个节点，并假定它们能够互相发现彼此，它们将会自动地形成并加入到一个叫做"elasticsearch"的集群中。
<a name="Lma6v"></a>
## 配置
1、打开config文件夹下的配置文件elasticsearch.yml<br />2、解开配置集群名称的注释cluster.name(多个节点当成一个整体，集群名称必须相同)<br />3、解开配置节点名称的注释node.name（节点名称不能相同）<br />4、解开配置主机名称的注释network.host<br />5、解开配置端口号的注释http.port<br />6、增加节点间通信端口配置transport.tcp.port: 9301<br />7、增加配置node.master: true,node.data: true，表示当前节点可以为master也可以为子节点<br />8、添加跨域配置http.cors.enabled: true，http.cors.allow-origin: "*"<br />9、启动集群并查看集群状态
```json
GET请求     http://127.0.0.1:9201/_cluster/health

{
    "cluster_name": "my-application",
    "status": "green",  //集群状态正常
    "timed_out": false,
    "number_of_nodes": 1,//节点数
    "number_of_data_nodes": 1,//数据节点数
    "active_primary_shards": 0,
    "active_shards": 0,
    "relocating_shards": 0,
    "initializing_shards": 0,
    "unassigned_shards": 0,
    "delayed_unassigned_shards": 0,
    "number_of_pending_tasks": 0,
    "number_of_in_flight_fetch": 0,
    "task_max_waiting_in_queue_millis": 0,
    "active_shards_percent_as_number": 100
}
```
10、多节点增加配置，用来查找其他节点增加到该模块，第一个启动的机器不用增加该配置
```json
discovery.seed_hosts: ["localhost:9301"]//该配置项为数组，后启动的机器需要把之前启动机器
的IP和端口全部配置
discovery.zen.fd.ping_timeout: 1m
discovery.zen.fd.ping_retries: 5
```
11、再次查看集群状态
```json
{
    "cluster_name": "my-application",
    "status": "green",
    "timed_out": false,
    "number_of_nodes": 2,  //节点数量变为2
    "number_of_data_nodes": 2,//数据节点数量变为2
    "active_primary_shards": 0,
    "active_shards": 0,
    "relocating_shards": 0,
    "initializing_shards": 0,
    "unassigned_shards": 0,
    "delayed_unassigned_shards": 0,
    "number_of_pending_tasks": 0,
    "number_of_in_flight_fetch": 0,
    "task_max_waiting_in_queue_millis": 0,
    "active_shards_percent_as_number": 100
}
```
12、将当前节点作为主节点cluster.initial_master_nodes: ["当前节点的node.name"]
<a name="bcAPS"></a>
## linux下ES的部署
修改es目录下config/elasticsearch.yml文件
```json
cluster.name: elasticsearch
node.name: node-1
network.host: 本机IP
http.port: 9200
cluster.initial_master_nodes: ["node-1"]
#集群部署配置
#集群内同时启动的数据任务个数，默认是2个
cluster.routing.allocation.cluster_concurrent_rebalance: 16
#添加或删除节点及负载均衡时并发恢复的线程个数，默认4个
cluster.routing.allocation.node_concurrent_recoveries: 16
#初始化数据恢复时，并发恢复线程的个数，默认4个
cluster.routing.allocation.node_initial_primaries_recoveries: 16
```
修改系统配置文件/etc/security/limits.conf，因为ES生成的数据量和文件量比较多，为了不在控制这些文件出现问题
```json
#文件末尾增加如下内容
#每个进程可以打开的文件数的限制
"linux用户" soft nofile 65536
"linux用户" hard nofile 65536
```
修改系统配置文件/etc/security/limits.d/20-nproc.conf
```json
#文件末尾增加如下内容
#每个进程可以打开的文件数的限制
"linux用户" soft nofile 65536
"linux用户" hard nofile 65536
```
修改/etc/sysctl.conf
```json
#在文件中增加下面内容
#一个进程可以拥有的VMA(虚拟内存区域)的数量，默认值65536
vm.max_map_count=655360
```
重新加载  sysctl -p<br />启动ES
```json
#启动
bin/elasticsearch
#后台启动
bin/elasticsearch -d
```
<a name="gdRC5"></a>
# 七、核心概念
<a name="PBSvT"></a>
## 索引（一切设计都是为了提高搜索的性能）
一个索引就是一个拥有几分相似特征的文档的集合。比如，你可以有一个客户数据的索引，另外一个产品目录的索引，还有一个订单数据的索引。一个索引有一个名字来标识（必须全部是小写字母），并且当我们要对这个索引中的文档进行索引、搜索、更新和删除的时候，都要使用到这个名字。在一个集群中，可以定义任意多的索引。<br />能搜索的数据必须索引，这样的好处是可以提高查询速度。
<a name="Rh7Ek"></a>
## 类型（7.x版本以后不再支持）
在一个索引中，可以定义一种或多种类型。<br />一个类型是索引的一个逻辑上的分类/分区，其语义完全有用户来定。通常会为具有一组共同字段的文档定义一个类型。不同的版本，类型发生了不同的变化
<a name="zgDXC"></a>
## 文档
一个文档是一个可被索引的基础信息单元，也就是一条数据。<br />比如：你可以拥有某一个客户的文档，某一个产品的一个文档。文档以JSON格式来表示，而JSON是一个到处存在的互联网数据交互格式
<a name="iErY4"></a>
## 字段
相当于是数据表的字段，对文档数据根据不同属性进行的分类标识
<a name="hCs04"></a>
## 映射
处理数据的方式和规则方面做一些限制，如：某个字段的数据类型、默认值、分析器、是否被索引等等。这些都是映射里面可以设置的，其他就是处理ES里面数据的一些使用规则设置也叫做映射，按着最优规则处理数据对性能提高很大，因此才需要建立映射，并且需要思考如何建立映射才能对性能更好。
<a name="s6w2h"></a>
## 分片（可理解为Mysql数据库的分表）
一个索引可以存储超出单个节点硬件限制的大量数据。比如，一个具有10亿文档数据的索引占据1TB的磁盘空间，而任一节点都可能没有这样大的磁盘空间。或者单个节点处理搜索请求，响应太慢。为了解决这个问题，Elasticsearch提供了将索引划分成多份的能力，每一份就称之为分片。当你创建一个索引的时候，你可以指定你想要的分片的数量。每个分片本身也是一个功能完善并且独立的“索引”，这个索引可以指到集群中的任何节点上。<br />**分片很重要，主要有两方面原因：**<br />1、允许水平分割/扩展内容容量<br />2、允许在分片之上进行分布式、并行的操作，进而提高性能/吞吐量<br />一个分片怎么分布，文档怎样聚合和搜索请求，是完全由Elasticsearch管理的，对于用户来说无需关心。<br />**被混淆的概念**：一个Lucene索引我们在Elasticsearch称作分片。一个Elasticsearch索引是分片的集合。当Elasticsearch在索引中搜索的时候，他发送查询到每一个属于索引的分片（Lucene索引），然后合并每个分片的结果到一个全局的结果集
<a name="Rilqx"></a>
## 副本
在一个网络/云的环境里，失败随时都有可能发生，在某个分片/节点不知怎么的就处于离线状态，或者由于任何原因消失了，这种情况下，有一个故障转移机制是非常有用并且是强烈推荐的。为此目的Elasticsearch允许你创建分片的一份或多份拷贝，这些拷贝叫做复制分片（副本）。<br />**复制分片重要的两个原因：**<br />1、在分片/节点失败的情况下，提供了高可用性。因为这个原因，注意到复制分片从不与 原/主要分片置于同意节点上是非常重要的。<br />2、扩展你的搜索量/吞吐量，因为搜索可以在所有副本上并行运行<br />总之，每个索引可以被分成多个分片。一个索引也可以被复制0次或多次。一旦复制了，每个索引就有了主分片（作为复制源的原来的分片）和复制分片（主分片的拷贝）之别。分片和复制的数量可以在索引创建的时候指定。在索引创建之后，你可以在任何时候动态的改变复制的数量，但是不能改变分片的数量。默认情况下，Elasticsearch中每个索引被分片1一个主分片和一个复制，这意味着，如果你的集群中至少有两个节点，你的索引将会有1个主分片和另外1个复制分片（1个完全拷贝），这样的话每个索引总共就有2个分片，我们需要根据索引的需要确定分片个数。
<a name="be8aV"></a>
## 分配
将分片分配给某个节点的过程，包括分配主分片或者副本。如果是副本，还包含从主分片复制数据的过程，这个过程是由master节点完成的
<a name="yPiMP"></a>
# 八、系统架构
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625561696065-6a964914-2a2d-46dc-b78f-d75aabec13df.png#clientId=u71197859-8879-4&from=paste&id=u0820efd1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=302&originWidth=600&originalType=url&ratio=1&size=161922&status=done&style=none&taskId=u6b80abad-30d2-49e9-a579-438b7ae9938)<br />一个运行中的 Elasticsearch 实例称为一个节点，而集群是由一个或者多个拥有相同cluster.name 配置的节点组成， 它们共同承担数据和负载的压力。当有节点加入集群中或者从集群中移除节点时，集群将会重新平均分布所有的数据。<br />当一个节点被选举成为主节点时， 它将负责管理集群范围内的所有变更，例如增加、<br />删除索引，或者增加、删除节点等。 而主节点并不需要涉及到文档级别的变更和搜索等操作，所以当集群只拥有一个主节点的情况下，即使流量的增加它也不会成为瓶颈。 任何节点都可以成为主节点。我们的示例集群就只有一个节点，所以它同时也成为了主节点。<br />作为用户，我们可以将请求发送到集群中的任何节点 ，包括主节点。 每个节点都知道任意文档所处的位置，并且能够将我们的请求直接转发到存储我们所需文档的节点。 无论我们将请求发送到哪个节点，它都能负责从各个包含我们所需文档的节点收集回数据，并将最终结果返回給客户端。 Elasticsearch 对这一切的管理都是透明的。
<a name="xmmL8"></a>
# 九、单节点集群
为索引分配3个主分片和一份副本
```json
{
  "settings" :{
     "number_of_shards" : 3,
     "number_of_replicas" : 1
  }
}
```
集群现在是拥有一个索引的单节点集群。所有 3 个主分片都被分配在 node-1 。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625563870383-0b57a3d5-7065-411f-b4c1-e1db49870cf8.png#clientId=u71197859-8879-4&from=paste&id=RHStk&margin=%5Bobject%20Object%5D&name=image.png&originHeight=148&originWidth=574&originalType=url&ratio=1&size=15706&status=done&style=none&taskId=ub6d41784-097e-462b-ad6c-efbe48b77d5)<br />通过 elasticsearch-head 插件（一个Chrome插件）查看集群情况 。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625563878058-04f1db68-f0de-4bbc-a5e7-3a870b1c0a1d.png#clientId=u71197859-8879-4&from=paste&id=u664e8ded&margin=%5Bobject%20Object%5D&name=image.png&originHeight=286&originWidth=1359&originalType=url&ratio=1&size=41298&status=done&style=none&taskId=uc659b015-eb0e-4caf-92a6-f1734948a15)<br />​

​

集群健康值:yellow( 3 of 6 )：表示当前集群的全部主分片都正常运行，但是副本分片没有全部处在正常状态。<br />3 个主分片正常。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625563897939-db0614ba-048e-4d45-9141-8d4f35887c5f.png#clientId=u71197859-8879-4&from=paste&id=u7277563d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=39&originWidth=268&originalType=url&ratio=1&size=4452&status=done&style=none&taskId=u8bbfa5e2-bb75-4a3d-974b-9ad2446944c)<br />3 个副本分片都是 Unassigned，它们都没有被分配到任何节点。 在同 一个节点上既保存原始数据又保存副本是没有意义的，因为一旦失去了那个节点，我们也将丢失该节点 上的所有副本数据。<br />当前集群是正常运行的，但存在丢失数据的风险。
<a name="lK6I8"></a>
# 十、故障转移
当集群中只有一个节点在运行时，意味着会有一个单点故障问题——没有冗余。 幸运的是，我们只需再启动一个节点即可防止数据丢失。当你在同一台机器上启动了第二个节点时，只要它和第一个节点有同样的 cluster.name 配置，它就会自动发现集群并加入到其中。但是在不同机器上启动节点的时候，为了加入到同一集群，你需要配置一个可连接到的单播主机列表。之所以配置为使用单播发现，以防止节点无意中加入集群。只有在同一台机器上运行的节点才会自动组成集群。<br />如果启动了第二个节点，集群将会拥有两个节点 : 所有主分片和副本分片都已被分配 。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564412923-8b6b7e2e-de86-469a-a5d7-e2dc4006083c.png#clientId=u71197859-8879-4&from=paste&id=u70faf3db&margin=%5Bobject%20Object%5D&name=image.png&originHeight=151&originWidth=580&originalType=url&ratio=1&size=21381&status=done&style=none&taskId=u39bcd695-afdd-4843-8d4b-918f1d8ca22)<br />通过 elasticsearch-head 插件查看集群情况<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564433367-0944ee45-49c4-42ba-98bd-b3d59a251e16.png#clientId=u71197859-8879-4&from=paste&id=u7ae11590&margin=%5Bobject%20Object%5D&name=image.png&originHeight=272&originWidth=1353&originalType=url&ratio=1&size=42200&status=done&style=none&taskId=uf01f0a72-830d-48a0-b2f7-3c28cf92d1a)<br />集群健康值:green( 3 of 6 )：表示所有 6 个分片（包括 3 个主分片和 3 个副本分片）都在正常运行。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564448116-3530d775-8140-4f1d-8f4f-7081481dbbed.png#clientId=u71197859-8879-4&from=paste&id=u7f1db51a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=40&originWidth=265&originalType=url&ratio=1&size=5892&status=done&style=none&taskId=u973c5524-e526-46dc-9a93-db3c4742d44)3 个主分片(边框加粗的)正常。<br />第二个节点加入到集群后， 3 个副本分片将会分配到这个节点上——每 个主分片对应一个副本分片。这意味着当集群内任何一个节点出现问题时，我们的数据都完好无损。所 有新近被索引的文档都将会保存在主分片上，然后被并行的复制到对应的副本分片上。这就保证了我们 既可以从主分片又可以从副本分片上获得文档
<a name="xMjbP"></a>
# 十一、水平扩容
怎样为我们的正在增长中的应用程序按需扩容呢？当启动了第三个节点，我们的集群将会拥有三个节点的集群 : 为了分散负载而对分片进行重新分配 。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564748015-5d27d5bd-c386-4551-89a7-6fb8d1952212.png#clientId=u71197859-8879-4&from=paste&id=uaae1e665&margin=%5Bobject%20Object%5D&name=image.png&originHeight=150&originWidth=590&originalType=url&ratio=1&size=27487&status=done&style=none&taskId=u6fece222-ebcd-43d9-ac21-375354386c2)<br />通过 elasticsearch-head 插件查看集群情况。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564758652-d3fe1e79-ece4-47ea-853e-517af97be2da.png#clientId=u71197859-8879-4&from=paste&id=ua26f8def&margin=%5Bobject%20Object%5D&name=image.png&originHeight=330&originWidth=1356&originalType=url&ratio=1&size=47527&status=done&style=none&taskId=u520b1dc9-f322-4e19-8e79-ce147ca1267)<br />集群健康值:green( 3 of 6 )：表示所有 6 个分片（包括 3 个主分片和 3 个副本分片）都在正常运行。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564771020-7540f271-f21a-46e6-8ddc-42d3196a31f9.png#clientId=u71197859-8879-4&from=paste&id=ud3b6a94c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=171&originWidth=370&originalType=url&ratio=1&size=14056&status=done&style=none&taskId=u8f077f2d-9c7b-4fb2-8a4e-7e6c4b18cdb)<br />Node 1 和 Node 2 上各有一个分片被迁移到了新的 Node 3 节点，现在每个节点上都拥有 2 个分片， 而不是之前的 3 个。 这表示每个节点的硬件资源（CPU, RAM, I/O）将被更少的分片所共享，每个分片 的性能将会得到提升。<br />分片是一个功能完整的搜索引擎，它拥有使用一个节点上的所有资源的能力。 我们这个拥有 6 个分 片（3 个主分片和 3 个副本分片）的索引可以最大扩容到 6 个节点，每个节点上存在一个分片，并且每个 分片拥有所在节点的全部资源。<br />但是如果我们想要扩容超过 6 个节点怎么办呢？<br />主分片的数目在索引创建时就已经确定了下来。实际上，这个数目定义了这个索引能够<br />存储 的最大数据量。（实际大小取决于你的数据、硬件和使用场景。） 但是，读操作——<br />搜索和返回数据——可以同时被主分片 或 副本分片所处理，所以当你拥有越多的副本分片<br />时，也将拥有越高的吞吐量。<br />在运行中的集群上是可以动态调整副本分片数目的，我们可以按需伸缩集群。让我们把<br />副本数从默认的 1 增加到 2。
```json
#PUT http://127.0.0.1:1001/users/_settings
{
    "number_of_replicas" : 2
}
```
users 索引现在拥有 9 个分片： 3 个主分片和 6 个副本分片。 这意味着我们可以将集群<br />扩容到 9 个节点，每个节点上一个分片。相比原来 3 个节点时，集群搜索性能可以提升 3 倍。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564866845-2289fd0d-a3a1-49e2-8cb3-333d59dcbb0d.png#clientId=u71197859-8879-4&from=paste&id=u9fd4edc0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=149&originWidth=582&originalType=url&ratio=1&size=26850&status=done&style=none&taskId=u9d4b42e5-9200-4e80-a5af-f72d2225444)<br />通过 elasticsearch-head 插件查看集群情况：<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625564876594-5e0bd668-471b-4505-933b-d38029de6453.png#clientId=u71197859-8879-4&from=paste&id=uc10cdc91&margin=%5Bobject%20Object%5D&name=image.png&originHeight=338&originWidth=1353&originalType=url&ratio=1&size=49312&status=done&style=none&taskId=ue0e3df82-d06e-4137-8e3c-7f4a9cd14f4)<br />当然，如果只是在相同节点数目的集群上增加更多的副本分片并不能提高性能，因为每个分片从节点上获得的资源会变少。 你需要增加更多的硬件资源来提升吞吐量。<br />但是更多的副本分片数提高了数据冗余量：按照上面的节点配置，我们可以在失去 2 个节点<br />的情况下不丢失任何数据。
<a name="l2CBo"></a>
# 十二、应对故障
我们关闭第一个节点，这时集群的状态为:关闭了一个节点后的集群。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625565423568-9d6b7dfa-0381-4ef5-beb3-c5f57f1ab5e7.png#clientId=u71197859-8879-4&from=paste&id=uf6dd4f3c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=146&originWidth=589&originalType=url&ratio=1&size=22187&status=done&style=none&taskId=uf38e3cd7-29d4-41e8-a782-23de94010f3)<br />我们关闭的节点是一个主节点。而集群必须拥有一个主节点来保证正常工作，所以发生的第一件事情就是选举一个新的主节点： Node 2 。在我们关闭 Node 1 的同时也失去了主<br />分片 1 和 2 ，并且在缺失主分片的时候索引也不能正常工作。 如果此时来检查集群的状况，我们看到的状态将会为 red ：不是所有主分片都在正常工作。<br />幸运的是，在其它节点上存在着这两个主分片的完整副本， 所以新的主节点立即将这些分片在 Node 2 和 Node 3 上对应的副本分片提升为主分片， 此时集群的状态将会为yellow。这个提升主分片的过程是瞬间发生的，如同按下一个开关一般。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625565448292-f3aba217-9adc-4a74-9727-4308c459ad0d.png#clientId=u71197859-8879-4&from=paste&id=u3b1b8d88&margin=%5Bobject%20Object%5D&name=image.png&originHeight=334&originWidth=1355&originalType=url&ratio=1&size=47884&status=done&style=none&taskId=u25ccfb9e-f338-417d-bb89-24795ad17ef)<br />集群可以将缺失的副本分片再次进行分配，那么集群的状态也将恢复成之前的状态。 如果 Node 1 依然拥有着之前的分片，它将尝试去重用它们，同时仅从主分片复制发生了修改的数据文件。和之前的集群相比，只是 Master 节点切换了。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625565489289-ba5414b1-17ea-4f17-9b70-6af02fc560c7.png#clientId=u71197859-8879-4&from=paste&id=u18f53535&margin=%5Bobject%20Object%5D&name=image.png&originHeight=233&originWidth=1363&originalType=url&ratio=1&size=56408&status=done&style=none&taskId=uac7730d4-4aa7-42b1-a2ac-bf7062d24e2)
<a name="eKtCJ"></a>
# 十三、路由计算
索引一个文档的时候，文档会被存储到一个主分片中。 Elasticsearch 如何知道一个文档应该存放到哪个分片中呢？当我们创建文档时，它如何决定这个文档应当被存储在分片 1 还是分片 2 中呢？首先这肯定不会是随机的，否则将来要获取文档的时候我们就不知道从何处寻找了。实际上，这个过程是根据下面这个公式决定的：
```json
shard = hash(routing) % number_of_primary_shards
```
routing 是一个可变值，默认是文档的 _id ，也可以设置成一个自定义的值。 routing 通过hash 函数生成一个数字，然后这个数字再除以 number_of_primary_shards （主分片的数量）后得到余数 。这个分布在 0 到 number_of_primary_shards-1 之间的余数，就是我们所寻求的文档所在分片的位置。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625565560163-2ab193fe-3fdc-4122-9ba0-7f50c04f16eb.png#clientId=u71197859-8879-4&from=paste&id=ueae0776d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=522&originWidth=1002&originalType=url&ratio=1&size=315633&status=done&style=none&taskId=ueeb3aea3-11f5-400f-b8a9-11038b80eaa)<br />这就解释了为什么我们要在创建索引的时候就确定好主分片的数量并且永远不会改变这个数量:因为如果数量变化了，那么所有之前路由的值都会无效，文档也再也找不到了。<br />所有的文档API ( get . index . delete 、 bulk , update以及 mget ）都接受一个叫做routing 的路由参数，通过这个参数我们可以自定义文档到分片的映射。一个自定义的路由参数可以用来确保所有相关的文档—一例如所有属于同一个用户的文档——都被存储到同一个分片中。
<a name="PiidF"></a>
# 十四、分片控制
我们可以发送请求到集群中的任一节点。每个节点都有能力处理任意请求。每个节点都知道集群中任一文档位置，所以可以直接将请求转发到需要的节点上。在下面的例子中，如果将所有的请求发送到Node 1001，我们将其称为协调节点**coordinating node**。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625565623502-5f9bbde5-adf7-43ec-bcaf-ce3399493201.png#clientId=u71197859-8879-4&from=paste&id=uf41b8b4c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=561&originWidth=1154&originalType=url&ratio=1&size=397658&status=done&style=none&taskId=u3f9821d1-d6bc-4a15-bdbd-7f515a6f176)<br />当发送请求的时候， 为了扩展负载，更好的做法是轮询集群中所有的节点。
<a name="smS5B"></a>
# 十五、数据写流程
新建、索引和删除请求都是写操作， 必须在主分片上面完成之后才能被复制到相关的副本分片。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625566361891-a9ff15bb-4f08-4554-a372-96980c64cd1d.png#clientId=u71197859-8879-4&from=paste&id=ub8bd03d1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=677&originWidth=1081&originalType=url&ratio=1&size=548495&status=done&style=none&taskId=u6b5b6f96-8f1e-4f08-9d69-69d1bb62313)<br />在客户端收到成功响应时，文档变更已经在主分片和所有副本分片执行完成，变更是安全的。有一些可选的请求参数允许您影响这个过程，可能以数据安全为代价提升性能。这些选项很少使用，因为 Elasticsearch 已经很快，但是为了完整起见， 请参考下文：<br />**1、consistency**<br />即一致性。在默认设置下，即使仅仅是在试图执行一个写操作之前，主分片都会要求必须要有规定数量quorum（或者换种说法，也即必须要有大多数）的分片副本处于活跃可用状态，才会去执行写操作（其中分片副本 可以是主分片或者副本分片）。这是为了避免在发生网络分区故障（network partition）的时候进行写操作，进而导致数据不一致。 规定数量即：** int((primary + number_of_replicas) / 2 ) + 1**<br />**consistency 参数的值可以设为**：<br />one ：只要主分片状态 ok 就允许执行写操作。<br />all：必须要主分片和所有副本分片的状态没问题才允许执行写操作。<br />quorum：默认值为quorum , 即大多数的分片副本状态没问题就允许执行写操作。<br />**注意**，规定数量的计算公式中number_of_replicas指的是在索引设置中的设定副本分片数，而不是指当前处理活动状态的副本分片数。如果你的索引设置中指定了当前索引拥有3个副本分片，那规定数量的计算结果即：**int((1 primary + 3 replicas) / 2) + 1 = 3**，如果此时你只启动两个节点，那么处于活跃状态的分片副本数量就达不到规定数量，也因此您将无法索引和删除任何文档。<br />**2、timeout**<br />如果没有足够的副本分片会发生什么？Elasticsearch 会等待，希望更多的分片出现。默认情况下，它最多等待 1 分钟。 如果你需要，你可以使用timeout参数使它更早终止：100是100 毫秒，30s是30秒。<br />新索引默认有1个副本分片，这意味着为满足规定数量应该需要两个活动的分片副本。 但是，这些默认的设置会阻止我们在单一节点上做任何事情。为了避免这个问题，要求只有当number_of_replicas 大于1的时候，规定数量才会执行。
<a name="qLF7l"></a>
# 十六、数据读流程
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625567239302-912e7a67-58d2-4366-b8be-fe36b849d850.png#clientId=u71197859-8879-4&from=paste&id=ue72c1a8d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=348&originWidth=752&originalType=url&ratio=1&size=211724&status=done&style=none&taskId=u8047f84d-2f90-495e-baa3-14f0ca524b1)<br />在处理读取请求时，协调结点在每次请求的时候都会通过轮询所有的副本分片来达到负载均衡。在文档被检索时，已经被索引的文档可能已经存在于主分片上但是还没有复制到副本分片。 在这种情况下，副本分片可能会报告文档不存在，但是主分片可能成功返回文档。 一旦索引请求成功返回给用户，文档在主分片和副本分片都是可用的。
<a name="vNX69"></a>
# 十七、更新流程
部分更新一个文档结合了先前说明的读取和写入流程<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625623841286-50bf917a-35b4-4e1e-b9ad-24e6cec33b14.png#clientId=u389ce190-0009-4&from=paste&id=u0cde8e6a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=245&originWidth=608&originalType=url&ratio=1&size=50710&status=done&style=none&taskId=ub78e46d5-bd3f-405b-bd0f-75bb6c84827)<br />部分更新一个文档的步骤如下：​<br />1、客户端向Node 1发送更新请求。<br />2、它将请求转发到主分片所在的Node 3 。<br />3、Node 3从主分片检索文档，修改_source字段中的JSON，并且尝试重新索引主分片的文档。如果文档已经被另一个进程修改,它会重试步骤3 ,超过retry_on_conflict次后放弃。<br />4、如果 Node 3成功地更新文档，它将新版本的文档并行转发到Node 1和 Node 2上的副本分片，重新建立索引。一旦所有副本分片都返回成功，Node 3向协调节点也返回成功，协调节点向客户端返回成功。<br />当主分片把更改转发到副本分片时， 它不会转发更新请求。 相反，它转发完整文档的新版本。请记住，这些更改将会异步转发到副本分片，并且不能保证它们以发送它们相同的顺序到达。 如果 Elasticsearch 仅转发更改请求，则可能以错误的顺序应用更改，导致得到损坏的文档。
<a name="O1LjJ"></a>
# 十八、批量操作流程
mget和 bulk API的模式类似于单文档模式。区别在于协调节点知道每个文档存在于哪个分片中。它将整个多文档请求分解成每个分片的多文档请求，并且将这些请求并行转发到每个参与节点。<br />协调节点一旦收到来自每个节点的应答，就将每个节点的响应收集整理成单个响应，返回给客户端。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625639184311-7cff09fc-8d36-4223-b560-a62cc1d52267.png#clientId=u389ce190-0009-4&from=paste&id=u05c962dc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=206&originWidth=600&originalType=url&ratio=1&size=55465&status=done&style=none&taskId=u7b348d47-4e02-4092-b972-a91294280a5)<br />**用单个 mget 请求取回多个文档所需的步骤顺序:**<br />1、客户端向 Node 1 发送 mget 请求。<br />2、Node 1为每个分片构建多文档获取请求，然后并行转发这些请求到托管在每个所需的主分片或者副本分片的节点上。一旦收到所有答复，Node 1 构建响应并将其返回给客户端。<br />可以对docs数组中每个文档设置routing参数。<br />bulk API， 允许在单个批量请求中执行多个创建、索引、删除和更新请求。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1625639278278-314df525-f58a-4601-8759-c2c574f4d7bd.png#clientId=u389ce190-0009-4&from=paste&id=uc028fda2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=259&originWidth=603&originalType=url&ratio=1&size=53343&status=done&style=none&taskId=u50be2931-abe0-40f6-908b-64e2c5c3d86)<br />**bulk API 按如下步骤顺序执行：**<br />1、客户端向Node 1 发送 bulk请求。<br />2、Node 1为每个节点创建一个批量请求，并将这些请求并行转发到每个包含主分片的节点主机。<br />3、主分片一个接一个按顺序执行每个操作。当每个操作成功时,主分片并行转发新文档（或删除）到副本分片，然后执行下一个操作。一旦所有的副本分片报告所有操作成功，该节点将向协调节点报告成功，协调节点将这些响应收集整理并返回给客户端。
<a name="Fn5gy"></a>
# 十九、文档搜索
[

](https://blog.csdn.net/u011863024/article/details/115721328)<br />​<br />
