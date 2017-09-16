---
layout: post
title: "Node常用缓存技术"
tags:
    -JavaScript
categories:
    javascript
---

## 为什么要用缓存

- 性能：将相应数据存储起来以避免数据的重复创建、处理和传输，可有效提高性能。比如将不改变的数据缓存起来，例如国家列表等，这样能明显提高web程序的反应速度；

- 稳定性：同一个应用中，对同一数据、逻辑功能和用户界面的多次请求时经常发生的。当用户基数很大时，如果每次请求都进行处理，消耗的资源是很大的浪费，也同时造成系统的不稳定。例如，web应用中，对一些静态页面的呈现内容进行缓存能有效的节省资源，提高稳定性。而缓存数据也能降低对数据库的访问次数，降低数据库的负担和提高数据库的服务能力；

- 可用性：有时，提供数据信息的服务可能会意外停止，如果使用了缓存技术，可以在一定时间内仍正常提供对最终用户的支持，提高了系统的可用性。

## 缓存的分类
- 本地缓存
    - 文件缓存
    - 内存缓存
        - lru-cache

            LUR(least recently used) 是根据数据的活跃度进行更新的缓存算法
    - 内存文件缓存
        - 利用linux系统的/dev/shm/
        
            因为 /dev/shm/这个目录不在硬盘上，而是在内存里，它就所谓的tmpfs。在Redhat/CentOS等linux发行版中默认大小为物理内存的一半。

- 外部缓存
    - memcache: 是一套分布式的高速缓存系统
    - Redis: 是一个开源的支持网络、可基于内存亦可持久化的日志型、Key-Value数据库


## 参考资料
 - [介绍缓存的基本概念和常用的缓存技术](http://blog.csdn.net/smxjant/article/details/77991923)
 - [MemCache](https://baike.baidu.com/item/MemCache)
 - [Redis](https://baike.baidu.com/item/Redis)
 - [Linux目录下/dev/shm的理解和使用](http://blog.csdn.net/stone8761/article/details/50715467)