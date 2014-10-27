---
layout: post
title: "Creating uber JAR for Spark project using sbt-assembly"
date: 2014-04-08T09:47:00+05:30
comments: true
categories:
 - mergeStrategy in assembly sbt
 - Spark Scala
 - Spark sbt assembly
 - sbt
 - Spark assembly
 - apache spark tutorial
 - Apache Spark
 - Big Data Spark
 - How to make Spark Single Jar
 - Spark uber jar
 - Spark fat jar
 - Spark sbt 
---
In the previous post shared how to use sbt in Spark-streaming project. This post is about how to create a fat jar for spark streaming project using sbt plugin. sbt-assembly is a sbt plugin to create a fat JAR of sbt project with all of its dependencies.

Add sbt-assembly plugin in **_project/plugin.sbt_**
```scala
addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.9.1")
```

Specify sbt-assembly.git as a dependency in project/project/build.scala


```scala
import sbt._

object Plugins extends Build {
  lazy val root = Project("root", file(".")) dependsOn(
    uri("git://github.com/sbt/sbt-assembly.git#0.9.1")
  )
}
```
In build.sbt file add the following contents
```scala
import AssemblyKeys._ // put this at the top of the file,leave the next line blank

assemblySettings
```
Use full keys to configure the assembly plugin. For more details [refer](https://github.com/sbt/sbt-assembly)
```
target                        assembly-jar-name             test
assembly-option               main-class                    full-classpath
dependency-classpath          assembly-excluded-files       assembly-excluded-jars
```
If multiple files share the same relative path the default strategy is to verify that all candidates have the same contents and error out otherwise. This behavior can be configured for Spark projects using assembly-merge-strategy as follows.

```scala
mergeStrategy in assembly <<= (mergeStrategy in assembly) { (old) =>
  {
    case PathList("javax", "servlet", xs @ _*) => MergeStrategy.last
    case PathList("org", "apache", xs @ _*) => MergeStrategy.last
    case PathList("com", "esotericsoftware", xs @ _*) => MergeStrategy.last
    case "about.html" => MergeStrategy.rename
    case x => old(x)
  }
}
```
From the root folder run
```
sbt/sbt assembly
```
the assembly plugin then packs the class files and all the dependencies into a single JAR file: target/scala_2.10/TwitterPopularTags-assembly-0.3.0.jar.

You can find an example project from [here](https://github.com/prabeesh/SparkTwitterAnalysis)
