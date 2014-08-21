--- 
layout: post 
title: Memory errors in Java 
---
<p>
	Memory in <i>Java</i> is largely made easy by garbage collection. This
	automatic management of memory does not prevent from any memory
	problem. Here are some basics elements I find useful to review while
	facing a memory error.
</p>
<p>
	The memory is divided in two distinct spaces, even if this <a
		href="http://openjdk.java.net/jeps/122">might change in Java 8</a><a
		href="http://www.blogger.com/null">.</a><br />
<ul>
	<li>The PermGen space contains classes definitions</li>
	<li>The Heap space contains objects</li>
</ul>
When a memory problem occurs, an
<a
	href="http://docs.oracle.com/javase/7/docs/api/java/lang/OutOfMemoryError.html">error</a>
is raised. This
<a
	href="http://docs.oracle.com/javase/7/docs/api/java/lang/Throwable.html">throwable</a>
contains information about the cause of the problem and the impacted
memory space. Most of time, these informations are sufficient to help
solve the problem.
</p>
<p>
	The JVM options mentioned in this post are for <i>HotSpot</i>
	(Sun/Oracle implementation). For more informations, the <a
		href="http://www.oracle.com/technetwork/java/javase/gc-tuning-6-140523.html">official
		<i>HotSpot</i> tuning documentation
	</a> is very helpful.<br />
	<a
		href="http://docs.oracle.com/javase/7/docs/webnotes/tsg/TSG-VM/html/memleaks.html#gbyuu"><br /></a><a
		href="http://docs.oracle.com/javase/7/docs/webnotes/tsg/TSG-VM/html/memleaks.html#gbyuu"><u>java.lang.OutOfMemoryError:
			PermGen space</u></a><br />
<ul></ul>
The space allocated for classes definitions is full. This can happen if
the environment loads a large number of classes (common in Java EE
environments). The allocated space can be configured via the JVM option
<i>-XX:PermSize=256m</i>
(for 256 megabytes).
</p>
<p>
	In some situations, this saturation can be caused by a hot deployment.
	A workaround for such a problem is the JVM option&nbsp; <i>-XX:+CMSClassUnloadingEnabled</i>.
	This clear all references to obsolete classes definitions. A very
	helpful option when processing multiple hot deployments in a <i>Tomcat</i>
	environment.
</p>
<p>
	A <a
		href="http://frankkieviet.blogspot.fr/2006/10/classloader-leaks-dreaded-permgen-space.html">blog
		post</a> by Frank Kieviet explains a pattern that could also cause PermGen
	space errors.
</p>
<p>
	<a
		href="http://docs.oracle.com/javase/7/docs/webnotes/tsg/TSG-VM/html/memleaks.html#gbyvh"><u>Message
			java.lang.OutOfMemoryError: Java heap space</u></a>
</p>
<p>The created objects stay in the Heap space while being referenced
	in the executed program. When an object is not referenced any more, it
	becomes available for release by the Garbage Collector (GC). Most of
	time, the GC acts when the available memory becomes low. This is highly
	configurable with many JVM options.</p>
<p>
	If there is no memory leak, the easy solution is to increase the
	available space.<br />All becomes complicated when there is a memory
	leak. The cause can be difficult to identify. Several tools help to
	identify the problem nature.
</p>
<p>
	I personally generate an <i>hprof</i> file with the JVM option <i>-XX:+HeapDumpOnOutOfMemory</i>.
	Another JVM option <i>-XX:HeapDumpPath=...</i> allows to specify the
	generated file location.The <a href="http://www.eclipse.org/mat/">Eclipse
		MAT</a> tools helps to visualize the generated file.
</p>
<p>
	Another solution is to run your program with the Eclipse <a
		href="http://www.eclipse.org/tptp/">TPTP tools</a>. But I prefer to
	avoid this option because it requires much resources to run (and was
	quite unstable the last time I used it).
</p>
<p>
	<a
		href="http://www.oracle.com/technetwork/java/javase/gc-tuning-6-140523.html#cms.oom"><u>Message
			java.lang.OutOfMemoryError: GC limit overhead exceeded</u></a>
</p>
<p>
	This error happens when the system spends too much time executing
	garbage collection. Literally, there is no memory saturation but the
	system uses most of its memory despite garbage collections. A simple
	workaround can be to extend the Heap space. If the problem persists,
	tuning the GC configuration will probably be the solution.
</p>