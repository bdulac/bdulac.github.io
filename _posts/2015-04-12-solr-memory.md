--- 
layout: post 
title: Apache Solr and memory management with <em>mmap</em> system calls
categories:
  - Web
  - Solr
---
<p>
In the frame of my professional practice, I built most of an architecture based on <em><a href="http://lucene.apache.org/solr/">Apache Solr</a></em>. This platform is in a few words an <a href=="http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol">HTTP</a> interface handling one or several <em><a href="http://lucene.apache.org/">Apache Lucene</a></em> indexes. The classical access to <em>Solr</em>-managed indexes is made with an HTTP client. Some solutions like the <em><a href="https://wiki.apache.org/solr/DataImportHandler">DataImportHandler</a></em> allow to write in the <em>Lucene</em> files directly on the server side: for several reasons we chose to use the traditional client API called <em><a href="https://wiki.apache.org/solr/Solrj">SolrJ</a></em>.
</p>
<p>
Unlike other indexing software like <em><a href="https://github.com/elastic/elasticsearch">Elasticsearch</a></em>, <em>Solr</em> can be deployed in any <a href="http://en.wikipedia.org/wiki/Web_container"><em>Java Servlet</em> container</a>. The documentation provides an <a href="https://wiki.apache.org/solr/SolrTomcat">example with <em>Apache Tomcat</em></a>: this is our target environment. Like in any other <em>Tomcat</em> installation, there is the question of memory allocation to the JVM. Reading the <a href="https://wiki.apache.org/solr/SolrPerformanceFactors#Memory_allocated_to_the_Java_VM "><em>Solr</em> section on the topic</a>, it was chosen to allow a large part of the RAM to the JVM (5GB on a total of 6: one for the system). 
</p>
<p>
We identified quickly a main problem: while indexing, the <em>Solr</em> engine issued <em>timeout</em> errors on <em>select</em> queries. A <a href="http://stackoverflow.com/q/14635381/1207019">stackoverflow exchange</a> describes a similar behavior. We noticed on server side an important usage of virtual memory.
</p>
<p>
As I answered in the exchange, we solved this problem a few months ago after reading a <a href="http://blog.thetaphi.de/2012/07/use-lucenes-mmapdirectory-on-64bit.html">blog post</a> by Uwe Schindler (a <em>Solr</em> committer). With <em>Solr 4</em> and several <em>Solr 3</em> versions, you have to let an important share of your RAM free so that the system can use properly the <em>mmap</em> system call. This is due to the introduction of a new <em>Lucene</em> component: the <em><a href="https://lucene.apache.org/core/3_5_0/api/core/org/apache/lucene/store/MMapDirectory.html">MMapDirectory</a></em>. The blog post gives a plenty of informations on the system configuration. In our case, this solved the problem: we could finally index without any more <em>timeout</em> issue.
</p>