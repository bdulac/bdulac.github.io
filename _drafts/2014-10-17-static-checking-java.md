--- 
layout: post 
title: Static-checking in Java
categories:
  - Software quality
  - Software engineering
  - Java
  - Programming
  - Practice
---
<p>
In my <a href="../note/apple-ssl-case">latest post</a> I wrote about code quality: in a few words, I believe in and <a href="http://en.wikipedia.org/wiki/Static_program_analysis">static-checking</a>. Static means without executing the program. In a software process point of view, this would imply before runtime, in other words at compile-time. For a developer, it can be very useful to have such a verification simply with a compilation, without executing a specific tool (by the way, some very interesting software are available, just <a href="http://findbugs.sourceforge.net/">Findbugs</a> for example). Here is the point: how would it be possible to proceed that kind of control without rewriting a compiler from scratch ?
</p>
<p>
The <a href="../java/">Java</a> platform provides a very interesting feature to perform such operations: <a href="http://docs.oracle.com/javase/tutorial/java/annotations/">annotations</a>. These are metadata 
</p>
<p>
&lt; Java 8: <a href="http://docs.oracle.com/javase/7/docs/technotes/guides/apt/">APT</a>
</p>
<p>
&gt;= Java 8: <a href="https://www.jcp.org/en/jsr/detail?id=269">JSR 269</a>
</p>