title: Solr技术分享
date: 2015-11-05 03:05:33
tags: Solr
---
# Solr技术分享

## Solr 简介

`Solr`是Apache的一个子项目，采用Java开发，基于`Lucene`的全文搜索服务器，同时对其进行了扩展，提供了比Lucene更为丰富的查询语言，同时实现了可配置、可扩展并对查询性能进行了优化，并且提供了一个完善的功能管理界面，是一款非常优秀的全文搜索引擎。  
Solr提供了分面搜索、命中醒目显示并且支持多种输出格式（包括XML/XSLT和JSON格式）。它易于安装和配置，而且附带了一个基于HTTP的管理界面。Solr已经在众多大型的网站中使用，较为成熟和稳定。Solr包装并扩展了Lucene，所以Solr的基本上沿用了Lucene的相关术语。更重要的是，Solr创建的索引与Lucene搜索引擎库完全兼容。通过对Solr进行适当的配置，某些情况下可能需要进行编码，Solr可以阅读和使用构建到其他Lucene应用程序中的索引。此外，很多 Lucene 工具（如Nutch、 Luke）也可以使用Solr 创建的索引。

## Solr原理

Solr对外提供标准的http接口来实现对数据的索引的增加、删除、修改、查询。在Solr中，用户通过向部署在servlet容器中的SolrWeb应用程序发送HTTP请求来启动索引和搜索。Solr接受请求，确定要使用的适当SolrRequestHandler，然后处理请求。通过HTTP以同样的方式返回响应。默认配置返回Solr的标准XML响应，也可以配置Solr 的备用响应格式。  
可以向 Solr 索引 servlet 传递四个不同的索引请求：
+ add/update 允许向 Solr 添加文档或更新文档。直到提交后才能搜索到这些添加和更新。
+ commit 告诉 Solr，应该使上次提交以来所做的所有更改都可以搜索到。
+ optimize 重构Lucene的文件以改进搜索性能。索引完成后执行一下优化通常比较好。如果更新比较频繁，则应该在使用率较低的时候安排优化。一个索引无需优化也可以正常地运行。优化是一个耗时较多的过程。
+ delete 可以通过 id 或查询来指定。按 id 删除将删除具有指定 id 的文档；按查询删除将删除查询返回的所有文档。

## Solr的部署与安装

由于Solr是Java开发，所以他可以被部署在Windows或者Linux上，由于项目中的环境是Linux，所以将只描述Linux环境。

#### Tomcat

Solr需要托管在Tomcat下以及需要安装JDK，安装Tomcat和JDK这里不做过多描述，详细可自行百度

#### 部署Solr

去官网[下载Solr](http://www.apache.org/dyn/closer.lua/lucene/solr/5.3.1)下载Solr，下载完毕以后解压，将Solr的部署包放到tomcat的webapps文件夹下，然后启动tomcat，tomcat会自动将Solr的压缩包解压并部署到tomcat上

#### 创建Solr实例

在官网上下载的Solr解压后，有一个Solr_Home的文件夹，我们将其放在tomcat的文件夹下（或者别的位置，根据自己喜好）

#### 设置Solr_Home

以上部署完毕后，打开`tomcat\webapps\solr\WEB-INF`文件夹，编辑该文件夹下的web.xml文件，找到其中的`<env-entry-value>`节点，将该节点的值修改为上一步中Solr_Home的路径

#### 重启Tomcat

以上操作都完成后，重启Tomcat，然后访问Tomcat的地址+/solr，应该就可以打开Solr的在线管理工具了

