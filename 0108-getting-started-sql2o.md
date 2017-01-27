---
layout: default
title: Getting Started Sql2o
short_title: Sql2o
category: getting_started
module: sql2o
description: SimpleFlatMapper java sql2 ResultSetHandler mapper deep object
---
# Getting Started Sql2o

{% include maven_dependency.md %}


## SQL2o integration

{% highlight java %}
Query query = sql2o.open().createQuery("select * from table");
query.setAutoDeriveColumnNames(true);
query.setResultSetHandlerFactoryBuilder(new SfmResultSetHandlerFactoryBuilder());

List<DbObject> dbObjects = query.executeAndFetch(DbObject.class);
{% endhighlight %}