---
layout: default
title: Google Protocol Buffers
short_title: Google Protocol Buffers
category: docs
description: SimpleFlatMapper java mapping to Google Protocol Buffers
---

Since version [3.12](/2017/06/09/v3.12.html) SimpleFlatMapper can map to Google Protocol Buffers objects.

All you need to do is add sfm-converter-protobuf to your dependencies, to be able to instantiate `com.google.protobuf.Timestamp`.

```xml
    <dependency>
        <groupId>org.simpleflatmapper</groupId>
        <artifactId>sfm-converter-protobuf</artifactId>
        <version>{% include currentversion.html %}</version>
    </dependency>
```
see [sfm-test-proto](https://github.com/arnaudroger/SimpleFlatMapper/tree/master/sfm-test-proto) for running code.

Not all configuration have been tested so if you encounter a problem please raise an [issue](https://github.com/arnaudroger/SimpleFlatMapper/issues/new).