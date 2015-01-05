---
layout: page
title: JAX-RS (category)
article: true
resource: true
categories:
  - Java
  - Web
  - REST
---
<div>
<p>
<a href="https://jax-rs-spec.java.net/">Java API for RESTful Services (JAX-RS)</a> is defined in three specifications:
</p>
<ul>
	<li>JAX-RS 1.0 (<a href="https://jcp.org/en/jsr/detail?id=311">JSR 311</a>, part of <em>Java EE</em> 6, <em>Java SE/EE</em> 5 compliant)</li>
	<li>JAX-RS 1.1 (<a href="https://jcp.org/aboutJava/communityprocess/maintenance/jsr311/">JSR 311 maintenance release</a>)</li>
	<li>JAX-RS 2.0 (<a href="https://jcp.org/en/jsr/detail?id=339">JSR 339</a>, part of <em>Java EE</em> 7, <em>Java SE/EE</em> 6 compliant)</li>
</ul>
<p>
The reference implementation is <em>Jersey</em>. These notes largely summarize the <a href="https://jersey.java.net/documentation/latest/">documentation</a>. 	Here we consider JAX-RS development outside of any <em>Java EE</em> application server.
</p>
<p>
For non-maven developers, dependencies for pure JAX-RS development are limited. The only needed libraries are JARs in the <a href="https://jersey.java.net/download.html">RI bundle</a> <em>lib</em> and <em>api</em> directories.
</p>
<p>
For a maven project: 
</p>
<pre>&lt;dependency&gt;
    &lt;groupId&gt;javax.ws.rs&lt;/groupId&gt;
    &lt;artifactId&gt;javax.ws.rs-api&lt;/artifactId&gt;
    &lt;version&gt;2.12&lt;/version&gt;
&lt;/dependency&gt;</pre>
<p>
To use jersey-specific features, the following dependecies should be specified:
</p>
<pre>&lt;dependency&gt;
    &lt;groupId&gt;org.glassfish.jersey.containers&lt;/groupId&gt;
    &lt;artifactId&gt;jersey-container-servlet&lt;/artifactId&gt;
    &lt;version&gt;2.12&lt;/version&gt;
&lt;/dependency&gt;
<!-- For Jersey client-specific features -->
&lt;dependency&gt;
    &lt;groupId&gt;org.glassfish.jersey.core&lt;/groupId&gt;
    &lt;artifactId&gt;jersey-client&lt;/artifactId&gt;
    &lt;version&gt;2.12&lt;/version&gt;
&lt;/dependency&gt;</pre>
<p>
<b>TODO</b> concise conf & environment note for JAX-RS dev with <em>Jersey</em> in <em>Java SE</em> env...
</p>
<p>Here are some personal notes about JAX-RS components and extensions...</p>
</div>
<div>
<h2><a href="#client-api" name="client-api">Client API</a></h2>
<p>
The RESTful client API is part of the specification since JAX-RS 2.0. The classifiers are defined in the <a href="http://docs.oracle.com/javaee/7/api/javax/ws/rs/client/package-summary.html">javax.ws.rs.client</a> package. The component implementation is identified in <a href="http://cxf.apache.org/docs/jax-rs-client-api.html">CXF</a>, <a href="http://docs.jboss.org/resteasy/docs/3.0-beta-3/userguide/html/RESTEasy_Client_Framework.html">RestEasty</a> and <a href="https://jersey.java.net/documentation/2.12/client.html">Jersey</a>.
</p>
<p>
Since JAX-RS 2.0, as the client API is part of the specification, Jersey does not require any more libraries than the <a href="https://jersey.java.net/download.html">RI bundle</a> <em>lib</em> directory.
</p>
</div>
<div>
<h2><a href="#multipart" name="multipart">Multipart</a></h2>
<p>
<a href="http://www.w3.org/Protocols/rfc1341/7_2_Multipart.html">Multipart</a> does not seem to be covered by the JAX-RS specifications. However, <a href="http://cxf.apache.org/docs/jax-rs-multiparts.html#JAX-RSMultiparts-MultipartannotationandOptionalattachments">CXF</a>, <a href="http://docs.jboss.org/resteasy/docs/1.1.GA/userguide/html/Multipart.html">RestEasy</a> and <a href="https://jersey.java.net/apidocs/2.12/jersey/org/glassfish/jersey/media/multipart/package-summary.html">Jersey</a> provide a non-standard support for such a content-type.
</p>
<p>
This guide summarizes informations from the <a href="https://jersey.java.net/documentation/2.12/media.html#multipart">Jersey 2.12</a> documentation.
</p>
<p>
For a non-maven project, the <a href="https://jersey.java.net/project-info/2.12/jersey/project/jersey-media-multipart/dependencies.html">list of dependencies</a> should be satisfied. To the core, Jersey needs two additional JARs: 
</p>
<ul>
	<li><a href="http://repo1.maven.org/maven2/org/glassfish/jersey/media/jersey-media-multipart/">Media-Multipart</a></li>
	<li><a href="https://mimepull.java.net/">MIME pull</a></li>
