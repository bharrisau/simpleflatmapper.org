---
layout: default
title: Getting Started Csv
short_title: Csv
category: getting_started
module: csv
---

{% include maven_dependency.md %}

# Reading a csv file

The CsvParser api allows you to read from a File, a Reader or a CharSequence
via a [RowHandler](http://static.javadoc.io/org.simpleflatmapper/sfm-util/{% include currentversion.html %}/index.html?org/simpleflatmapper/util/RowHandler.html) callback, 
a Iterator or a Stream of String[]

{% highlight java%}
// Callback
CsvParser
    .forEach(file, consumer);
    
// Iterator
try (CloseableIterator<String[]> it = CsvParser.iterator(file)) {
    while(it.hasNext()) {
        consumer.consumer(it.next());
    }
}

// Stream
try (Stream<String[]> stream = CsvParser.stream(file)) {
    stream.forEach(consumer);
}
{% endhighlight %}

# Mapping a csv to an object

You can also ask the row to be map to an object. You can then read the csv from a File, a Reader 
or a CharSequence via a [RowHandler](http://static.javadoc.io/org.simpleflatmapper/sfm-util/{% include currentversion.html %}/index.html?org/simpleflatmapper/util/RowHandler.html) callback, 
a Iterator or a Stream of your type.

{% highlight java%}
// Callback
CsvParser
    .mapTo(MyObject.class)
    .forEach(file, consumer);
    
// Iterator
try (CloseableIterator<String[]> it = 
        CsvParser.mapTo(MyObject.class).iterator(file)) {
    while(it.hasNext()) {
        consumer.consumer(it.next());
    }
}

// Stream
try (Stream<String[]> stream = 
        CsvParser.mapTo(MyObject.class).stream(file)) {
    stream.forEach(consumer);
}
{% endhighlight %}


# Writing a csv from an object
