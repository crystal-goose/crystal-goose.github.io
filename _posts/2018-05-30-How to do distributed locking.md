---
layout: post
title: How to do distributed locking
---

# How to do distributed locking

Martin Kleppmann 是 DDIA （Design Data Intensive Web Applications）的作者。他认为 [redlock](https://redis.io/topics/distlock) 分布式锁是不安全的。Redlock 是基于 Redis 的分布式锁。在文章中也介绍了如何正确的实现单节点 Redis 锁。

[Kleppmann的帖子](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)
[Antirez（Redis开发者）的回复]http://antirez.com/news/101 回复了 Kleppmann。
[HackerNews上的后续讨论](https://news.ycombinator.com/item?id=11065933)

## 先介绍一下 Redlock

### 如何正确设置单节点的锁

要点如下
* 使用随机字符做签名，防止释放了别人的锁
* 一条指令内加锁同时设置释放时间 （lock validity time）

### Redlock
N个master。
1. 获取当前时间 （ms）
2. 顺序在N个master上加锁。在每个节点上，使用一个比总的自动释放时间要小的时间作为timeout。比如 auto-release time = 10s，那么每个节点上的 timeout 可以设为 5~50 ms。这可以防止当某个节点挂掉后，client 被阻塞的事件过长。
3. client 计算加锁花了多少时间。只有当在多数节点（至少3个）上加锁成功，且耗时小于 local validity time，才认为整体加锁成功。
4. 如果得到了锁，那么要从 validity time中把加锁的耗时减掉。
5. 如果加锁失败，尝试在所有节点上释放锁。
6. 如果加锁失败，需要等待一个随机时间后再尝试重新申请锁。

## Kleppmann的观点

Kleppmann认为的使用锁的原因
* Efficiency. 防止一些昂贵的操作执行多次。
* Correctness

两者都很重要。但在每个使用锁的场景，都要明确哪一个是该场景所要求的。

如果只是为了效率，那么没有必要使用 Redlock。因为起 Redis 集群的成本还是挺高的，不如用一个单实例 Redis 来搞定，最多做个主备。 

既然 Redlock 假设的场景使用了多个节点的集群，那么我们可以假设它是为了 correctness。那么Kleppmann认为在某些场景下，Redlock 是不安全的，可能会有2个 client 同时认为自己加锁成功。



