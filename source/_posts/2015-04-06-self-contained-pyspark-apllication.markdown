---
layout: post
title: "Self Contained PySpark Application"
date: 2015-04-06 23:09:01 +0530
comments: true
published: false
categories: 
---
[Previous post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/) mentions about installation of spark and Scala interactive shell etc. Actually Spark supports Scala, Java and Python. This post is going to check how to play Spark with Python. Like Scala iteractive shell there is interactive shell for Python, just run the following command from spark root folder 
```
./bin/pyspark
```  
this will give python interactive shell for spark. Enjoy Spark in Python also
###Stand alone PySpark Application 
One the [previous posts](/blog/2014/04/01/a-standalone-spark-application-in-scala/) mentions about stand alone Spark application in Scala. In this post going to introduce how to write stand alone Python application/self contained PySpark application. Don't forget to build Spark using sbt assembly before going to start. To build Spark [refer this post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/). 
Actually it is simple just add PySpark lib path in the system python path as follows
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
Now pyspark is avaible in system path. After writing Python run the code using python command then it run in local spark instance with default configurations. But usually for spark applications it is better to use the spark submit script. As an example 
```
./bin/spark-submit --master local[8] <python_file.py>
``` 
For more details about spark submit [refer](https://spark.apache.org/docs/latest/configuration.html). It is possible to pass configuration values at run time. otherwise set it up in the conf/spark-defaults.conf. The configured values in the conf/spark-defaults.conf also effected while you running the pyspark code simply using python command.  

Now you are thinking about why we don't have a pip install for pyspark. You can find the reason in this [jira ticket](https://issues.apache.org/jira/browse/SPARK-1267).   

If you are a fan of iPython then you have the option to run PySpark there refer this [blog post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/) for more detail.    
