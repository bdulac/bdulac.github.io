---
layout: page
title: JSTL (and EL)
article: true
resource: true
categories:
  - Java
  - Web
---
<div>
<h2><a href="#custom-el-functions" name="custom-el-functions">Custom EL functions</a></h2>
<p>
The first official documentation available on the topic is <em><a href="http://docs.oracle.com/javaee/5/tutorial/doc/bnahq.html#bnaio" target="_blank">The Java EE 5 tutorial</a></em>. The JSTL specification allows to define custom expressions. This is done easily with a simple static methods specified in a <em>Tag Library Definition</em> (tld) file. For example, a file located at <em>/WEB-INF/tags/my-functions.tld</em>:
</p>
<pre>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;taglib xmlns="http://java.sun.com/xml/ns/j2ee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee/web-jsptaglibrary_2_0.xsd"
	version="2.0"&gt;
    &lt;tlib-version&gt;2.0&lt;/tlib-version&gt;
    &lt;uri&gt;/WEB-INF/tags/my-functions.tld&lt;/uri&gt;
    &lt;function&gt;
    	&lt;name&gt;myMethod&lt;/name&gt;
        &lt;function-class&gt;my.package.MyFunctions&lt;/function-class&gt;
        &lt;function-signature&gt;java.lang.String myMethodSignature( java.lang.String )&lt;/function-signature&gt;
    &lt;/function&gt;
&lt;/taglib&gt;</pre>
<p>
Can be loaded by the JSP that way (the URI can be improved);
<pre>&lt;%@ taglib prefix="mine" uri="/WEB-INF/tags/my-functions.tld" %&gt></pre>
</p>
<p>
Then the static method is called with a simple expression using the specified prefix:
</p>
<pre>${mine:myMethod('my string value')}</pre>
<div>
<h2><a href="#fn" name="fn">"fn" (functions)</a></h2>
<p>
There is a problem in testing the content of an HTTP request URL: the <a href="http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html#getRequestURL()">HttpServletRequest method</a> returns a <a href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuffer.html">	StringBuffer</a>. The <a href="http://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fn/contains.fn.html">fn:contains(.., ..)</a> function accepts only strings. Using the <code>getRequestURL()</code> result as an argument works fine. But this is not static-type conform. Here the Eclipse IDE Web page validation complains.
</p>
<p>
In order to code in a static-type way, the solution is to set the <code>StringBuffer</code> in a variable to transform it into a string. Then the function can be used properly without any validation problem:  
</p>
<pre>&lt;c:set var="requestUrl" value="${pageContext.request.requestURL}" /&gt;
&lt;c:if test="${fn:contains(requestUrl, '...')}"&gt;
&lt;/c:if&gt;</pre>
</div>
<div>
<h2><a href="#fmt" name="fmt">"fmt" (messages)</a></h2>
<p>
Using a <a href="http://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fmt/message.html">message</a> tag (fmt) with <a href="http://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fmt/param.html">param</a> children, I had to escape quotes unless the message would not include the parameters.
</p>
</div>