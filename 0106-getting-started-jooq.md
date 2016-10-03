---
layout: default
title: Getting Started jOOQ
short_title: jOOQ
category: getting_started
module: jooq
---

{% include maven_dependency.md %}

There are 2 mapping strategies available in jOOQ.

* the generated classes from the db information. You will get a record that will have named getters matching the column names.
* the fetchInto(Class) method that will call the jOOQ mapper or a third party mapper specified in the configuration.

because fetchInto has to go through the Record creation, its use will mainly be when your query does not map to an generated object - ie sub set of field, joins -.

# SFM as a RecordMapperProvider

Sfm can be plugged into the fetchInto mapping. 

All you need to do is 

{% highlight java %}
configuration.set(new SfmRecordMapperProvider()));
{% endhighlight %}

when instantiating your DSL. You will then be able use fetchInto with a cost very close to fetching the record - see the performance section - and the flexibility that SFM offers.

# SFM on the ResultSet

Because the RecordMapperProvider works on the record that we don't need we are not as performant as working directly with the ResultSet. Fortunately jOOQ allows you to fetch the ResultSet directly avoiding the cost of the transition form ResultSet to Record.

{% highlight java %}
JdbcMapper mapper = JdbcMapperFactory.newInstance().newMapper(MyObject.class);

ResultQuery<MyRecord> query = dsl.select().from(TABLE);
try (ResultSet rs = query.fetchResultSet()) {
    mapper.stream(rs).forEach(System.out::println);
}
{% endhighlight %}

That will allow you to get the query generation power of jOOQ and the close to pure Jdbc performance of SimpleFlatMapper.
