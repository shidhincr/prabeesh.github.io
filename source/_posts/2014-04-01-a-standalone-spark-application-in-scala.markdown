---
layout: post
title: "A Standalone Spark Application in Scala"
date: 2014-04-01T22:56:00+05:30
comments: true
categories: [Apache Spark, SBT, Scala, BigData]
keywords: [spark streaming twitter example, spark eclipse plugin, apache spark tutorial, spark twitter streaming, scala spark, spark eclipse, apache spark example, apache spark scala, apache spark eclipse, spark stream, apache spark examples, spark standalone, spark twitter example, spark scala, spark tutorial apache, apache spark filter, apache spark streaming, apache spark project, apache spark tutorials, eclipse spark, spark in eclipse, apache spark eclipse plugin, sbt command line arguments, spark streaming, apache spark configuration, spark scala examples, apache spark github, spark standalone application, spark streaming example, eclipse sbt, spark streaming twitter, spark scala tutorial]
description: Spark Application in Scala, Building Spark Applications, Developing Spark Applications
---

Sharing  some ideas about how to create a Spark-streaming stand-alone application and how to run the Spark applications in scala-SDK (Eclipse IDE). 
## Building Spark Application using SBT 
A Standalone application in Scala using Apache Spark API. The application is build using Simple Build Tool(SBT). 

For  creating a stand alone app take the twitter popular tag [example](https://github.com/apache/spark/blob/branch-0.9/examples/src/main/scala/org/apache/spark/streaming/examples/TwitterPopularTags.scala)

This program calculates popular hashtags (popular topics) over sliding 10 and 60 second windows from a Twitter stream. The stream is instantiated with credentials and optionally filters supplied by the command line arguments.

But here modified the code for talking twitter authentication credentials through command line argument. So it needs to give the arguments as <master> <consumerKey> <consumerSecret> <accessToken> <accessTokenSecret> <filters>.
```Scala
// Twitter Authentication credentials  
System.setProperty("twitter4j.oauth.consumerKey", args(1))  
System.setProperty("twitter4j.oauth.consumerSecret", args(2))  
System.setProperty("twitter4j.oauth.accessToken", args(3))  
System.setProperty("twitter4j.oauth.accessTokenSecret", args(4))  
``` 
If you want to read twitter authentication credential from file, refer this [link](https://github.com/pwendell/spark-twitter-collection/blob/master/TwitterUtils.scala)

The sbt configuration file. For more detail about sbt [refer](http://www.scala-sbt.org/release/docs/Getting-Started/Setup.html)
```Scala
name := "TwitterPopularTags" 

version := "0.1.0" 

scalaVersion := "2.10.3" 

libraryDependencies ++= Seq("org.apache.spark" %% 
"spark-core" % "0.9.0-incubating", 
"org.apache.spark" %% "spark-streaming" % "0.9.0-incubating", 
"org.apache.spark" %% "spark-streaming-twitter" % "0.9.0-incubating")

resolvers += "Akka Repository" at "http://repo.akka.io/releases/"
```
You can find the project from [here](https://github.com/prabeesh/SparkTwitterAnalysis/tree/0.1.0)
##Spark programming in Eclipse
Using sbt eclipse plugin, sbt project can run on Eclipse IDE.  For more details find [here](https://github.com/typesafehub/sbteclipse)
```Scala
addSbtPlugin("com.typesafe.sbteclipse" % "sbteclipse-plugin" % "2.1.0")
```
then run from root folder of the project
```
sbt/sbt eclipse
```
This command  creates a project compatible with Eclipse. Upon opening the eclipse IDE this project can now be imported and the executed with spark.

You can find the sbt eclipse project from [here](https://github.com/prabeesh/SparkTwitterAnalysis/tree/0.2.0)

To avoid generating eclipse source entries for the java directories and put all libs in the lib_managed directory, that way we can distribute eclipse project files, for this - add the contents to build.sbt
```Scala
/*put all libs in the lib_managed directory, 
that way we can distribute eclipse project files
*/

retrieveManaged := true

EclipseKeys.relativizeLibs := true

// Avoid generating eclipse source entries for the java directories

(unmanagedSourceDirectories in Compile) <<= (scalaSource in Compile)(Seq(_))

(unmanagedSourceDirectories in Test) <<= (scalaSource in Test)(Seq(_))  
```