</ul>
<p>
For a maven project: 
</p>
<pre>&lt;dependency&gt;
    &lt;groupId&gt;org.glassfish.jersey.media&lt;/groupId&gt;
    &lt;artifactId&gt;jersey-media-multipart&lt;/artifactId&gt;
    &lt;version&gt;2.12&lt;/version&gt;
&lt;/dependency&gt;</pre>
<p>
The use is rather simple, e.g. with a file:
</p>
<pre>@FormDataParam("paramName")
		File f
		</pre>
</div>
<div  itemprop="about" itemscope itemtype="http://schema.org/SoftwareApplication">
<h2><a href="#jersey-json" name="jersey-json">JSON processing with Jersey 2</a></h2>
<!--
<p>See <a href="http://bdulac.github.io/note/json-processing-with-jersey">this note</a>.</p>
-->
<p>
An experience (first published in the blog - 2014-09-26 - too technical for such a place)...
</p>
<p>
I tried to use 
	<a itemprop="url" href="https://jersey.java.net/documentation/2.12/media.html#json.json-p">
		<span itemprop="name">JSONP
	</span>
	</a> with 
	<span itemprop="isPartOf" itemscope itemtype="http://schema.org/SoftwareApplication>
		<a itemprop="url" href="https://jersey.java.net/">
			<span itemprop="name"><em>Jersey</em></span>
		</a>
	</span>. 
	Simple use case: turn a JSON server response into POJOs (a Jersey service is client of another RESTful service)...
</p>
<p>
First step, Jersey installation: for a non-maven project in a <a href="http://tomcat.apache.org/">Tomcat</a> environment, the <a href="https://jersey.java.net/project-info/2.12/jersey/project/jersey-media-json-processing/dependencies.html">list of dependencies</a> should be satisfied in addition to the core framework. The elements can be found in:
</p>
<ul>
	<li>The <a itemprop="requirements" href="https://jersey.java.net/download.html">RI bundle</a> </li>
	<li><a itemprop="requirements" href="http://search.maven.org/remotecontent?filepath=javax/json/javax.json-api/1.0/javax.json-api-1.0.jar">JSONP-API</a></li>
	<li><a itemprop="requirements" href="http://search.maven.org/remotecontent?filepath=org/glassfish/javax.json/1.0.4/javax.json-1.0.4.jar">JSONP</a></li>
	<li><a itemprop="requirements" href="http://central.maven.org/maven2/org/glassfish/jsonp-jaxrs/1.0/jsonp-jaxrs-1.0.jar">JSONP-JAX-RS</a></li>
	<li><a itemprop="requirements" href="http://repo1.maven.org/maven2/org/glassfish/jersey/media/jersey-media-json-processing/">Jersey-Media-Json-Processing</a></li>
</ul>
<p>
For the client code, I followed the <a href="https://jersey.java.net/documentation/2.12/client.html#client.ex.formpost">Jersey client doc sample</a>. Well, all I got was: 
</p>
<pre>MessageBodyReader not found for media type=application/json</pre>
<p>
Then, I discovered the following <a href="https://blogs.oracle.com/groundside/entry/jax_rs_2_0_messagebodyreader">post</a>. Consequently, I added an explicit default constructor. Same error. I read the <a href="https://jersey.java.net/documentation/2.12/media.html#d0e6497">Jersey-JSON doc</a> again. What a shame: 
</p>
<pre>POJO support represents the easiest way to convert your Java Objects to JSON and back. Media modules that support this approach are MOXy and Jackson</pre>
<p>
It seems JSONP is not able to provide a simple POJO support. I came back to <a href="http://www.json.org/java/">the basics</a>. All that mess with Jackson, Moxy, JSONP for such simple operations reminds me of an XML nightmare a few years ago... 
</p>
</div>
<div>
<h2><a href="#jersey-mvc-jsp" name="jersey-mvc-jsp">Jersey 2 Integration with JSP</a></h2>
<p>
This guide summarizes informations from the <a href="https://jersey.java.net/documentation/2.12/mvc.html">Jersey 2.12</a> documentation. The MVC and MVC features are extensions.
</p>
<p>
For a non-maven project, the <a href="https://jersey.java.net/project-info/2.12/jersey/project/jersey-mvc-jsp/dependencies.html">list of dependencies</a> should be satisfied. The elements can be found in: 
</p>
<ul>
	<li>The <a href="https://jersey.java.net/download.html">RI bundle</a> (plus the ext directory)</li>
	<li>The MVC and MVC-JSP extensions in the <a href="http://repo1.maven.org/maven2/org/glassfish/jersey/ext/">maven repository</a></li>
