
[![Maven Central](https://img.shields.io/maven-central/v/org.simpleflatmapper/sfm-{{page.module}}.svg)](http://search.maven.org/#artifactdetails%7Corg.simpleflatmapper%7Csfm-{{page.module}}%7C{% include currentversion.html %}%7C)
[![JavaDoc](https://img.shields.io/badge/javadoc-{{ site.libraryVersion }}-blue.svg)](http://www.javadoc.io/doc/org.simpleflatmapper/sfm-{{page.module}})

## Setting up the environment 

Add the [Dependency](http://search.maven.org/#artifactdetails%7Corg.simpleflatmapper%7Csfm-{{page.module}}%7C{% include currentversion.html %}%7C) to your build.
 
for Maven :

### Java 8
{% highlight xml %}
<dependency>
    <groupId>org.simpleflatmapper</groupId>
    <artifactId>sfm-{{page.module}}</artifactId>
    <version>{% include currentversion.html %}</version>
</dependency>
{% endhighlight %}

### Java 6, 7

{% highlight xml %}
<dependency>
    <groupId>org.simpleflatmapper</groupId>
    <artifactId>sfm-{{page.module}}</artifactId>
    <version>{% include currentversion.html %}</version>
    <classifier>jdk16</classifier>
</dependency>
{% endhighlight %}

### Java 9

Version 3.1 is not yet published, the maven compiler plugin is not compatible with last 140 version.
 
{% highlight xml %}
<dependency>
    <groupId>org.simpleflatmapper</groupId>
    <artifactId>sfm-{{page.module}}</artifactId>
    <version>3.0</version>
    <classifier>jdk9ea</classifier>
</dependency>
{% endhighlight %}