---
layout: page
title: JSTL
article: true
resource: true
categories:
  - Java
  - Web
---
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