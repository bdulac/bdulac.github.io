---
layout: page
title: Eclipse platform and plug-in development
article: true
resource: true
categoryPage: Eclipse platform
categories:
  - Eclipse
  - Platform
  - Plug-in
---
<div>
<h2>Target platform</h2>
<p>
The Eclipse IDE has been a plug-in environment since its early versions. It has become an application platform since Eclipse 3 with the adoption of the <a href="http://en.wikipedia.org/wiki/OSGi">OSGi</a> modular system. <a href="http://www.eclipse.org/equinox/">Equinox</a>, a project developed by the foundation, is the OSGi framework implementation that runs the Eclipse IDE. Anyone developing an Eclipse plug-in also develops an OSGi bundle. As this technology is about modules, an important architectural point here is dependencies (between modules).
</p>
<p>
Other platforms than the Eclipse IDE adopt a similar organization, i.e. a set of OSGi bundles as components, here are three examples: 
</p>
<ul>
<li><em><a href="http://jonas.ow2.org/">JOnas</a></em></li>
<li><em><a href="https://glassfish.java.net/">Glassfish</a></em></li>
<li>Eclipse <em><a href="http://www.eclipse.org/virgo/">Virgo</a></em></li>
</ul>
<p>
Some components available as Eclipse plug-ins can be deployed in <em>JOnas</em> or <em>Glassfish</em>, for example the OSGi distribution of <a href="http://www.eclipse.org/eclipselink/">EclipseLink</a>. But this is not true for all plug-ins. As Eclipse is an IDE, dependencies on graphical elements come easily. Therefore most Eclipse plug-ins can't be deployed in other environments.
</p>
<p>
This is the reason why it is important to choose the right target platform when developing an Eclipse plug-in. A 
<span itemprop="citation" itemscope itemtype="http://schema.org/BlogPosting">
	<a itemprop="url" href="http://eclipsesource.com/blogs/2014/02/04/step-by-step-how-to-bring-jax-rs-and-osgi-together/">blog post</a> 
	<span>
	by
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<span itemprop="name">
			<a itemprop="sameAs" href="http://eclipsesource.com/blogs/author/hstaudacher/">
			<link itemprop="sameAs" href="https://twitter.com/vogella"></link>
				<span itemprop="givenName">Holger</span> 
				<span itemprop="familyName">Staudacher</span>
				</a>
			</span>
		</span>
	</span> explains how to 
	<span itemprop="about">define a runtime for a Jersey/JAX-RS application</span>.
</p>
<p>
This post is interesting on the definition point of view. A simple element is missing: 
	<span itemprop="citation" itemscope itemtype="http://schema.org/TechArticle">
	<span itemprop="about">how to use the defined target runtime</span> when developing an Eclipse plug-in ? A
		<a itemprop="url" href="http://www.vogella.com/tutorials/EclipseTargetPlatform/article.html">
			<span itemprop="learningResourceType">tutorial</span>
		</a> by 
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<span itemprop="name">
				<a itemprop="sameAs" href="http://www.vogella.com/people/larsvogel.html">
				<link itemprop="sameAs" href="https://twitter.com/vogella"></link>
				<span itemprop="givenName">Lars</span> 
				<span itemprop="familyName">Vogel</span>
				</a>
			</span>
		</span>
		details such a procedure (in section 3).
	</span> 
<p>
</div>
<div>
<h2><a href="#emf-model-change-listener" name="emf-model-change-listener">EMF model change listener</a></h2>
<p>
As explained in the <a href="http://www.eclipsezone.com/eclipse/forums/t115262.html">EclipseZone forum exchange</a> on the topic, two strategies are available to listen to changes on an EMF model:  
</p>
<ol>
	<li>
		<em><a href="http://download.eclipse.org/modeling/emf/emf/javadoc/2.4.3/org/eclipse/emf/ecore/util/EContentAdapter.html">EContentAdapter</a></em> (from the EMF core)
	</li>
	<li>
		<em><a href="http://download.eclipse.org/modeling/emf/transaction/javadoc/workspace/1.4.0/org/eclipse/emf/transaction/ResourceSetListener.html">ResourceSetListener</a></em> (from the <a href="https://wiki.eclipse.org/EMF/Transaction">EMF/transaction</a>)
	</li>
