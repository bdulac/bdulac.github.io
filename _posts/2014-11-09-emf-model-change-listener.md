---
layout: post
title: "EMF model change listener"
categories:
  - Eclipse platform
  - Java
resource: true
---
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
				<link itemprop="sameAs" href="https://twitter.com/vogella" />
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
