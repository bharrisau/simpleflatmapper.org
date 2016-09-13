# Setting up the environment 

Add the [Dependency](http://search.maven.org/#artifactdetails%7Corg.simpleflatmapper%7Csfm-{{page.module}}%7C{% include currentversion.html %}%7C) to your build.
 
for Maven :

## Java 8
{% highlight xml %}
<dependency>
    <groupId>org.simpleflatmapper</groupId>
    <artifactId>sfm-{{page.module}}</artifactId>
    <version>{% include currentversion.html %}</version>
</dependency>
{% endhighlight %}

## Java 6, 7

{% highlight xml %}
<dependency>
    <groupId>org.simpleflatmapper</groupId>
    <artifactId>sfm-{{page.module}}</artifactId>
    <version>{% include currentversion.html %}</version>
    <classifier>jdk16</classifier>
</dependency>
{% endhighlight %}