</ol>
<p>
The <em>EContentAdapter</em> notifies of change on any EMF object (<em>EObject</em>). This requires to have a direct access on the object, what does not help much to listen on third-party changes (external editor on anything else). A 
	<span itemprop="citation" itemscope itemtype="http://schema.org/TechArticle">
		<a itemprop="url" href="http://www.vogella.com/tutorials/EclipseEMFNotification/article.html">
			<span itemprop="learningResourceType">tutorial</span>
		</a> by 
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<span itemprop="name">
				<a itemprop="sameAs" href="http://www.vogella.com/people/larsvogel.html">
				<link itemprop="sameAs" href="https://twitter.com/vogella"></link>
				<span itemprop="givenName">Lars</span> 
				<span itemprop="familyName">Vogel</span>
				</a>
			</span>
		</span>
	</span> details how to use it.
</p>
<p>
The <em>ResourceSetListener</em> solution, far more complete on the transaction point of view, helps to listen on external editor changes. It is <a href="http://en.wikipedia.org/wiki/Observer_pattern">observer pattern</a>. An access to the editor's editing domain is required, it must be of type <em><a href="http://download.eclipse.org/modeling/emf/transaction/javadoc/1.1.1/org/eclipse/emf/transaction/TransactionalEditingDomain.html">TransactionalEditingDomain</a></em> in order to expose the <a href="http://download.eclipse.org/modeling/emf/transaction/javadoc/1.1.1/org/eclipse/emf/transaction/TransactionalEditingDomain.html#addResourceSetListener%28org.eclipse.emf.transaction.ResourceSetListener%29">registration method</a>. 
</p>
</div>
<div>
<h2><a href="#jdt-decode-signatures" name="jdt-decode-signatures">Decode simple JDT signatures</a></h2>
<p>
The JDT sometimes returns simplified type signatures, for example the <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IMethod.html#getParameterTypes--">IMethod#getParameterTypes()</a></em> method can return values such as <em>QString</em> instead of <em>java.lang.String</em>. 
</p>
<p>
To decode such values, the <em><a href="http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FSignature.html">org.eclipse.jdt.core.Signature</a></em> class provides utility functions. <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/Signature.html#getSignatureSimpleName-java.lang.String-">Signature#getSignatureSimpleName(String)</a></em> transforms <em>QString</em> into the simple name, i.e. <em>String</em>.
</p>
<p>To get the full name, the containing type allows to resolve the simple name. <em><a href="http://help.eclipse.org/juno/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IType.html#resolveType(java.lang.String)">IType#resolveType(String)</a></em> transforms this simple name using the imports of the containing type. The result is an array with two dimensions. The first one is for the case where there are multiple answers possible. The second one separates the name of the package and the simple name. 
</p>
<p>
The following code returns the first full name of a method return type:
</p>
<pre>
	String name = method.getReturnType();
	String simpleName = Signature.getSignatureSimpleName(name);
	IType type = method.getDeclaringType();
	String[][] allResults = type.resolveType(simpleName);
	String fullName = null;
	if(allResults != null) {
		String[] nameParts = allResults[0];
		if(nameParts != null) {
			fullName = new String();
			for(int i=0 ; i < nameParts.length ; i++) {
				if(fullName.length() > 0) {
					fullName += '.';
				}
				if(nameParts[i] != null) {
					fullName += nameParts[i];
				}
			}
		}
	}
	return name;</pre>
<p>
An <a href="http://stackoverflow.com/a/27777064/1207019">exchange on stackoverflow</a> details the code for parameters types full names.
</p>
</div>
<div>
<h2><a href="#programmatically-refactor-jdt" name="programmatically-refactor-jdt">Programmatically refactor with the JDT</a></h2>
<p>
Using the internal <a href="http://git.eclipse.org/c/jdt/eclipse.jdt.ui.git/plain/org.eclipse.jdt.ui/core%20refactoring/org/eclipse/jdt/internal/corext/refactoring/rename/">rename package</a> is not a very good idea (discouraged access warning). There is an <a href="http://www.eclipse.org/articles/article.php?file=Article-Unleashing-the-Power-of-Refactoring/index.html">official documentation</a> on that topic. A <a href="http://stackoverflow.com/q/9129689/1207019">stackoverflow exchange</a> also mentions interesting informations.
</p>
</div>