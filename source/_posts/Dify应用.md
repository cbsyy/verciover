---
title: Dify应用开发
date: 2025-02-12 14:28:37
categories: Dify
tags:
  - Dify
  - 应用
---

ollama url
http://localhost:11434
http://host.docker.internal:11434

## Dify下载部署本地
https://blog.csdn.net/He_r_o/article/details/141105083?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522af75d5d326be0c04ed881163630d2e95%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=af75d5d326be0c04ed881163630d2e95&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-141105083-null-null.142^v101^pc_search_result_base3&utm_term=dify&spm=1018.2226.3001.4187

https://blog.csdn.net/u010522887/article/details/141407784



# 当前任务：
数据查询---主要看  提供表结构能不能准确生成  查询sql
识别到表名和字段名

# 实现方式思路：
用户询问一个问题->llm将问题处理成sql语句->到数据库查询相关内容->返回给llm解析回答

加入agent，但也只是多个表单独查询，并没有真正的多表关联查询。我们自己的做法是在数据库端把表整合为视图，尽可能降低多表关联查询的需求，以降低大模型的难度，获得更稳定的结果

通过循环
可能要从工程方面入手和llm两方面入手 优化
主要是数据工程，比如 建立数据集市，LLM只生成集市层面的SQL
数据集市 是面向业务域 被清洗过的数据

这样做是类似在数据库端把表整合为视图，尽可能降低多表关联查询的需求，以降低大模型的难度，获得更稳定的结果。
我还做了点小优化 用户传问题 我就把比较难理解的问题提前用kimi帮我生成了sql查询语句 然后相当于存到了知识库，然后到生成sql要去数据库找的时候 就是问题+知识库检索出来的一起转sql查了
