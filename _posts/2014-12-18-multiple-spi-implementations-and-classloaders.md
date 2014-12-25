--- 
layout: post 
title: Multiple standard API implementations (SPI) and ClassLoaders
categories:
  - Java
  - SPI
  - Multiple
  - JPA implementation
resource: true
---
<p>
I recently faced a singular situation: I had to adapt an application as a <a href="http://lucene.apache.org/solr/"><em>Solr</em></a> plug-in. That application was using two different JPA implementations. As a reference to a <a href="http://bdulac.github.io/note/spi">previous post</a>, in a traditional environment a standard API implementation is usually specified using the SPI. A central interface for the API is identified (e.g. <a href="http://docs.oracle.com/javase/7/docs/api/java/sql/Driver.html">java.sql.Driver</a> for JDBC). Then the full name of the implementing class is specified in the content of a file available in the ClassPath under the location <em>META-INF/services/{"fullInterfaceName"}</em>. Multiple implementations can be specified on separate lines, this is an important point.
<p>
Usually nobody cares about the SPI: each implementation has its own <em>META-INF/services</em> declaration. If you want to check it just take a look inside the JAR of your usual JDBC driver (type 4). This is why the JDBC <a href="http://docs.oracle.com/javase/7/docs/api/java/sql/DriverManager.html">DriverManager</a> does not require any more to use a <em>Class.forName(...)</em> call since Java 6. Things become more complex when multiple implementations are available in the ClassPath: for example when an application uses both a PostgreSQL and a MySQL driver. This is a common case. The JDBC API solves the problem with a workaround: a specific <a href="http://docs.oracle.com/javase/tutorial/essential/environment/sysprop.html">system property</a> (jdbc.drivers) can be used to specify the classes names. This is not the case for all standard APIs. To solve that, the usual solution is to define your own <em>META-INF/services/{"fullInterfaceName"}</em> file in your application ClassPath. But with a <em>Solr</em> plug-in, just like my situation, it is difficult to handle the question of class loading.
</p>
<p>
In order to troubleshoot the loading of SPI implementations the JRE <a href="http://docs.oracle.com/javase/6/docs/api/java/util/ServiceLoader.html#load(java.lang.Class, java.lang.ClassLoader)">ServiceLoader#loadClass(Class,ClassLoader)</a> methods is a very useful tool. In my case, it showed me that the <a href="http://docs.oracle.com/javaee/6/api/javax/persistence/spi/PersistenceProvider.html">PersistenceProvider</a> implementations specified in my <em>META-INF/services/javax.persistence.spi.PersistenceProvider</em> file where not properly loaded in the <em>Solr</em> plug-in. As a consequence, the call to <a href="https://docs.oracle.com/javaee/6/api/javax/persistence/Persistence.html#createEntityManagerFactory(java.lang.String)">Persistence.createEntityManagerFactory(String)</a> failed.
</p>
<p>
Understanding that the problem of implementation discovery was related to the ClassLoader, I had a look at the <a href="https://github.com/eclipse/javax.persistence/blob/master/src/javax/persistence/spi/PersistenceProviderResolverHolder.java">source of PersistenceProviderResolverHolder</a>. It showed me that the ClassLoader used for the discovery of the JPA implementations was the current thread's:
<pre>
Thread.currentThread().getContextClassLoader()</pre>
<p>
Then the solution was obvious. Before calling <a href="https://docs.oracle.com/javaee/6/api/javax/persistence/Persistence.html#createEntityManagerFactory(java.lang.String)">Persistence.createEntityManagerFactory(...)</a> I just forced the ClassLoader associated to the thread:
</p>
<pre>ClassLoader cLoader = getClass().getClassLoader();
Thread.currentThread().setContextClassLoader(cLoader);</pre>
<p>
Well, in the end all is logical. But such problems can be quite challenging to understand. The <em>Java</em> platform could be improved on that point. Perhaps an improvement provided by <a href="http://openjdk.java.net/projects/jigsaw/">project Jigsaw</a> ? 
</p>