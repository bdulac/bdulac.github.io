--- 
layout: post 
title: Compile-time checking in Java
categories:
  - Software quality
  - Software engineering
  - Java
  - Programming
  - Practice
---
<p>
In my <a href="../note/apple-ssl-case">latest post</a> I wrote about code quality: in a few words, I believe in <a href="http://en.wikipedia.org/wiki/Static_program_analysis">static-checking</a>. Static means without executing the program. In a software process point of view, this would imply before runtime, in other words at compile-time. For a developer, it can be very useful to have such a verification simply with a compilation, without executing a specific tool (by the way, some very interesting software are available, just <a href="http://findbugs.sourceforge.net/">Findbugs</a> for example).
</p>
<p>
Here is the point: how would it be possible to proceed that kind of control without rewriting a compiler from scratch ?
</p>
<p>
The <a href="../java/">Java</a> platform provides a very interesting feature to perform such operations: <a href="http://docs.oracle.com/javase/tutorial/java/annotations/">annotations</a> (<a href="https://www.jcp.org/en/jsr/detail?id=175">JSR 175</a>). These are metadata <a href="http://docs.oracle.com/javase/tutorial/java/annotations/declaring.html">defined as java types</a>. Annotations have been introduced in the Java language starting with Java SE 5. Annotations can be processed at compile-time or runtime. 
</p>
<p>
@see https://blogs.oracle.com/java-platform-group/entry/java_8_s_new_type
</p>
<p>
The Sun Java SE distribution provided from the starting point a facility for annotation processing at compile-time called <a href="http://docs.oracle.com/javase/1.5.0/docs/guide/apt/">APT</a> (for Annotation Processing Tool). This was a vendor-specific feature (in <em>Sun</em> packages).
</p>
<p>
Since Java 6, that function is part of the platform with <a href="https://www.jcp.org/en/jsr/detail?id=269">JSR 269</a> (<em><a href="http://docs.oracle.com/javase/6/docs/api/javax/annotation/processing/package-summary.html">javax.annotation.processing</a></em> package, reference implementation part of the <a href="https://jcp.org/aboutJava/communityprocess/mrel/jsr269/index2.html">Java SE</a> distribution). With Java SE 8, the historical APT packaging <a href="http://openjdk.java.net/jeps/117">is removed</a> (after <a href="docs.oracle.com/javase/7/docs/technotes/guides/apt/">deprecation in Java SE 7</a>).
</p>
@see http://kerebus.com/2011/02/using-java-6-processors-in-eclipse/
