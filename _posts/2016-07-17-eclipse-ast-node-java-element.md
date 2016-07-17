---
layout: post
title: 'Eclipse JDT: get the ASTNode from an IJavaElement'
categories:
  - Eclipse platform
  - JDT
  - Java
  - AST
resource: true
---
<p>
I previously wrote about <a href="http://bdulac.github.io/note/java-compilation-with-the-eclipse-ide"><em>Java</em> compilation with the Eclipse IDE</a>. The JDT include several representations of the language components:
</p>
<ul>
    <li>
    	The <a href="http://www.eclipse.org/articles/article.php?file=Article-JavaCodeManipulation_AST/">AST</a> is a sharp representation of programs used for compilation
    </li>
	<li>The <a href="http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Fguide%2Fjdt_int_model.htm">Java model</a> is a more abstract object representation of the Java elements
	</li>
</ul>
<p>
For a specific purpose I recently needed to get the Javadoc text for a Java element. Unfortunately, the method to retrieve attached Javadoc <a href="http://help.eclipse.org/indigo/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FIJavaElement.html">always return null</a> for source documents. Therefore I needed to go from the <em><a href="http://help.eclipse.org/indigo/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FIJavaElement.html">IJavaelement</a></em> interface to the <em><a href="http://help.eclipse.org/juno/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FASTNode.html">ASTNode</a></em> representation. The <a href="https://wiki.eclipse.org/JDT/FAQ#From_an_IJavaElement_to_its_declaring_ASTNode">official documentation</a> is a bit light on that point: a first step is to get the proper compilation unit. This is possible via the <em><a href="http://help.eclipse.org/indigo/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FIMember.html">IMember</a></em> interface. Here is the final code:   
</p>
<p>
<script src="https://gist.github.com/bdulac/62954848149321f1d39924d1e0405994.js"></script>
</p>
