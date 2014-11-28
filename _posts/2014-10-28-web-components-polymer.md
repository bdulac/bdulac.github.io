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
	<span itemprop="name">Google I/O 2014</span>, 
	<span itemprop="subEvent" itemtype="http://schema.org/Event">
		<em><a href="http://www.youtube.com/watch?v=8OJ7ih8EE7s">Polymer</a></em>
		<meta itemprop="url" content="http://www.youtube.com/watch?v=8OJ7ih8EE7s" />
		<meta itemprop="name" content="Polymer and Web Components change everything you know about Web development" />
		<meta itemprop="startDate" content="2014-06-25T01:00" />
		<meta itemprop="endDate" content="2014-06-25T01:45" />
	</span>
	was introduced in deep 
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
	<span itemprop="organizer" itemscope itemtype="http://schema.org/Organization" itemid="#goog">
		<meta itemprop="legalName" content="Google inc." />
		<link itemprop="sameAs" href="http://www.google.com"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/Google"></link>
	</span>
</span>
<span itemprop="about" itemscope itemtype="http://schema.org/Code">
	<em>Polymer</em>
	<meta itemprop="url" content="https://www.polymer-project.org/" />
	<meta itemprop="codeRepository" content="https://github.com/Polymer/">
	is a very interesting move by 
	<meta itemprop="author">
		<link itemprop="sameAs" href="#goog">Google</link>
	</meta>
</span> 
promoting in some way a W3C work: 
<span itemprop="about" itemscope itemtype="http://schema.org/TechArticle">
	<a href="http://www.w3.org/TR/custom-elements/">Web components.</a>
	<meta itemprop="url" content="href="http://www.w3.org/TR/custom-elements/" />
	<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/Web_Components" />
	<span itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
		<meta itemprop="legalName" content="World Wide Web Consortium" />
		<link itemprop="sameAs" href="http://www.w3.org/"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/World_Wide_Web_Consortium"></link>
	</span>
</span>
I try to sum up here all I learned from <a href="https://www.polymer-project.org/docs/start/tutorial/intro.html">the <em>Polymer</em> tutorial</a>.
</p>
<p>
What is the relationship between Web components (as a W3C recommendation) and the <a href="http://polymer-project.org/"><em>Polymer</em> project</a> (as lead by Google) ? In a few words, <em>Polymer</em> bridges the gap between the work pending in the frame of the recommendation working group and the features implemented by browsers. This is done via a simple Javascript, <em>platform.js</em>.
</p>
<p>
Web components are custom HTML tags. <b>How is the behavior and rendering of such elements defined ?</b>
</p>
<p>
The components definition relies by convenience on another W3C recommendation, 
<span itemprop="citation" itemscope itemtype="http://schema.org/TechArticle">
	<a href="http://www.w3.org/TR/html-imports/">HTML imports.</a>
	<meta itemprop="url" content="http://www.w3.org/TR/html-imports/" />
	<span itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
		<meta itemprop="legalName" content="World Wide Web Consortium" />
		<link itemprop="sameAs" href="http://www.w3.org/"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/World_Wide_Web_Consortium"></link>
	</span>
</span>
Introduced as a new <span itemprop="citation" itemscope itemtype="http://schema.org/TechArticle">
	<a href="http://www.w3.org/TR/html5/links.html#linkTypes">link type</a>
	<meta itemprop="url" content="http://www.w3.org/TR/html5/links.html#linkTypes" />
	<span itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
		<meta itemprop="legalName" content="World Wide Web Consortium" />
		<link itemprop="sameAs" href="http://www.w3.org/"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/World_Wide_Web_Consortium"></link>
	</span>
</span> (<em>import</em>) the principle is simple. This allows to include an external resource into an HTML resource. The practice for Web components is to use an included resource defining the behavior of each custom element in order to allow reuse of that definition. Web components could of course be defined without imports but this would be of limited interest.
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
				<a itemprop="sameAs" href="https://twitter.com/zenorocha">
						<span itemprop="name">
						<span itemprop="givenName">Zeno</span> 
						<span itemprop="familyName">Rocha</span>
					</span>,
			  	</a>
			  	<link itemprop="sameAs" href="https://github.com/zenorocha"></link>
			  	<span itemprop="memberOf" itemscope itemtype="http://schema.org/Organization" itemid="#goog">
					<meta itemprop="legalName" content="Liferay, Inc." />
					<link itemprop="sameAs" href="http://www.liferay.com/"></link>
				</span>
				<span itemprop="memberOf" itemscope itemtype="http://schema.org/Organization" itemid="#goog">
					<meta itemprop="legalName" content=" Google Developer Experts program" />
					<link itemprop="sameAs" href="https://developers.google.com/experts/"></link>
				</span>
			</span>
		</span> each name should contain a dash in order to avoid conflicts with standard HTML elements (which are still important because needed in the definition of custom elements).
</p>
<p>
In the introduction, <link itemprop="sameAs" href="#bidelman">Bidelman</link> states that every framework is compatible with 
<span itemprop="citation" itemscope itemtype="http://schema.org/TechArticle">
	<a href="http://www.w3.org/DOM/#what">DOM</a>
	<meta itemprop="url" content="http://www.w3.org/DOM/#what" />
	<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/Document_Object_Model#cite_note-Introduction-1" />.
	<span itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
		<meta itemprop="legalName" content="World Wide Web Consortium" />
		<link itemprop="sameAs" href="http://www.w3.org/"></link>
		<link itemprop="sameAs" href="http://en.wikipedia.org/wiki/World_Wide_Web_Consortium"></link>
	</span>
</span>
Indeed, as a result of the document structure simplification induced by Web components, this is a huge change in the way information is provided on the Web. This won't change so much for end users in the first place.
</p>
<p>
On a software engineering point of view, the step could be a real revolution: information provided by the Web server could have a same structure for a Web browser and for any software client. HTML would really look like an XML document, except for the head imports.
</p>
<p>
What will make the real success of Web components is the behavior of software giants. And with <em>Polymer</em>, Google seems to be seriously involved. Could it be a serious move to use Web standards in replacement of any Android API challenged by the <a href="http://www.google.fr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CCEQFjAA&url=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FOracle_v._Google&ei=GoNPVJr-KIfeaM69gsgJ&usg=AFQjCNGcs0490Akq-aklYP09IHZlns9imA&bvm=bv.77880786,d.d2s">Oracle lawsuit</a> ? Perhaps the end of the mobile native / Web apps dichotomy ? Is it a dream ? Still a long way to go for involved engineers, but so many promises...
</p>