---
layout: default
title: Getting Started Excel spreadsheet
short_title: Excel
category: getting_started
module: poi
---
# Getting Started Excel POI

{% include maven_dependency.md %}

## Quick start

{% highlight java %}
final SheetMapper<DbObject> sheetMapper =
        SheetMapperFactory
                .newInstance()
                .newMapper(DbObject.class);

...

    try (InputStream is = new FileInputStream("file.xls");
            Workbook workbook = new HSSFWorkbook(is)){
        sheetMapper.stream(workbook.getSheetAt(0)).forEach(System.out::println);
    }
{% endhighlight %}
