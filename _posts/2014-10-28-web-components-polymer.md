---
layout: post
title: "Web components and the Polymer project"
categories: 
  - Web
  - Web components
  - W3C
  - Polymer
  - Google
  - Software engineering
resource: true
---

<p>
At 
<span itemprop="about" itemscope itemtype="http://schema.org/Event">
	<meta itemprop="startDate" content="2014-06-24" />
	<meta itemprop="endDate" content="2014-06-26" />
	<span itemprop="name">Google I/O 2014<span>, 
	<span itemprop="subEvent" itemtype="http://schema.org/Event">
		<em><a itemprop="url" href="http://www.youtube.com/watch?v=8OJ7ih8EE7s">Polymer</a></em>
		<meta itemprop="name" content="Polymer and Web Components change everything you know about Web development" />
		<meta itemprop="startDate" content="2014-06-25T01:00" />
		<meta itemprop="endDate" content="2014-06-25T01:45" />
	</span>
	was introduced
	by 
	<span itemprop="performer" itemscope itemtype="http://schema.org/Person" itemid="#bidelman">
		<link itemprop="sameAs" href="https://plus.google.com/+EricBidelman/posts"></link>
		<a itemprop="sameAs" href="https://twitter.com/ebidel">
			<span itemprop="name"> 
				<span itemprop="givenName">Eric</span>
				<span itemprop="familyName">Bidelman</span>.
			</span>
		</a>
	</span>	 
	<span itemprop="organizer" itemscope itemtype="http://schema.org/Organization">
		<meta itemprop="legalName" content="Google inc." />
		<link itemprop="sameAs" href="http://www.google.com"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/Google"></link>
	</span>
</span><em>Polymer</em> is a very interesting move by Google promoting in some way a W3C work: 
<a href="http://www.w3.org/TR/components-intro/">Web components</a>. I try to sum up here all I learned from <a href="https://www.polymer-project.org/docs/start/tutorial/intro.html">the <em>Polymer</em> tutorial</a>.
</p>
<p>
What is the relationship between Web components (as a W3C recommendation) and the <a href="http://polymer-project.org/"><em>Polymer</em> project</a> (as lead by Google) ? In a few words, <em>Polymer</em> bridges the gap between the work pending in the frame of the recommendation working group and the features implemented by browsers. This is done via a simple Javascript, <em>platform.js</em>.
</p>
<p>
Web components are custom HTML tags. <b>How is the behavior and rendering of such elements defined ?</b>
</p>
<p>
The components definition relies on another W3C recommendation, <a href="http://www.w3.org/TR/html-imports/">HTML imports</a>. Introduced as a new <a href="http://www.w3.org/TR/html5/links.html#linkTypes">link type</a>, <em>import</em>, the principle is simple. This allows to include an external resource into an HTML resource. The practice for Web components is to use an included resource to define the behavior of each custom element.
</p>
<p>
One important point is in the naming of custom element. As explained in 
<span itemprop="citation" itemscope itemtype="http://schema.org/Article">
			<a itemprop="sameAs" href="http://webcomponents.org/articles/how-should-i-name-my-element/">
			    that article
				<em><meta itemprop="name" content="How should I name my element?" /></em>
			</a>
			by 
			<span itemprop="author" itemscope itemtype="http://schema.org/Person">
			  <a itemprop="sameAs" href="https://github.com/zenorocha">
				<span itemprop="name">
					<span itemprop="givenName">Zeno</span> 
					<span itemprop="familyName">Rocha</span>
				</span>,
			  </a>
			  <link itemprop="sameAs" href="https://twitter.com/zenorocha"></link>
			</span>
		</span> each name should contain a dash in order to avoid conflicts with standard HTML elements (which are still important because needed in the definition of custom elements).
</p>
<p>
The negative point in using <em>Polymer</em> is that, probably because of the ongoing draft recommendation process, components definition require the use of a <em>Polymer</em>-specific tag. I guess things should evolve here. As a consequence:
</p>
<ul>
	<li>
	If the definition of components becomes standard, <em>Polymer</em>-written components will have to be adapted (a slightest pain if the tag has just to be removed)
	</li>
	<li>
	If the definition of components stays an implementation-specific feature, Web components will be a real mess
	</li>
</ul>
<p>
In the introduction, <link itemprop="sameAs" href="#bidelman">Bidelman</link> states that every framework is compatible with DOM. Indeed, as a result of the document structure simplification induced by Web components, this is a huge change in the way information is provided on the Web. This won't change so much for end users in the first place.
</p>
<p>
On a software engineering point of view, the step could be a real revolution: information provided by the Web server could have a same structure for a Web browser and for any software client. HTML would really look like an XML document, except for the head imports.
</p>
<p>
What will make the real success of Web components is the behavior of software giants. And with <em>Polymer</em>, Google seems to be seriously involved. Could it be a serious move to use Web standards in replacement of any Android API challenged by the <a href="http://www.google.fr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CCEQFjAA&url=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FOracle_v._Google&ei=GoNPVJr-KIfeaM69gsgJ&usg=AFQjCNGcs0490Akq-aklYP09IHZlns9imA&bvm=bv.77880786,d.d2s">Oracle lawsuit</a> ? Perhaps the end of the mobile native / Web apps dichotomy ? Is it a dream ? Still a long way to go for involved engineers, but so many promises...
</p>