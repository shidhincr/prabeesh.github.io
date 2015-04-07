---
layout: post
title: "Self Contained PySpark Application"
date: 2015-04-07 21:05:30 +0530
comments: true
categories: [Apache Spark, PySpark, Python]
keywords: [stand alone pyspark application, python spark example, beginners guide to pyspark, pyspark spark example, apllications in pyspark]
description: This post talking about how set up the pyspark single application  
---
In my [previous post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/) I wrote about installation of Spark, Scala interactive shell etc. This post will talk about doing same in Python. Like Scala iteractive shell there is interactive shell for Python. To activate the same run the following command from spark root folder 
```
./bin/pyspark
```  
this will give Python interactive shell for spark. Enjoy Spark using Python

For experimentation and development the above mentioned shell will do, but once the code is moved to production we are talking about a stand alone application. In one the my [previous posts](/blog/2014/04/01/a-standalone-spark-application-in-scala/) I have talked about stand alone Spark application in Scala. Here the same is in Python application, as mentioned in the [Spark official site](https://spark.apache.org/docs/latest/quick-start.html#self-contained-applications) we can call it a self contained PySpark application. To build Spark using sby assembly [refer this post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/). Begin by adding Pyspark lib in system Python path as follows
```
cd ~
vi .bashrc
```
then add following two path export in end of bashrc file 
```
export SPARK_HOME=<path to Spark home>
export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
```
don't forget to export the SPARK_HOME, then as usual restart bash
```
. .bashrc
```
PySpark depends the py4j Python package. It helps Python interpreter to dynamically access the Spark object from the JVM, install py4j python package using following comand.    
```
pip install py4j
```
Now PySpark is avaible in system path. After writing our Python, one can simply run the code using python command then it runs in local Spark instance with default configurations. For Spark applications it is better to use the spark submit script. 
```
./bin/spark-submit --master local[8] <python_file.py>
``` 
For more details about spark submit [refer here](https://spark.apache.org/docs/latest/configuration.html). From the site we can observe that configuration values can be passed at run time. It can also be changed in the conf/spark-defaults.conf file. After configuring spark one needs to run it using the python command, for the changes to get reflected.   

Now you are thinking about why we don't have a pip install for pyspark. You can find the reason in this [jira ticket](https://issues.apache.org/jira/browse/SPARK-1267).   

If you are a fan of iPython then you have the option to run PySpark there as well refer this [blog post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/) for more detail.    

