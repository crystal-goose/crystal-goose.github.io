---
layout: post
title: 学习一下spark的release candidate vote
---

收到Spark 2.3.1(RC1)的vote mail，学习一下内容和排版

* 邮件不加称呼，直奔主题
* 限宽大约80个英文字符
* 链接单独起一行，顶格

===========================
加重的段落标题，上下各一行等号
===========================


Please vote on releasing the following candidate as Apache Spark version 2.3.1.

The vote is open until Friday, May 18, at 21:00 UTC and passes if
a majority of at least 3 +1 PMC votes are cast.

[ ] +1 Release this package as Apache Spark 2.3.1
[ ] -1 Do not release this package because ...

To learn more about Apache Spark, please see http://spark.apache.org/

The tag to be voted on is v2.3.1-rc1 (commit cc93bc95):
https://github.com/apache/spark/tree/v2.3.0-rc1

The release files, including signatures, digests, etc. can be found at:
https://dist.apache.org/repos/dist/dev/spark/v2.3.1-rc1-bin/

Signatures used for Spark RCs can be found in this file:
https://dist.apache.org/repos/dist/dev/spark/KEYS

The staging repository for this release can be found at:
https://repository.apache.org/content/repositories/orgapachespark-1269/

The documentation corresponding to this release can be found at:
https://dist.apache.org/repos/dist/dev/spark/v2.3.1-rc1-docs/

The list of bug fixes going into 2.3.1 can be found at the following URL:
https://issues.apache.org/jira/projects/SPARK/versions/12342432

FAQ

=========================
How can I help test this release?
=========================

If you are a Spark user, you can help us test this release by taking
an existing Spark workload and running on this release candidate, then
reporting any regressions.

If you're working in PySpark you can set up a virtual env and install
the current RC and see if anything important breaks, in the Java/Scala
you can add the staging repository to your projects resolvers and test
with the RC (make sure to clean up the artifact cache before/after so
you don't end up building with a out of date RC going forward).

===========================================
What should happen to JIRA tickets still targeting 2.3.1?
===========================================

The current list of open tickets targeted at 2.3.1 can be found at:
https://s.apache.org/Q3Uo

Committers should look at those and triage. Extremely important bug
fixes, documentation, and API tweaks that impact compatibility should
be worked on immediately. Everything else please retarget to an
appropriate release.

==================
But my bug isn't fixed?
==================

In order to make timely releases, we will typically not hold the
release unless the bug in question is a regression from the previous
release. That being said, if there is something which is a regression
that has not been correctly targeted please ping me or a committer to
help target the issue.