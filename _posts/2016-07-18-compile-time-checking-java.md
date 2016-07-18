---
layout: post
title: Compile-time checking in Java
categories:
  - Java
  - Software quality
  - Software engineering
  - Programming practice
resource: true
---
<p>
In a <a href="http://bdulac.github.io/note/apple-ssl-case">previous post</a> I wrote about code quality: in a few words, I believe in <span itemprop="about"><a itemprop="sameAs" href="http://en.wikipedia.org/wiki/Static_program_analysis">static-checking</a></span>. Static means without executing the program. In a software process point of view, this would imply before runtime, in other words at compile-time. For a developer, it can be very useful to have such a verification simply with a compilation, without executing a specific tool (by the way, some very interesting software of that kind are available, just <a href="http://findbugs.sourceforge.net/">Findbugs</a> for example).
</p>
<p>
Here is the point: how would it be possible to proceed that kind of control without rewriting a compiler from scratch ?
</p>
<p>
The <b><em><a href="http://bdulac.github.io/java/">Java</a></em></b> platform provides a very interesting feature to perform such operations: <a href="http://docs.oracle.com/javase/tutorial/java/annotations/">annotations</a> (<a href="https://www.jcp.org/en/jsr/detail?id=175">JSR 175</a>). These are metadata <a href="http://docs.oracle.com/javase/tutorial/java/annotations/declaring.html">defined as java types</a>. Annotations have been introduced in the Java language starting with Java SE 5. <b>Annotations</b> can be processed at <b>compile-time</b> or runtime.
</p>
<!--
<p>
@see https://blogs.oracle.com/java-platform-group/entry/java_8_s_new_type
</p>
-->
<p>
The Sun Java SE distribution provided from the starting point a facility for annotation processing at compile-time called <a href="http://docs.oracle.com/javase/1.5.0/docs/guide/apt/">APT</a> (for Annotation Processing Tool). This was a vendor-specific feature (in <em>Sun</em> packages) executed in a specific and eponymous command line tool.
</p>
<p>
Since Java 6, that function is part of the platform with <a href="https://www.jcp.org/en/jsr/detail?id=269">JSR 269</a> (<em><a href="http://docs.oracle.com/javase/6/docs/api/javax/annotation/processing/package-summary.html">javax.annotation.processing</a></em> package, reference implementation part of the <a href="https://jcp.org/aboutJava/communityprocess/mrel/jsr269/index2.html">Java SE</a> distribution). The contributed processing can be executed along compilation. With Java SE 8, the historical APT packaging and specific tool <a href="http://openjdk.java.net/jeps/117">is removed</a> (after <a href="docs.oracle.com/javase/7/docs/technotes/guides/apt/">deprecation in Java SE 7</a>).
</p>
<p>
If the topic seems basic for the Java platform, there is a lack of exhaustive documentation for annotation processors development. I found some precious informations in  
<span itemprop="citation" itemscope itemtype="http://schema.org/BlogPosting">
	<a itemprop="url" href="http://kerebus.com/2011/02/using-java-6-processors-in-eclipse/">
		<em>Using Java 6 processors in Eclipse</em>
	</a>
	, a blog post by  
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<a itemprop="sameAs" href="https://github.com/kallebertell">
			<span itemprop="name">
				<span itemprop="givenName">Carl-Petter</span>
				<span itemprop="familyName">Bertell</span>
			</span>
		</a>
		<link itemprop="sameAs" href="http://kerebus.com" />
	</span>
</span>.
The <a href="../eclipse/platform/">Eclipse platform</a> provide very precious functions with the <a href="http://www.eclipse.org/jdt/apt/">JDT-APT project</a>.
</p>
<p>
<span itemprop="citation" itemscope itemtype="http://schema.org/Creativework">
A very interesting
	<a itemprop="url" href="http://www.eclipse.org/jdt/apt/eclipsecon2007.zip">
		<span itemprop="learningResourceType">presentation</span>
		at EclipseCon 2007
	</a>
	by
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<span itemprop="name">
			<span itemprop="givenName">Walter</span>
			<span itemprop="familyName">Harley</span>
		</span>,
	</span>
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<span itemprop="name">
			<span itemprop="givenName">Gary</span>
			<span itemprop="familyName">Horen</span>
		</span>
	</span> and
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<span itemprop="name">
			<span itemprop="givenName">Jess</span>
			<span itemprop="familyName">Garms</span>
		</span>
	</span>
	from
	<span itemprop="author" itemscope itemtype="http://schema.org/Organization">
		<a itemprop="sameAs" href="http://en.wikipedia.org/wiki/BEA_Systems">
			<span itemprop="legalName">BEA systems</span>
		</a>
	</span> develops many important points about compile-time checking: what could be done with annotation processors and what requires more. For example, the processor does not provide the structure of the <a href="http://en.wikipedia.org/wiki/Abstract_syntax_tree">AST</a> and thereby does not allow flow analysis.
</span>
</p>
<p>
A <b>processor</b> must implement the <b><em><a href="http://docs.oracle.com/javase/8/docs/api/javax/annotation/processing/Processor.html">javax.annotation.processing.Processor</a></em> interface</b>. The implementation should be <b>specified</b> to the platform <b>using the <a href="http://bdulac.github.io/note/spi">SPI</a></b> system. An abstract class <em><a href="http://docs.oracle.com/javase/8/docs/api/javax/annotation/processing/AbstractProcessor.html">AbstractProcessor</a></em> is provided to help implementations.
</p>
<p>
  In a
<span itemprop="citation" itemscope itemtype="http://schema.org/BlogPosting">
	<a itemprop="url" href="http://www.alexecollins.com/java-annotation-processor-tutorial/">
		tutorial about annotation processing,
	</a>
	<span itemprop="author" itemscope itemtype="http://schema.org/Person">
		<a itemprop="sameAs" href="https://github.com/alexec">
			<span itemprop="name">
				<span itemprop="givenName">Alex</span>
				<span itemprop="familyName">Collins</span>
			</span>
		</a>
		<link itemprop="sameAs" href="http://www.alexecollins.com" />
    details the
    <span itemprop="about">implementation of a compile-time processor</span>  
    for the
      <a
        itemprop="about" href="http://docs.spring.io/autorepo/docs/spring/4.2.x/javadoc-api/org/springframework/transaction/annotation/Transactional.html">
        @Transactional annotation of the spring framework
      </a>.
	  </span>
  </span>
</p>
