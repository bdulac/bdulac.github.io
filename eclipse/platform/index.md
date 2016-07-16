---
layout: category
title: Eclipse platform and plug-in development (category)
article: true
resource: true
categoryPage: Eclipse platform
---
<div>
<h2>The Eclipse target platform</h2>
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
			    <link itemprop="sameAs" href="https://twitter.com/vogella" />
				  <span itemprop="givenName">Holger</span>
				  <span itemprop="familyName">Staudacher</span>
				</a>
			</span>
		</span>
	</span> explains how to
	<span itemprop="about">define a runtime for a Jersey/JAX-RS application</span>.
</span>
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
				    <link itemprop="sameAs" href="https://twitter.com/vogella" />
				    <span itemprop="givenName">Lars</span>
				    <span itemprop="familyName">Vogel</span>
				  </a>
			  </span>
		  </span>
		  details such a procedure (in section 3).
	  </span>
  </span>
</p>
