---
tags: ['study-notes', 'apache-spark']
title: 'Introduction to Big Data with Apache Spark'
---
[https://www.edx.org/course/introduction-big-data-apache-spark-uc-berkeleyx-cs100-1x](https://www.edx.org/course/introduction-big-data-apache-spark-uc-berkeleyx-cs100-1x)

## Spark and Semi Structured Data
- XML and Tabular data
- Panda DataFrame is alternative to R
- Dict (column name) -> Series (Column)
- Spark 1.3 introduced DataFrame
- Spark -> Pandas: spark_df.toPandas
- Pandas -> Spark: context.createDataFrame(pandas_sf)
- Scala is faster than Python for reading and writing files and binary files are much faster than text files

## Spark and Structured Data
- Structured data has schema
- SQL is supported by pySpark DataFrames
- SparkSQL support: inner, outer, left outer, right outer and semijoin.
- For pair RDD, spark supports: join, leftOuterJoin, rightOuterJoin, fullOuterJoin


**Links Provided:**

- [City of San Francisco online data][1]
- [City of San Francisco 3-1-1 report data][2]
- [Structured Open Urban Data: Understanding the Landscape][3] paper
- [Spark online documentation for DataFrames][4]
- [Spark DataFrame API][5]
- [Apache Common Log Format specification][6]
- Two month's worth of all HTTP requests to the NASA - Kennedy Space Center WWW server in Florida in 1995 are available online [here][7].

**Lab:**

- Analyze NASA log files
- takeOrdered

[1]: https://data.sfgov.org/
[2]: http://www.sf311.org/
[3]: http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4174913/pdf/big.2014.0020.pdf
[4]: https://spark.apache.org/docs/latest/sql-programming-guide.html
[5]: https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.DataFrame
[6]: http://httpd.apache.org/docs/2.4/logs.html#common
[7]: http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html
