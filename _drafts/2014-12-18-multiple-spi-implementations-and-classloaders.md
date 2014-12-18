--- 
layout: post 
title: Multiple SPI(s) implementations and ClassLoaders
categories:
  - Java
  - SPI
  - JPA implementation
resource: true
--- 
<p>
Multiple implementations, SPI declaration available in the ClassPath.
ClassLoader ? <a href="http://docs.oracle.com/javase/6/docs/api/java/util/ServiceLoader.html#load(java.lang.Class, java.lang.ClassLoader)">ServiceLoader#loadClass(Class,ClassLoader)</a>
</p> 
<p>
But what about the access proposed by specific APIs ?
</p>
<ul>
  <li>
    <a href="http://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html#drivermanager">DriverManager.getCollection(...)</a> for JDBC
  </li>
  <li>
  	<a href="https://docs.oracle.com/javaee/6/api/javax/persistence/Persistence.html#createEntityManagerFactory(java.lang.String)">Persistence.createEntityManagerFactory(String)</a> for JPA
  </li>
</ul>
<p>
Before calling <a href="https://docs.oracle.com/javaee/6/api/javax/persistence/Persistence.html#createEntityManagerFactory(java.lang.String)">Persistence.createEntityManagerFactory(...)</a>
</p>
<pre>ClassLoader cLoader = getClass().getClassLoader();
		Thread.currentThread().setContextClassLoader(cLoader);</pre>
</p>