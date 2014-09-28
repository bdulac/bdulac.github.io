--- 
layout: post 
title: "JSON processing with Jersey 2"
categories:
  - Java
  - Jersey
  - JSON
  - Programming practice
---
<span itemprop="about" itemscope itemtype="http://schema.org/SoftwareApplication">
<p>
Today I tried to use 
<a itemprop="url" href="https://jersey.java.net/documentation/2.12/media.html#json.json-p">
	<span itemprop="name">JSONP</span>
</a>
 with 
<span itemprop="isPartOf" itemscope itemtype="http://schema.org/SoftwareApplication>
	<a itemprop="url" href="https://jersey.java.net/">
		<span itemprop="name"><em>Jersey</em></span>
	</a>
</span>. Simple use case: turn a JSON server response into POJOs (a Jersey service is client of another RESTful service)...
</p>
<p>
First step, Jersey installation: for a non-maven project in a <a href="http://tomcat.apache.org/">Tomcat</a> environment, the <a href="https://jersey.java.net/project-info/2.12/jersey/project/jersey-media-json-processing/dependencies.html">list of dependencies</a> should be satisfied in addition to the core framework. The elements can be found in:
</p>
<ul>
	<li>
		The <a itemprop="requirements" href="https://jersey.java.net/download.html">RI bundle</a> 
	</li>
	<li><a itemprop="requirements" href="http://search.maven.org/remotecontent?filepath=javax/json/javax.json-api/1.0/javax.json-api-1.0.jar">JSONP-API</a></li>
	<li><a itemprop="requirements" href="http://search.maven.org/remotecontent?filepath=org/glassfish/javax.json/1.0.4/javax.json-1.0.4.jar">JSONP</a></li>
	<li><a itemprop="requirements" href="http://central.maven.org/maven2/org/glassfish/jsonp-jaxrs/1.0/jsonp-jaxrs-1.0.jar">JSONP-JAX-RS</</a></li>
	<li><a itemprop="requirements" href="http://repo1.maven.org/maven2/org/glassfish/jersey/media/jersey-media-json-processing/">Jersey-Media-Json-Processing</a></li>
</ul>
<p>For the client code, I followed the <a href="https://jersey.java.net/documentation/2.12/client.html#client.ex.formpost">Jersey client doc sample</a>. Well, all I got was: </p>
<pre>MessageBodyReader not found for media type=application/json</pre>
<p>
		Then, I discovered the following 
		<a href="https://blogs.oracle.com/groundside/entry/jax_rs_2_0_messagebodyreader">post</a>.
		I added an explicit default constructor. Same error. I read the <a href="https://jersey.java.net/documentation/2.12/media.html#d0e6497">Jersey-JSON doc</a> again. What a shame: 
</p>
<pre>POJO support represents the easiest way to convert your Java Objects to JSON and back.

Media modules that support this approach are MOXy and Jackson</pre>
<p>
			It seems JSONP is not able to provide a simple POJO support. 
			I came back to <a href="http://www.json.org/java/">the basics</a>.
			All that mess with Jackson, Moxy, JSONP for such basic operations reminds me of an XML nightmare a few years ago... 
</p>
</span>