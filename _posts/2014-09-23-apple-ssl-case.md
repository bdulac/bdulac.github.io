--- 
layout: post 
title: "Apple SSL case: code length"
categories:
  - Software quality
  - Software engineering
  - Programming practice
---

<p>
	The point is clearly about programming practice... In February 2014, Apple faced an SSL bug. This was a very simple code mistake due to 	conditional sequences.
</p>
<p>
	The thoughts easily focus on curly braces. Two comments suggested the solution could be about test cases (Tobias Goeschel provides a very simple code extract of the guilty section):
</p>
<ul>
	<li>
		<span itemscope itemtype="http://schema.org/BlogPosting">
		<link itemprop="sameAs" href="https://blog.codecentric.de/en/2014/02/curly-braces/"></link>
		<a href="https://blog.codecentric.de/en/2014/02/curly-braces/">
			<span itemprop="author" itemscope itemtype="http://schema.org/Person">
				<span itemprop="name">Tobias Goeschel</span>
				<link itemprop="sameAs" href="https://blog.codecentric.de/en/author/tobias-goeschel/"></link>
			</span>
		</a>
		<span>
	</li>
	<li>
		<span itemscope itemtype="http://schema.org/BlogPosting">
		<link itemprop="sameAs" href="https://www.imperialviolet.org/2014/02/22/applebug.html"></link>
		<a href="https://www.imperialviolet.org/2014/02/22/applebug.html">
			<span itemprop="author" itemscope itemtype="http://schema.org/Person">
				<span itemprop="name">Adam Langley</span>
				<link itemprop="sameAs" href="https://github.com/agl"></link>
				<link itemprop="sameAs" href="https://www.imperialviolet.org"></link>
			</span>
		</a>
		</span>
	</li>
</ul>
<p>
	For sure, testing is an important point in code quality. But this is an utopia: in a 
ideal world there would be a test case for any code piece. For sure, there are excellent other tools, I previously wrote about <a href="http://bdulac.github.io/note/design-by-contract-assertions-and-exceptions/">design by contract</a>.  
	<span itemscope itemtype="http://schema.org/ScholarlyArticle">
		Writing a <span itemprop="about">verified program</span>, 
		checking 
			<a itemprop="sameAs" href="http://dx.doi.org/10.1145/363235.363259">
				<span itemprop="about">axioms</span>
			</a>
		is an important topic. 
	</span>. 
	I won't say any practice is inappropriate.
</p>
<p>
	Stop dreaming about a world with perfect programs. Let the code verification/prove apart and come back to the code. Adam Langley also suggests code reviews are important. Curly braces ? Perhaps the point isn't central. What matter is a readable code, and others point of view. Many programmers write endless code sequences. What could be the solution ?
</p> 
<p>
	We, French people, tend to be very verbose in our texts. At school, we are taught to be concise. We do not succeed in any case. How would it be possible in code ? Think about <a href="https://dev.twitter.com/overview/api/counting-characters">Twitter 140 characters</a>. Just think about what a French journalists  <a href="http://www.slate.fr/story/41689/140-signes-twitter-fin-google">could write in 2011</a>. Nowadays, very few journalist still criticize the system. Conciseness can be very useful.  
</p>
<p>
	Why don't compilers warn when a function exceeds 100 lines (or any number that suits you) ?
</p>