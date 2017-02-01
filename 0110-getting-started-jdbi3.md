---
layout: default
title: Getting Started JDBI3
short_title: JDBI3
category: getting_started
module: jdbi3
description: SimpleFlatMapper java jdbi3 ResultSetMapper mapper deep object
---

# Getting Started JDBI3

{% include maven_dependency.md %}

## Init plugin
You can register the SfmJdbiPlugin

```java
Jdbi dbi = Jdbi.create(DbHelper.getHsqlDataSource());
dbi.installPlugins();
```

or 

```java
Jdbi dbi = Jdbi.create(DbHelper.getHsqlDataSource());
dbi.installPlugin(new SfmJdbiPlugin());
```

to register the Sfm RowMapperFactory.

