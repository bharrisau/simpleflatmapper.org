---
layout: default
---

SimpleFlatMapper provides a very fast and easy to use mapper for

 * [Jdbc, aka micro ORM](0102-getting-started-jdbc.html)
 * [Csv](0101-getting-started-csv.html), [Excel spreadsheet](0105-getting-started-poi.html)
 * [Cassandra Datastax](0103-getting-started-datastax.html)
 
It integrates with 
 * [jOOQ](0106-getting-started-jooq.html)
 * [Spring Jdbc](0104-getting-started-springjdbc.html)
 * [Sql2o](0108-getting-started-sql2o.html)
 * [QueryDSL](0107-getting-started-querydsl.html)
 
The mapper [supports](0201-property-mapping.html)   
 * Constructor injection
 * Setter injection
 * Public Field injection
 * [Builder Pattern](0201-property-mapping.html#builder-pattern) - like [Immutables](http://immutables.github.io/) -
 * Deep object structure
 * Tuples] including [jOOL](https://github.com/jOOQ/jOOL) tuples ans [Fasttuple](https://github.com/boundary/fasttuple)
 * List, Array and Map
 
No annotation, no configuration needed. 
Default behavior can be changed programmatically.
You can also extends the type mapping by providing converters

The csv module also provides one of the [fastest java csv parser](https://github.com/arnaudroger/SimpleFlatMapper/wiki/Csv-Performance).

It can all run on java 6, 7, 8 and 9.

Some sample code :

# Jdbc
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

# Csv
{% highlight java %}
CsvParser
    .mapTo(MyObject.class)
    .stream(reader)
    .forEach(System.out::println);
{% endhighlight %}





 