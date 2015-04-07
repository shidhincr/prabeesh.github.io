---
layout: post
title: "Self Contained PySpark Apllication"
date: 2015-04-06 23:09:01 +0530
comments: true
published: false
categories: 
---
In the [previous post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/) mentioned about installation of spark and Scala interactive shell etc. Actually Spark supports Scala, Java and Python. Here going to check how to play Spark with Python. Like Scala iteractive shell there is interactive shell for Python, just run the following command from spark root folder 
```
./bin/pyspark
```  
this will give python interactive shell for spark. Enjoy Spark in Python also

For starting interactive shell is fine. In production level should need stand alone application. One the [previous](/blog/2014/04/01/a-standalone-spark-application-in-scala/) posts is talking about stand alone Spark application in Scala. In this post going to introduce how to write stand alone Python application or with reference to  [Spark official](https://spark.apache.org/docs/latest/quick-start.html#self-contained-applications) site also call it as self contained PySpark application. Should build spark using sbt assembly before going to start, to build Spark [refer](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/). Actually it is simple just add PySpark lib path in the system python path as follows
```
cd ~
vi .bashrc
```
then add following two path export in end of bashrc file 
```
export SPARK_HOME=<path to your Spark home>
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

If you are fan of iPython then you have the option to run PySpark there refer this [blog post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/) for more detail.    
