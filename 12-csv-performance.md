---
layout: default
title: Peformance comparaison
---

[Raw Data](https://github.com/arnaudroger/mapping-benchmark/blob/master/sfm-csv/jmh-result-3.5.csv)
[Benchmark Code](https://github.com/arnaudroger/mapping-benchmark/blob/master/sfm-csv)


The score are time in ms to parse the file, the lower the better. 
Univocity is the benchmark with readInputOnSeparateThread set to false, 
ConcurrentUnivocity has that flag set to true. 
All the parallel test appart from ConcurrentUnivocity uses a [ParallelReader](https://github.com/arnaudroger/SimpleFlatMapper/blob/master/sfm-util/src/main/java/org/simpleflatmapper/util/ParallelReader.java).

Why only those 3? because the other that I tested are pretty slow in compaison. If you think your csv parser is worth benchmark [Open an issue](https://github.com/arnaudroger/mapping-benchmark/issues/new).

# Parsing a unescaped [Csv](http://www.maxmind.com/download/worldcities/worldcitiespop.txt.gz)

| Parser        | avgt | 90th | 95th | 99th | 
| ------------- | ----:| -----:| -----:| -----:|
| Jackson       | 1237 | 1281  |  1300 |  1346 |
| Sfm           | 854  | 858   | 859   | 865   |
| Univocity     | 958  | 969   | 974   | 994   |

![Parce csv no quotes](/assets/perf/3.5/no_quotes.png)

# Parsing a escaped version of [Csv](http://www.maxmind.com/download/worldcities/worldcitiespop.txt.gz)

| Parser        | avgt | 90th | 95th | 99th | 
| ------------- | ----:| -----:| -----:| -----:|
| Jackson       | 1490 | 1726 | 1778 | 1810 |
| Sfm           |1267 | 1502 | 1538 | 1550 |
| Univocity     |1846 | 1883 | 1906 | 1963 |

![Parce csv with quotes](/assets/perf/3.5/quotes.png)

# Parsing a unescaped [Csv](http://www.maxmind.com/download/worldcities/worldcitiespop.txt.gz) with [ParallelReader](https://github.com/arnaudroger/SimpleFlatMapper/blob/master/sfm-util/src/main/java/org/simpleflatmapper/util/ParallelReader.java)

ConcurrentUnivocity uses readInputOnSeparateThread set to true and no ParallelReader.

| Parser        | avgt | 90th | 95th | 99th | 
| ------------- | ----:| -----:| -----:| -----:|
| Jackson       | 1360 | 1545 | 1589 | 1875 |
| Sfm           |749 | 825 | 891 | 999 |
| Univocity     |852 | 895 | 965 | 1097 |
| ConcurrentUnivocity     |795 | 806 | 813 | 849 |

![Parce csv, Parallel reader, no quotes](/assets/perf/3.5/par_noquotes.png)

# Parsing a escaped version of [Csv](http://www.maxmind.com/download/worldcities/worldcitiespop.txt.gz) with [ParallelReader](https://github.com/arnaudroger/SimpleFlatMapper/blob/master/sfm-util/src/main/java/org/simpleflatmapper/util/ParallelReader.java)

ConcurrentUnivocity uses readInputOnSeparateThread set to true and no ParallelReader.

| Parser        | avgt | 90th | 95th | 99th | 
| ------------- | ----:| -----:| -----:| -----:|
| Jackson       | 1368 | 1493 | 1560 | 1699
| Sfm           |951 | 1048 | 1109 | 1230
| Univocity     |1378 | 1480 | 1545 | 1828
| ConcurrentUnivocity     |1302 | 1330 | 1365 | 1589

![Parce csv, Parallel reader, with quotes](/assets/perf/3.5/par_quotes.png)

# Summary

Sfm is wining on all measures appart from the 90th percentile on unescaped parallel - That is likely link to the implementation of the ParallelReader.
The Sfm non parallel escaped reading is even faster than the ConcurrentUnivocity. and only 60ms behind on the non escaped content - might not worth wasting a cpu.

Jackson is better than Univocity on escaped content, Univocity is better than Jackson on unescaped.
For some reason the advantages that Jackson possesses disappear in the parallel treatment.