--- 
layout: post 
title: Dynamic assignation and proxy objects
categories:
  - Java
  - Proxy
  - JPA implementation
resource: true
---
<p>
	Still in <a href="http://en.wikipedia.org/wiki/Java_Persistence_API">JPA</a>,
	you perhaps wonder how <a
		href="http://docs.oracle.com/javaee/6/api/javax/persistence/FetchType.html#LAZY">lazy-loading</a>
	is managed. This is done via proxy objects.
</p>
<p>
	The Java SE platform provides a <a
		href="http://docs.oracle.com/javase/7/docs/api/java/lang/reflect/Proxy.html">proxy
		class</a> which creates proxy objects for interfaces. But this does not
	help when you wish to do the job on <a
		href="http://martinfowler.com/bliki/POJO.html">POJOs</a>.
</p>
<p>
	A framework allows to do this (and many other <a
		href="http://en.wikipedia.org/wiki/Java_bytecode">bytecode</a>
	operations) : <a href="http://www.jboss.org/javassist/">Javassist</a>.
	The <a
		href="http://www.csg.ci.i.u-tokyo.ac.jp/~chiba/javassist/html/javassist/util/proxy/ProxyFactory.html">ProxyFactory</a>
	class allows to build a substitute object for any class via the <a
		href="http://www.csg.ci.i.u-tokyo.ac.jp/~chiba/javassist/html/javassist/util/proxy/ProxyFactory.html#createClass%28%29">createClass</a>
	method. I guess the substitution is done by subclassing.
</p>
<p></p>
<p>
	Instances of this "dynamic" class can be created calling the <a
		href="http://docs.oracle.com/javase/7/docs/api/java/lang/Class.html#newInstance%28%29">newInstance</a>
	method. The created object implements the <a
		href="http://www.csg.ci.i.u-tokyo.ac.jp/~chiba/javassist/html/javassist/util/proxy/Proxy.html">Proxy</a>
	interface. To this this interface can be associated a <a
		href="http://www.csg.ci.i.u-tokyo.ac.jp/~chiba/javassist/html/javassist/util/proxy/MethodHandler.html">MethodHandler</a>
	object. Such an object is called on any access to the dynamic instance
	(including null tests). For a lazy-loading field, this is where to
	replace the dynamic instance.
</p>
<p>
	It is also recommended to specify a <a
		href="http://www.csg.ci.i.u-tokyo.ac.jp/~chiba/javassist/html/javassist/util/proxy/MethodFilter.html">MethodFilter</a>
	object to the ProxyFactory to avoid the creation of proxies when
	finalizing the reference.
</p>
<p>
<pre> 	ProxyFactory factory = new ProxyFactory();
	factory.setSuperclass(MyClass.class);
	factory.setFilter(
	  new MethodFilter() {
	    public boolean isHandled(Method m) {
	        // The filter to avoid finalization
	        return !m.getName().equals("finalize");
	    }
	  }
	);
	Class cl = factory.createClass();
	MethodHandler handler = new MethodHandler() {
	    public Object invoke(
	      Object self, 
	      Method m, 
	      Method proceed,
	      Object[] args
	    ) throws Throwable {
	        // On each access, execution of the original operation
	        return proceed.invoke(self, args);
	    }
	};
	MyClass cls = (MyClass)cl.newInstance();
	((Proxy)cls).setHandler(handler);
</pre>
</p>
<p>
	My way crossed a single problem with Javassist: null tests. While
	using dynamic objects to avoid unnecessary database access, the method
	filter proceeded the proxy replacement (database access) properly on
	null tests in most cases. But in some rare cases, the null test did not
	call the method filter and did not perform the test properly. Perhaps
	was this a misuse of the library. Anyway the workaround was to perform
	a double check (null reference test + null test on a mandatory
	property) in order to ensure the method filter call.
</p>
<p>
	<b>Edit</b> <em>(2014-10-16)</em> : this last point requires further explanations (in a few words this was a misuse). I used Javassist proxies to implement lazy-loading of an object-relational mapped attribute. The point was about replacing the proxy object. To do so, I was only listening to method calls on the proxy. But a field access is not a method call: it was possible to create direct references on the proxy object before replacing it. It seemed then impossible to replace all the assignated references and the proxy object was still assignated (that caused the null tests to fail).
</p>
