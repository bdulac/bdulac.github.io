--- 
layout: post 
title: ! 'Point of view: Packaging' 
categories:
  - Package
  - Software engineering
  - Software design
  - UML
  - Point of view
resource: true
---
<p>
According to the <a href="http://www.worldcat.org/oclc/39516151">UML user guide</a>, object-oriented software elements belong to four	categories :
</p>
<p>
<ul>
	<li>Structural things</li>
	<li>Behavioral things</li>
	<li>Grouping things</li>
	<li>Notational things</li>
</ul>
<p>
Obviously, classes are structural elements. According to this same book, <a href="http://en.wikipedia.org/wiki/Package_%28UML%29">packaging</a> is the act of grouping classes.
</p>
<p>
Something is bothering me about packaging. All programs I have been working on, and all courses I have been following, share a single vision of the way these groups should be considered.
</p>
<p>
In this single vision, classes are grouped on structural criteria. In a same package, we will find objects assuming a single role. This helps designing interesting <a href="http://en.wikipedia.org/wiki/Class_diagram">class</a> diagrams. To be honest, this has a real interest to build effective heritage hierarchies.
</p>
<p>
But in my point of view, we let apart behavioral criteria. This means, if we design <a href="http://en.wikipedia.org/wiki/Sequence_diagram">sequence</a>, <a href="http://en.wikipedia.org/wiki/Activity_diagram">activity</a> or <a href="http://en.wikipedia.org/wiki/State_diagram_%28UML%29">state</a> diagrams, the involved objects will belong to different packages.
</p>
<ol>
	<li><b>Usually</b>, package grouping is based on <b>classes roles</b></li>
	<li>Package grouping should also be based on <b>classes interactions</b></li>
</ol>
<p>
If we would like to design really modular applications, I think we should consider these two axes in packaging. On a pure design point of view, a class should belong to two packages : one structural (1) and one behavioral (2). This could be possible because one class usually has interactions with a few classes.
</p>
<p>
In <em>Java</em>, one solution to help set up this second kind of packages could be annotations. But the problem would be in class loading. This wouldn't be a real problem if we all time use to <a href="http://dx.doi.org/10.1145/1176617.1176622">write APIs</a>.
</p>