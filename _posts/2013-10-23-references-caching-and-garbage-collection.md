--- 
layout: post 
title: References, caching and garbage collection 
categories:
  - Java
  - JPA implementation
---
<p>For a long time I have been wondering how do frameworks manage
	memory while caching.</p>
<p>
	The <a href="http://www.eclipse.org/eclipselink/">EclipseLink</a>
	documentation <a
		href="http://wiki.eclipse.org/EclipseLink/UserGuide/JPA/Basic_JPA_Development/Caching/Type_and_Size">gave
		me the answer</a>. The Java SE platform provide special references :
</p>
<ul>
	<li><a
		href="http://docs.oracle.com/javase/7/docs/api/java/lang/ref/SoftReference.html">Soft
			references</a></li>
	<li><a
		href="http://docs.oracle.com/javase/7/docs/api/java/lang/ref/WeakReference.html">Weak
			references</a></li>
	<li><a
		href="http://docs.oracle.com/javase/7/docs/api/java/lang/ref/PhantomReference.html">Phantom
			references</a></li>
</ul>
<p>
	According to the official documentation, soft references are used to
	provide memory-sensitive properties to cached references. This can be
	very efficient.
</p>
<p>But access to soft-referenced objects needs to be done via
	specific objects so that freed references can be renewed (e.g. via a
	persistent storage).</p>
<p>
	The official API also provides a special <a
		href="http://docs.oracle.com/javase/7/docs/api/java/util/WeakHashMap.html">map
		with weak referenced keys</a>. This class can be useful but is not really
	appropriate for caching as keys are released.
</p>