---
tags: [changelog, elasticsearch, search]
title: note-search-elasticsearch
created: '2020-03-29T15:38:04.974Z'
modified: '2020-07-10T02:27:38.041Z'
---

# note-search-elasticsearch

## faq

- elasticsearch vs solr
  - 当实时建立索引的时候，solr会产生IO阻塞，而es则不会，所以es查询性能要高于solr
  - 在不断动态添加数据的时候，solr的检索效率会变低，而es则没有什么变化
  - 集群中节点发现，solr利用zookeeper进行分布式管理，而es自身带有分布式系统管理功能
  - solr一般部署到web服务器上，比如tomcat，solr的本质是一个动态web项目
  - solr支持更多的格式数据【xml、json、csv】，而es仅支持json文件格式
  - solr是传统搜索应用的有力解决方案，但是es更适合用于新兴的实时搜索应用
  - 单纯对已有数据进行检索的时候，solr效率高，但实时搜索的时候es效率高
  - solr官网提供的功能更多，而es本身更注重于核心功能，高级功能有多个第三方插件
  - ref
    - https://zhuanlan.zhihu.com/p/61257030

## docs

- ref
  - https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html
  - https://juejin.im/post/5d921442e51d4578364f6fd3
  
- **changelog**    
- 7.0.0-201904
  - 7.1开始，Security功能免费使用
  - 集群连接变化：TransportClient被废弃，es7的java代码只能使用rest client，建议采用RestHighLevelClient的方式操作ES集群
  - Zen2是Elasticsearch的全新集群协调层，提高了性能，并更易于使用
  - ES程序包默认打包jdk： 以至于7.x版本的程序包大小突然边300MB+ 对比6.x发现，包大了200MB+， 正是JDK的大小
  - Lucene9.0的支持
  - 正式废除单个索引下多Type的支持，在es7中使用默认的_doc作为type，官方会在8.x版本会彻底移除type
  - 兼容性：es 7.0 can read indices created in version 6.0 or above. 
    - An es 7.0 node will not start in the presence of indices created in a version of es before 6.0.
    - Indices created in es 5.x or before will need to be reindexed with es 6.x in order to be readable by es 7.x.
  - Index creation no longer defaults to five shards
    - Previous versions of Elasticsearch defaulted to creating five shards per index.
    - Starting with 7.0.0, the default is now one shard per index.
  - 查询相关性速度优化：Weak-AND算法，原理是取TOP N结果集，估算命中记录数
- 6.0.0-201708
  - 无缝滚动升级
  - Index sorting，即索引阶段的排序
  - 顺序号的支持，每个es的操作都有一个顺序编号（类似增量设计）
  - Load aware shard routing，基于负载的请求路由，目前的搜索请求是全节点轮询，那么性能最慢的节点往往会造成整体的延迟增加，新的实现方式将基于队列的耗费时间自动调节队列长度，负载高的节点的队列长度将减少，让其他节点分摊更多的压力，搜索和索引都将基于这种机制
  - 已经关闭的索引将也支持replica的自动处理，确保数据可靠
- 5.0.0-201610
  - Lucene 6.x的支持，磁盘空间少一半；索引时间少一半；查询性能提升25%；
  - Internal engine级别移除了用于避免同一文档并发更新的竞争锁，带来15%-20%的性能提升
  - 新增Sliced Scroll类型，现在Scroll接口可以并发来进行数据遍历了。每个Scroll请求，可以分成多个Slice请求
  - 新增了Profile API，新增了Rollover API，新增Reindex
  - 限制索引请求大小，避免大量并发请求压垮 ES
  - 限制单个请求的shards数量，默认1000个
- 2.0.0-201510
  - 增加了pipleline Aggregations
  - query/filter查询合并，都合并到query中，根据不同的上下文执行不同的查询
  - 存储压缩可配置
  - Rivers模块被移除
  - Multicast组播发现被移除，成为一个插件，生产环境必须配置单播地址
- 1.0.0-201402
  - 支持Aggregations聚合分析
  - Snapshot/Restore API 备份恢复API
  - CAT API 支持
  - 支持联盟查询
  - 断路器支持
  - Doc values 引入
- 0.7.0-201005
  - es集群自动发现模块Zen Discovery
  - 简单的插件管理机制
  - 更好支持ICU分词器
  - 更多的管理API