</ul>
<p>
For a maven project: 
</p>
<pre>&lt;dependency&gt;
    &lt;groupId&gt;org.glassfish.jersey.ext&lt;/groupId&gt;
    &lt;artifactId&gt;jersey-mvc-jsp&lt;/artifactId&gt;
    &lt;version&gt;2.12&lt;/version&gt;
&lt;/dependency&gt;</pre>
<p>
The next step is to specialize the <a href="https://jersey.java.net/apidocs/2.0/jersey/org/glassfish/jersey/server/ResourceConfig.html">ResourceConfig</a> class and to register the <a href="https://jersey.java.net/apidocs/2.12/jersey/org/glassfish/jersey/server/mvc/MvcFeature.html">McvFeature</a> and <a href="https://jersey.java.net/apidocs/2.12/jersey/org/glassfish/jersey/server/mvc/jsp/JspMvcFeature.html">JspMvcFeature</a> classes so that the extensions are loaded (in the constructor). By the way, the JSP pages path has to be specified:
</p>
<pre>super.register(org.glassfish.jersey.server.mvc.MvcFeature.class)
    .register(org.glassfish.jersey.server.mvc.jsp.JspMvcFeature.class)
    .property(MvcProperties.TEMPLATE_BASE_PATH, "templates");</pre>
<p>
Finally, jersey has to be registered as a web application. As of 2.12 version, the servlet mapping mode (web.xml or <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/ApplicationPath.html">ApplicationPath</a> annotation) is not supported by the <a href="https://jersey.java.net/documentation/2.12/mvc.html#mvc.example.implicit.class">MVC extension</a>. Jersey should be deployed as <a href="https://jersey.java.net/documentation/2.12/deployment.html#deployment.servlet.2">servlet filter</a>. Extract from the doc: 
</p>
<pre>&lt;web-app&gt;
    &lt;filter&gt;
        &lt;filter-name&gt;MyApplication&lt;/filter-name&gt;
        &lt;filter-class&gt;org.glassfish.jersey.servlet.ServletContainer&lt;/filter-class&gt;
        &lt;init-param&gt;
            ...
        &lt;/init-param&gt;
    &lt;/filter&gt;
    ...
    &lt;filter-mapping&gt;
        &lt;filter-name&gt;MyApplication&lt;/filter-name&gt;
        &lt;url-pattern&gt;/myApp/*&lt;/url-pattern&gt;
    &lt;/filter-mapping&gt;
    ...
&lt;/web-app&gt;</pre>
</div>
<div>
<h2><a href="#jersey-encoding" name="jersey-encoding">Encoding with Jersey 2</a></h2>
<p>
It seems Jersey 2 sets the encoding content type header as ISO-8859-1, even if the content is encoded in UTF-8 and a JSP page directive sets the proper value. The solution is to use a servlet filter to override the behavior. Tomcat provides <a href="https://tomcat.apache.org/tomcat-7.0-doc/api/org/apache/catalina/filters/SetCharacterEncodingFilter.html">one</a> out of the box, ready to use (configuration only, no coding).
</p>
</div>
<div>
<h2><a href="#http-301-code" name="http-301-code">HTTP 301 status code: Moved Permanently</a></h2>
<p>
The JAX-RS API does not expose an out-of-the box method to produce an <a href="http://en.wikipedia.org/wiki/HTTP_301">HTTP 301</a> response (as available for a temporary redirect - HTTP 307). The solution is to produce a <a href="http://en.wikipedia.org/wiki/HTTP_location">Location</a> header, here is the code (<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2">see here</a> for more details):
</p>
<pre>String redirUri = ...;
    return Response.status(Status.MOVED_PERMANENTLY)
        .header("Location", redirUri).build();
</pre>
</div>