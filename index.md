---
layout: default
description: SimpleFlatMapper java library fast and simple mapping, micro orm, csv parser, csv mapper
---


{% assign post = site.posts.first %}
SimpleFlatMapper [V{{ site.libraryVersion }}]({{ post.url }}) provides a very fast and easy to use mapper for

 * [Jdbc, aka micro ORM](0102-getting-started-jdbc.html) from ResultSet to PreparedStatement
 * [Csv Mapper](0101-getting-started-csv.html#mapping-a-csv-to-an-object) with its own [Csv Parser](reading-a-csv-file) 
 * [Excel spreadsheet](0105-getting-started-poi.html)
 * [Cassandra Datastax](0103-getting-started-datastax.html)
 
It integrates with 
 * [jOOQ](0106-getting-started-jooq.html)
 * [Spring Jdbc](0104-getting-started-springjdbc.html)
 * [JDBI ResultSetMapper and Binder](0109-getting-started-jdbi.html)
 * [Sql2o](0108-getting-started-sql2o.html)
 * [QueryDSL](0107-getting-started-querydsl.html)
 
The mapper [supports](0201-property-mapping.html)   
 * Constructor, Setter and Public field injection
 * [Builder Pattern](0201-property-mapping.html#builder-pattern) - like [Immutables](http://immutables.github.io/) -
 * Deep object structure
 * Tuples including [jOOL](https://github.com/jOOQ/jOOL) tuples and [Fasttuple](https://github.com/boundary/fasttuple)
 * List, Array and Map
 
No annotation, no configuration needed. 
Default behavior can be changed programmatically.
You can also extends the type mapping by providing [converters](0202-converters.html)

The csv module also provides one of the [fastest java csv parser](12-csv-performance.html).

It can all run on java 6, 7, 8 and 9.

Some sample code :

# Csv Mapper
{% highlight java %}
CsvParser
    .mapTo(MyObject.class)
    .stream(reader)
    .forEach(System.out::println);
{% endhighlight %}

# Jdbc Mapper
{% highlight java %}
JdbcMapper<MyObject> mapper =
    JdbcMapperFactory.newInstance().newMapper(MyObject.class);

public void findAll(Consumer<MyObject> consumer) throws SQLException {
    try (Connection conn = getConnection();
        PreparedStatement ps = 
            conn.prepareStatement("select * from my_table");
        ResultSet rs = ps.executeQuery();) {
        return mapper.forEach(rs, consumer);
    }
}
{% endhighlight %}






 