--- 
layout: post 
title: "Apple SSL case: code length"
categories:
  - Apple SSL / TLS bug (goto fail)
  - Software quality
  - Software engineering
  - Programming practice
---

<p>
	The point is clearly about programming practice. In February 2014, 
	<a href="http://www.theguardian.com/technology/2014/feb/25/apples-ssl-iphone-vulnerability-how-did-it-happen-and-what-next">Apple faced an SSL bug</a>. This was a very simple code mistake due to 	conditional sequences.
</p>
<p>
	Because of the conditional aspect, we easily focus on curly braces. Two comments suggested the solution to such a problem could be about test cases (both articles provide simple code extracts of the guilty section):
</p>
<ul>
	<li>
		<span itemprop="citation" itemscope itemtype="http://schema.org/BlogPosting">
			<a itemprop="sameAs" href="https://www.imperialviolet.org/2014/02/22/applebug.html">
				Apple's SSL/TLS bug
			</a>
			by 
			<span itemprop="author" itemscope itemtype="http://schema.org/Person">
				<span itemprop="name">Adam Langley</span>
				<link itemprop="sameAs" href="https://github.com/agl"></link>
				<link itemprop="sameAs" href="https://www.imperialviolet.org"></link>
			</span>
		</span>
	</li>
	<li>
		<span itemprop="citation"  itemscope itemtype="http://schema.org/BlogPosting">
			<a itemprop="sameAs" href="https://blog.codecentric.de/en/2014/02/curly-braces/">
				<span itemprop="name">Reflections on Curly Braces</span>
			</a>
			by
			<span itemprop="author" itemscope itemtype="http://schema.org/Person">
				<span itemprop="name">Tobias Goeschel</span>
				<link itemprop="sameAs" href="https://blog.codecentric.de/en/author/tobias-goeschel/"></link>
			</span>
		<span>
	</li>
</ul>
<p>
	For sure, testing is an important point in code quality. In an ideal world there would be a test case for any code piece. For sure, there are excellent other tools. I previously wrote about <a href="http://bdulac.github.io/note/design-by-contract-assertions-and-exceptions/">design by contract</a>.  
	<span itemprop="citation" itemscope itemtype="http://schema.org/ScholarlyArticle">
		Coding a <span itemprop="about">verified program</span>, 
		checking 
			<a itemprop="sameAs" href="http://dx.doi.org/10.1145/363235.363259">
				<span itemprop="author" itemscope itemtype="http://schema.org/Person">
					<span itemprop="name">Hoare</span>
					<link itemprop="sameAs" href="http://viaf.org/viaf/108123782"></link>
				</span>'s
				<span itemprop="about">axioms</span>
			</a>
		is also an important topic.
	</span>
	I won't say any practice is inappropriate.
</p>
<p>
	Stop dreaming about a world with perfect programs. Let the code verification/prove apart and come back to the code. Adam Langley also suggests code reviews are important. Curly braces ? Perhaps the point isn't central. What matter is a <span itemprop="about">readable code</span>. Many programmers write endless code sequences. What could be the solution ?
</p> 
<p>
	We, French people, tend to be very verbose in our texts. At school, we are taught to be concise. We do not succeed in any case. How would it be possible in code ? Think about <a href="https://dev.twitter.com/overview/api/counting-characters">Twitter 140 characters</a>. Just consider what a French journalist <a href="http://www.slate.fr/story/41689/140-signes-twitter-fin-google">could write in 2011</a>. Nowadays, very few journalist still criticize the system. Conciseness can be very useful.  
</p>
<p>
	Why don't compilers warn when a function exceeds 100 lines (or any number that suits you, 100 being quite long) ?
</p>