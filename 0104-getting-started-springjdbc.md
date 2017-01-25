---
layout: default
title: Getting Started Spring Jdbc
short_title: Spring Jdbc
category: getting_started
module: springjdbc
---
# Getting Started Spring jdbc

{% include maven_dependency.md %}

## Create RowMapper

See [JdbcTemplateMapperFactoryTest](https://github.com/arnaudroger/SimpleFlatMapper/blob/master/sfm-springjdbc/src/test/java/org/simpleflatmapper/jdbc/spring/test/JdbcTemplateMapperFactoryTest.java) for more examples.

{% highlight java %}
class MyDao {
	private final RowMapper<DbObject> rowMapper =
		JdbcTemplateMapperFactory.newInstance().newRowMapper(DbObject.class);
		
	private final ResultSetExtractorImpl<List<DbObject>> resultSetExtractor = 
	    JdbcTemplateMapperFactory.newInstance().newResultSetExtractor(DbObject.class);

    // row mapper
	public void doSomething() {
		List<DbObject> results = template.query(DbHelper.TEST_DB_OBJECT_QUERY, rowMapper);
	}

    // result set extractor with consumer
	public void doSomethingElse() {
		 template
		 	.query(TEST_DB_OBJECT_QUERY,
		 		parameterGetterMap.newResultSetExtractor((o) -> System.out.println(o.toString())));
	}
}
{% endhighlight %}

## SqlParameterSource

{% highlight java %}
class MyDao {
	private final SqlParameterSourceFactory<DbObject> parameterSourceFactory =
		JdbcTemplateMapperFactory.newInstance().newSqlParameterSourceFactory(DbObject.class);

	public void insertObject(DbObject object) {
        template.update(
            "INSERT INTO DBOBJECTS(id, name, email) VALUES(:id, :name, :email)",
            parameterSourceFactory.newSqlParameterSource(object));

	}

	public void insertObjects(Collection<DbObject> objects) {
        template.batchUpdate(
            "INSERT INTO DBOBJECTS(id, name, email) VALUES(:id, :name, :email)",
            parameterSourceFactory.newSqlParameterSources(objects));
	}
}
{% endhighlight %}

## Crud

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