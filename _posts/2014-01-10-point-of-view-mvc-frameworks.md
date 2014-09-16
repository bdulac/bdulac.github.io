--- 
layout: post 
title: ! 'Point of view: MVC frameworks'
categories:
  - Software engineering
  - Point of view
  - Software design
resource: true
---
<p>
	After some (bad) experiences, I am quite sceptical about <a
		href="http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller">MVC</a>
	frameworks.	The hall of fame has accepted a few names: <a
		href="http://struts.apache.org/">Struts</a>, <a
		href="http://www.playframework.com/">Play</a>, <a
		href="https://wicket.apache.org/">Wicket</a>... And then ?
</p>
<p>
	Each period has its champion. Struts, as one of the elders, had a
	long period. So many developers had to use it. But what about software
	maintenance and evolutions ? Struts 1 upgrade to
	version 2 ? What about moving to another technology ?
</p>
<p>
	Quite a nightmare, it is sometimes easier to rewrite completely
	the application. In my point of view, long term solutions rely directly on the
	Java platform. The classic <a
		href="https://jcp.org/aboutJava/communityprocess/final/jsr315/">Servlet</a>
	/ <a href="https://jcp.org/aboutJava/communityprocess/final/jsr245/">JSP</a>&nbsp;tandem
	is not an MVC implementation but is plain and simple and evolutions are
	easy. I understand <a href="https://jcp.org/en/jsr/detail?id=314">JSF</a>
	enthusiasts. The solution is modern and interesting on a productivity
	point of view. I have a personal problem with JSF (and <a
		href="http://www.youtube.com/watch?v=9ei-rbULWoA#t=47m">others</a>
	share my opinion) : JSF and JSP are bad companions. What a shame for
	two specifications...
</p>
<p>
	While the RESTful architectural style is trendy, the idea of
	integrating <a href="https://www.jcp.org/en/jsr/detail?id=339">JAX-RS</a>
	and JSPs is interesting (<a
		href="https://jersey.java.net/documentation/latest/mvc.html">part</a>
	of <a href="https://jersey.java.net/">Jersey</a>). Hope it will be part of the core specification someday.
</p>
<p>
	<b>Edit</b> <em>(2014-08-21)</em> : the JAX-RS / MVC integration was part of the 
	<a href="https://jcp.org/en/jsr/detail?id=339">JSR 339</a> initial request but was dismissed in the final specification. 
	A <a href="https://java.net/projects/jax-rs-spec/lists/users/archive/2014-08/message/16">recent message</a> on the 
	specification list let me have some hope...
</p>