---
layout: post
title: Tests
categories:
  - Software engineering
  - Software quality
  - Programming practice
  - Tests
---
<div itemprop="citation" itemscope itemtype="http://schema.org/ScholarlyArticle">
<p>
"Program testing can be used to show the presence of bugs, but never to show their absence!" said
	<link itemprop="sameAs" href="http://dx.doi.org/10.1145/355604.361591" />
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<a itemprop="sameAs" href="http://viaf.org/viaf/17820452">
			<span itemprop="name">
				<span itemprop="givenName">Edsger</span>
				<span itemprop="familyName">Dijkstra</span>
			</span>
		</a>
	</span>
		in
		<a href="http://dx.doi.org/10.1145/355604.361591">
			<span itemprop="name">The humble programmer.</span>
		</a>
The proposed alternative is following:
"The only effective way to raise the confidence level of a program significantly is to give a convincing proof of its correctness."
This was in
<span itemprop="copyrightYear">1972</span>.
</p>
</div>
<p>
Well, if the proof of a program has to be made, this would be at compile time. Since then, there has been
<a href="http://dl.acm.org/results.cfm?query=static%20checking">some works about static checking</a>. But what is the popularity in <a href="http://www.google.com/trends/explore#q=static%20checking%2C%20unit%20testing&cmpt=q">comparison</a> with testing ?
</p>
<p>
<a href="http://en.wikipedia.org/wiki/Black-box_testing">Black Box</a> / functional testing
<br />
<a href="http://en.wikipedia.org/wiki/White-box_testing">White Box</a> / structural testing
</p>
<p>
	I previously wrote about taking advantage of the design by contract  
	<span itemprop="citation" itemscope itemtype="http://schema.org/BlogPosting">
		<a itemprop="sameAs" href="{{ site.url }}/note/design-by-contract-assertions-and-exceptions">
			in the use of exceptions
		</a>
	</span>.
</p>
