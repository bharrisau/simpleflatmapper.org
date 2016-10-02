---
layout: default
title: Migrating to v3.
comments: true
---

# sfm module has been split into

* sfm-csv for the Csv related code, CsvParser, CsvMapper, CsvWritter.
* sfm-jdbc for the Jdbc related code, JdbcMapper, PreparedStatementMapper, Crud.

# the packages have been renamed

* org.sfm -> org.simpleflatmapper
* org.sfm.utils -> org.simpleflatmapper.util

# Joda time support

You know need to include the sfm-converter-joda-time module.



 