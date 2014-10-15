--- 
layout: post 
title: Design by contract, assertions and exceptions
categories:
  - Software engineering
  - Software quality
  - Programming practice
  - Java
  - Point of view
  - Design by contract
  - Assertion
  - Exception
resource: true
---
<p>Understanding design by contract is, I think, important for software quality (at least in <a href="http://en.wikipedia.org/wiki/Object-oriented_programming">OOP</a>).</p>
<p>
	<span itemprop="citation" itemscope itemtype="http://schema.org/Book">
		<link itemprop="sameAs" href="http://www.worldcat.org/oclc/17675237"></link>
		<span itemprop="author" itemscope itemtype="http://schema.org/Person" itemid="#meyer">
			<a itemprop="sameAs" href="http://en.wikipedia.org/wiki/Bertrand_Meyer">
				<link itemprop="sameAs" href="http://viaf.org/viaf/51714577"></link>
				<span itemprop="name">
					B. 
					<span itemprop="givenName" style="display:none;">Bertrand</span>
					<span itemprop="familyName">Meyer</span>
				</span>
			</a>
		</span>
		<a href="http://en.wikipedia.org/wiki/Object-Oriented_Software_Construction">introduced the idea</a>
		in <span itemprop="copyrightYear">1988</span>. 
	</span>
	It takes advantage of 
	<span itemprop="citation" itemscope itemtype="http://schema.org/ScholarlyArticle">
		<link itemprop="sameAs" href="http://dx.doi.org/10.1145/363235.363259"></link>
		<span itemprop="about">assertions</span>
		<a href="http://dx.doi.org/10.1145/363235.363259"> as defined</a> 
		by 
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<a itemprop="sameAs" href="http://en.wikipedia.org/wiki/Tony_Hoare">
				<link itemprop="sameAs" href="http://viaf.org/viaf/108123782"></link>
				<span itemprop="name">
					C.A.R. 
					<span itemprop="givenName" style="display:none;">Charles</span>
					<span itemprop="additionalName" style="display:none;">Anthony</span>
					<span itemprop="additionalName" style="display:none;">Richard</span>
					<span itemprop="familyName">Hoare</span>
				</span>
			</a>
		</span>
		(<span itemprop="copyrightYear">1969</span>), the seminal work of an <a itemprop="about" href="http://en.wikipedia.org/wiki/Hoare_logic">eponymous logic</a>.
	</span>
</p>
<p>
	Assertions are associated to an object method and qualified in
	one of three categories :
</p>
<ul>
	<li>Preconditions are assertions true before executing the method</li>
	<li>Postconditions are assertions true after executing the method</li>
	<li>Invariants are assertions true before and after executing the method</li>
</ul>
<p>
	<span itemscope itemtype="http://schema.org/SoftwareApplication">
		<span itemprop="author" itemscope itemtype="http://schema.org/Person" itemid="#meyer">
			<link itemprop="sameAs" href="#meyer">Meyer</link>
		</span> includes his idea in the 
		<a itemprop="url" href="http://www.eiffel.com/">Eiffel</a> 
		<span itemprop="applicationCategory">programming language</span>
	</span> : the assertions are checked in a static way (at
	compile time).
</p>
<p>
	If the <em>Java</em> programming language provides support for 
	<a href="http://docs.oracle.com/javase/7/docs/technotes/guides/language/assert.html">assertions</a>,
	these are checked only in a dynamic way (at runtime) and disabled by default. Because of runtime checking, 
	<a href="http://docs.oracle.com/javase/tutorial/essential/exceptions/">exceptions</a>
	are largely used instead of assertions. 
	In <i>Java</i>, a <a href="http://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html">proper</a> use of
	exceptions is more expressive than a proper use of assertions.
</p>
<p>
	<span itemprop="citation" itemscope itemtype="http://schema.org/Book">
		In 
		<link itemprop="sameAs" href="http://www.worldcat.org/oclc/124025332"></link>
		<a itemprop="sameAs" href="http://www.pearsonhighered.com/educator/product/Effective-Java/9780321356680.page">
			<span itemprop="name">Effective Java</span>
		</a>, 
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<a itemprop="sameAs" href="http://en.wikipedia.org/wiki/Joshua_Bloch">
				<link itemprop="sameAs" href="http://viaf.org/viaf/71793922"></link>
				<link itemprop="sameAs" href="https://twitter.com/joshbloch"></link>
				<span itemprop="name">
					<span itemprop="familyName">Bloch</span>
				</span>
			</a>
		</span> 
		defines 		
		<a href="http://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html">checked exceptions</a> as recoverable conditions
		<a href="http://docs.oracle.com/javase/7/docs/api/java/lang/RuntimeException.html">runtime exceptions</a> as programming errors.
	</span> 
</p>
<p>
	In an non-Java context, 
	<span itemprop="citation" itemscope itemtype="http://schema.org/Book">
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<a itemprop="sameAs" http://en.wikipedia.org/wiki/Martin_Fowler">
				<link itemprop="sameAs" href="http://viaf.org/viaf/5145169"></link>
				<span itemprop="name">
					Fowler
				</span>
			</a>
		</span>
		<a itemprop="sameAs" href="http://www.worldcat.org/oclc/630586726">says</a>
		 an exception is a situation where preconditions are satisfied but postconditions can not be satisfied.
	</span>
</p>
<p>I consider</p>
<ul>
	<li>Runtime exceptions should be used for checking preconditions</li>
	<li>
		Checked exceptions should be used when preconditions are true but postconditions can not be satisfied, assuming that the method is correct (e.g. the network connection is broken).&nbsp;
	</li>
</ul>
<p>
If a runtime exception is raised, the calling method should be bugged (or its preconditions are not properly checked).
</p>
<p>
	Some extensions to the <em>Java</em> platform provide support for static
	testing (assertions checking at compile time). For example, <a href="http://www.eecs.ucf.edu/~leavens/JML/">JML</a> takes advantage of <em>Java</em> comments: this is interesting for traditional compiling compliance.
</p>