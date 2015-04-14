---
layout: post
title: "Self Contained PySpark Application"
date: 2015-04-07 21:05:30 +0530
comments: true
categories: [Apache Spark, PySpark, Python]
keywords: [stand alone pyspark application, python spark example, beginners guide to pyspark, pyspark spark example, apllications in pyspark]
description: This post talking about how set up the pyspark single application  
---
In my [previous post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/), I wrote about installation of Spark and Scala interactive shell. Here in this post we'll see how to do the same in Python. 

Similar to Scala iteractive shell, there is an interactive shell available for Python. You can run it with the below command from spark root folder:
```
./bin/pyspark
```  
Now you can enjoy Spark using Python interactive shell.

This shell might be sufficient for experimentations and developments. However, for production level, we should use a stand alone application. I talked about a stand alone Spark application in Scala in one of my previous [post](/blog/2014/04/01/a-standalone-spark-application-in-scala/). Here comes the same written in Python -- you can find more about it in [Spark official site](https://spark.apache.org/docs/latest/quick-start.html#self-contained-applications) -- and known as a self contained PySpark application. 

First, [refer this post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/) to build Spark using sby assembly. Add Pyspark lib in system Python path as follows:
```
cd ~
vi .bashrc
```
Add the following exports in end of bashrc file 
```
export SPARK_HOME=<path to Spark home>
export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
```
Don't forget to export the SPARK_HOME. Restart `BASH` once it is done.
```
. .bashrc
```
PySpark depends on the `py4j` Python package. It helps Python interpreter to dynamically access the Spark object from the JVM.Install py4j python package using following comand:   
```
pip install py4j
```
PySpark should be avaible in system path by now. After writing the Python code, one can simply run the code using python command then it runs in local Spark instance with default configurations. For Spark applications, it is better to use the spark submit script. 
```
./bin/spark-submit --master local[8] <python_file.py>
``` 
For more details about spark submit [refer here](https://spark.apache.org/docs/latest/configuration.html). From the site we can observe that the configuration values can be passed at run time. It can also be changed in the conf/spark-defaults.conf file. After configuring spark, one needs to run it using the python command to see the changes reflected.

The reason for why there is no `pip install` for pyspark can be found in this [jira ticket](https://issues.apache.org/jira/browse/SPARK-1267).

If you are a fan of iPython, then you have the option to run PySpark. Refer this [blog post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/) for more detail.    

