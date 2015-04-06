---
layout: post
title: "Self Contained PySpark Apllication"
date: 2015-04-06 23:09:01 +0530
comments: true
published: false
categories: 
---
In [previous post](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/) mentioned about installation of spark and only taking about Scala, Scala interactive shell etc. Now just moving to Python. Like Scala iteractive shell there is interactive shell for Python, just run the following command from spark root folder 
```
./bin/pyspark
```  
this will give python interactive shell for spark. Enjoy  Spark in Python also

For starting interactive shell fine for us. In production level we should need stand alone application. One the [previous](/blog/2014/04/01/a-standalone-spark-application-in-scala/) posts is talking about stand alone Spark application in Scala. Here we can check how to we can write stand alone Python application or with reference to  [Spark official](https://spark.apache.org/docs/latest/quick-start.html#self-contained-applications) site we can call it as self contained PySpark application. For you should build spark using sbt assembly to build Spark [refer](/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/). Actually it is simple just add PySpark classes in the system python path as follows
```
cd ~
vi .bashrc
```
the add 
```
export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
```
don't forget to export the SPARK_HOME, then as usual restart bash
```
. .bashrc
```
Now we can import pyspark in our python code. After writing your Python code you simple run using python command then it run in local spark instance with default configurations. But usually for spark applications it is better to use the spark submit script 
```
./bin/spark-submit --master local[8] <python_file.py>
``` 
For more details about spark submit [refer](https://spark.apache.org/docs/latest/configuration.html). From here you also find the we can pass configuration values at run time. otherwise we can set it up in the conf/spark-defaults.conf. 

Now you are thinking about why we don't have a pip install for pyspark. You can find the reason in this [jira ticket](https://issues.apache.org/jira/browse/SPARK-1267).   

If you are fan of iPython then you have the option to run PySpark there refer this [blog post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/) for more detail.    
