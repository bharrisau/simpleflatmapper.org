---
layout: default
title: Getting Started QueryDsl
short_title: QueryDsl
category: getting_started
module: querydsl
description: SimpleFlatMapper java querydsl projection
---
# Getting Started QueryDsl

{% include maven_dependency.md %}

{% highlight java %}
SQLQuery sqlquery = new SQLQuery(conn, new HSQLDBTemplates());
 List<DbObject> list = 
    sqlquery
        .from(qTestDbObject)
        .where(qTestDbObject.id.eq(1l))
        .list(
            new QueryDslMappingProjection<DbObject>(
                DbObject.class, 
                qTestDbObject.id,
                qTestDbObject.name, 
                qTestDbObject.email, 
                qTestDbObject.creationTime, 
                qTestDbObject.typeName, 
                qTestDbObject.typeOrdinal));
     
{% endhighlight %}