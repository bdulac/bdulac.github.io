--- 
layout: post 
title: "Apple SSL case: code length"
categories:
  - Software quality
  - Software engineering
  - Programming
  - Practice
---

<p>
	In February 2014, Apple faced an SSL bug. This was a very simple code mistake due to 	conditional sequences.
</p>
<p>
	The point is for sure about programming practice... The thoughts easily focus on curly braces. Two comments suggested the solution could be about test cases (Tobias Goeschel provides a very simple code extract):
</p>
<ul>
	<li><a href="https://blog.codecentric.de/en/2014/02/curly-braces/">Tobias Goeschel</a></li>
	<li><a href="https://www.imperialviolet.org/2014/02/22/applebug.html">Adam Langley</a></li>
</ul>
<p>
	For sure, testing is an important point in code quality. But this is an endless debate: in a 
ideal world there would be a test case for any code piece. "Program testing can be used to show the presence of bugs, but never to show their absence!" said <a href="http://viaf.org/viaf/17820452">Edsger Dijkstra</a> in 
<a href="http://dx.doi.org/10.1145/355604.361591">The humble programmer</a>. 
For sure, there are excellent tools to make a right program, just <a href="http://dx.doi.org/10.1145/363235.363259">one kind</a> for example. I won't say any practice is inappropriate.
</p>
<p>
	Stop dreaming. Let the code verification/prove apart and come back to the code. Adam Langley also suggest code reviews are important. Curly braces ? Perhaps the point isn't central. What matter is a readable code, and others point of view. Many programmers write endless code sequences. What could be the solution ?
</p> 
<p>
	We, French people, tend to be very verbose in our texts. At school, we are taught to be concise. We do not succeed in any case. How would it be possible in code ? Think about <a href="https://dev.twitter.com/overview/api/counting-characters">Twitter 140 characters</a>. Just think about what a French journalists  <a href="http://www.slate.fr/story/41689/140-signes-twitter-fin-google">could write in 2011</a>. Nowadays, very few journalist still criticize the system. Conciseness can be very useful.  
</p>
<p>
	Why don't compilers warn when a function exceeds 100 lines ?
</p>