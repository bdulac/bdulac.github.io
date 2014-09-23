--- 
layout: post 
title: Design by contract, assertions and exceptions
categories:
  - Software engineering
  - Software quality
  - Programming practice
  - Point of view
  - Design by contract
  - Assertion
  - Exception
resource: true
---
<p>Understanding design by contract is important for code quality.</p>
<p>
	<span itemscope itemtype="http://schema.org/Book">
		<link itemprop="sameAs" href="http://www.worldcat.org/oclc/17675237"></link>
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<a itemprop="sameAs" href="http://viaf.org/viaf/51714577">
				<span itemprop="name">B. Meyer</span>
			</a>
		</span>
		<a href="http://www.worldcat.org/oclc/17675237">introduced the idea</a>
	</span>
	in <span itemprop="copyrightYear">1988</span>. 
	It takes advantage of 
	<span itemscope itemtype="http://schema.org/ScholarlyArticle">
		<link itemprop="sameAs" href="http://dx.doi.org/10.1145/363235.363259"></link>
		<span itemprop="about">assertions</span>
		<a href="http://dx.doi.org/10.1145/363235.363259"> as defined</a> 
		by 
		<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			<a itemprop="sameAs" href="http://viaf.org/viaf/108123782">
				<span itemprop="name">
				C.A.R. Hoare
				</span>
			</a>
		</span>
		(<span itemprop="copyrightYear">1969</span>).
	</span>
</p>
<p>
	Assertions are associated to an object method and qualified in
	one of three categories :
</p>
<ul>
	<li>Preconditions are assertions true before executing the method</li>
	<li>Postconditions are assertions true after executing the method</li>
	<li>Invariants are assertions true before and after executing the
		method</li>
</ul>
<p>
	Meyer includes his idea in the <a href="http://www.eiffel.com/">Eiffel</a>
	programming language : the assertions are checked in a static way (at
	compile time).
</p>
<p>
	If the <i>Java</i> programming language provides support for <a
		href="http://docs.oracle.com/javase/7/docs/technotes/guides/language/assert.html">assertions</a>,
	these are checked only in a dynamic way (at runtime) and disabled by
	default. Because of runtime checking, <a
		href="http://docs.oracle.com/javase/tutorial/essential/exceptions/">exceptions</a>
	are largely used instead of assertions. In <i>Java</i>, a proper use of
	exceptions<a
		href="http://docs.oracle.com/javase/tutorial/essential/exceptions/"></a>
	is more expressive than a proper use of assertions.
</p>
<p>
	<a href="http://viaf.org/viaf/71793922">Bloch</a> <a
		href="http://www.worldcat.org/oclc/124025332">defines</a> runtime
	exceptions as programming errors and checked exceptions as recoverable
	conditions.
</p>
<p>
	In an non-Java context, <a href="http://viaf.org/viaf/5145169">Fowler</a>
	<a href="http://www.worldcat.org/oclc/630586726">says</a> an exception
	is a situation where preconditions are satisfied but postconditions can
	not be satisfied.
</p>
<p>I consider</p>
<ul>
	<li>Runtime exceptions should be used for checking preconditions</li>
	<li>Checked exceptions should be used when preconditions are true
		but postconditions can not be satisfied, assuming that the method is
		correct (e.g. the network connection is broken).&nbsp;</li>
</ul>
<p>
If a runtime exception is raised, the calling method should be bugged
(or its preconditions are not properly checked).
</p>
<p>
	Some extensions to the <i>Java</i> platform provide support for static
	testing (assertions checking at compile time). For example, <a
		href="http://www.eecs.ucf.edu/~leavens/JML/">JML</a> takes advantage
	of <i>Java</i> comments.
</p>