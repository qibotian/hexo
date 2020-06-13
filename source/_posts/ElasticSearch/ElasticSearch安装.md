---
title: ElasticSearch安装
date: 2019-06-07
categories: ['ElasticSearch']
tags: ['ElasticSearch']
comments: true
---

-   简介
    Elasticsearch 是一个 **基于JSON** 、 **分布式**、**RESTful** 风格的搜索和数据分析引擎，能够解决不断涌现出的各种用例。

-   官网地址  
    <https://www.elastic.co/cn/>

  ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104622881.png)

-   es可以用来做什么
-   Logs 快速且可扩展的日志管理
-   Metrics 对您的系统指标进行检测和可视化
-   APM 获得有关自己应用程序性能的洞见
-   Uptime 检测可用性问题，并进行应对
-   Site Search 卓越的所搜
-   App Search 搜索文档，地理数据等形形色色的内容
-   Workplace Search 集中式搜索，应对企业内的数据孤岛情况
-   Maps 实时探索位置数据
-   SIEM 交互式调查和自动威胁检测
-   Endpoint Security 预防检测猎捕并应对威胁
    ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104709673.png)

-   下载地址  

    -   Es下载地址 <https://mirrors.huaweicloud.com/elasticsearch/7.6.2/>
    -   logstash下载地址 <https://mirrors.huaweicloud.com/logstash/>
    -   kibana 下载地址 <https://mirrors.huaweicloud.com/kibana>

    **需要jdk1.8以上的环境支持，都是免安装的，解压后即可使用**


-   elasticsearch 跨越设置  
      在`\config\elasticsearch.yml`最下面加入以下设置  

    ```yml
    http.cors.enabled: true
    http.cors.allow-origin: "*"
    ```

-   ik 分词器安装

    -   官网地址 （<https://github.com/medcl/elasticsearch-analysis-ik）>
    -   说明
        中文分词器
    -   下载地址，**选择与es对应的版本**  
        <https://github.com/medcl/elasticsearch-analysis-ik/releases>
    -   安装方式
        将下载的文件解压到`es目录\plugins\`下
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104737725.png)
    -   重启es,并查看加载情况
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104748449.png)
    -   分词方式
        -   ik_smart (最少分词)
            ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104849161.png)
        -   ik_max_word （最细粒度分词）
            ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104901929.png)
    -   加载自定义分词  
        在`\plugins\ik\config\IKAnalyzer.cfg.xml`中加上自己的分词文件
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104916622.png)
        并在当前目录新增自己的分词文档`qibotian.dic`,注意必须以**UTF-8**的格式保存。
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104925631.png)
        然后并重启es，并检查加载情况
      ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104934731.png)
        添加前：
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613104957755.png)
        添加后：
        ![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200613105009736.png)


-   运行es  
    在`bin\elasticsearch.bat`即可运行，

-   访问es  
    在浏览器中访问`127.0.0.1:9200`即可访问
    ![](http://qiniu.yangrouhubo.com/markdown-img-paste-2020061310502588.png)


-   kibana汉化  
    在`config\kinaba.yml`中添加以下代码

    ```yml
    i18n.locale: "zh-CN"
    ```

-   启动kibana,并测试  
    Kibana 是通向 Elastic 产品集的窗口。 它可以在 Elasticsearch 中对数据进行视觉探索和实时分析。  
    运行`bin\kibana.bat`, 并访问 `localhost:5601`


-   es 和 solr 的对比

| 比较模式 | es                              | solr                |
| ---- | ------------------------------- | ------------------- |
| 安装方式 | 开箱即用                            | 比较复杂                |
| 集群模式 | 自带集群                            | 需要依赖zk              |
| 数据格式 | 仅支持JSON                         | 支持JSON，XML,CSV等文件格式 |
| 功能支持 | 仅支持核心功能，其他需要插件支持，比如kibana的图像化界面 | 官方支持功能比较多           |
| 查询速度 | 即时查询很快，更适合实时查询                  | 查询快，但是更新索引速度慢       |
