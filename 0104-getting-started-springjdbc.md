---
layout: default
title: Getting Started Spring Jdbc
short_title: Spring Jdbc
category: getting_started
module: springjdbc
description: SimpleFlatMapper java generic RowMapper deep object
---
# Getting Started Spring jdbc

{% include maven_dependency.md %}

# Why Not BeanPropertyRowMapper?

First, the performance of BeanPropertyRowMapper is [abysmal](https://github.com/arnaudroger/SimpleFlatMapper/wiki/Jdbc-Performance-Local-Mysql), as it says in the [doc](http://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/core/BeanPropertyRowMapper.html)
it's not made for that. This module offers performance very close to a manually written RowMapper - it could even be faster as 
name access to a column is more expensive than by index.

Second SimpleFlatMapper support constructor injection, factory method, deep object etc...

Third, it also supports SqlParameterSource, and Crud operations.

You might also have a look at [Spring-JDBC-ROMA](http://serkan-ozal.github.io/spring-jdbc-roma/) that also creates
RowMapper.

# RowMapper

{% highlight java %}
class MyDao {
    private final RowMapper<DbObject> rowMapper =
        JdbcTemplateMapperFactory.newInstance().newRowMapper(DbObject.class);
        
    public List<DbObject> findAll() {
        return template.query(DbHelper.TEST_DB_OBJECT_QUERY, rowMapper);
    }
}
{% endhighlight %}

# SqlParameterSource

{% highlight java %}
class MyDao {
    private final SqlParameterSourceFactory<DbObject> parameterSourceFactory =
        JdbcTemplateMapperFactory
            .newInstance()
            .newSqlParameterSourceFactory(DbObject.class);

    public void insertObject(DbObject object) {
        template.update(
            "INSERT INTO DBOBJECTS(id, name, email)"
            + " VALUES(:id, :name, :email)",
            parameterSourceFactory.newSqlParameterSource(object));

    }

    public void insertObjects(Collection<DbObject> objects) {
        template.batchUpdate(
            "INSERT INTO DBOBJECTS(id, name, email)"
            + "VALUES(:id, :name, :email)",
            parameterSourceFactory.newSqlParameterSources(objects));
    }
}
{% endhighlight %}

# Crud

{% highlight java %}
class MyDao {

    JdbcTemplateCrud<DbObject, Long> objectCrud;

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        objectCrud =
            JdbcTemplateMapperFactory
                .newInstance()
                .<DbObject, Long>crud(DbObject.class, Long.class)
                .to(template, "TEST_DB_OBJECT");
    }

    public void insertObject(DbObject object) {
        crud.create(object);
    }

    public void insertObjects(Collection<DbObject> objects) {
        crud.create(objects);
    }
}
{% endhighlight %}

# More examples

See [JdbcTemplateMapperFactoryTest](https://github.com/arnaudroger/SimpleFlatMapper/blob/master/sfm-springjdbc/src/test/java/org/simpleflatmapper/jdbc/spring/test/JdbcTemplateMapperFactoryTest.java) for more examples.
