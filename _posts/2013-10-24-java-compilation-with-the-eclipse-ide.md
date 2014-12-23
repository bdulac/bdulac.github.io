--- 
layout: post 
title: Java compilation with the Eclipse IDE and Tomcat
categories:
  - Java
  - AST
  - Eclipse
  - Tomcat
  - JDT
resource: true
---
<p>
You probably have noticed that the <a href="http://www.eclipse.org/">Eclipse IDE</a> does not require a <a href="http://en.wikipedia.org/wiki/Java_Development_Kit">JDK</a> to compile a <em>Java</em> program: this is possible with a simple <a href="http://en.wikipedia.org/wiki/JRE#Execution_environment">JRE</a>.
</p>
<p>
The IDE <a href="http://www.eclipse.org/jdt/">Java Development Tools (JDT)</a> include the appropriate components to compile a program. An <a href="http://www.eclipse.org/articles/article.php?file=Article-JavaCodeManipulation_AST/index.html">AST parser</a> is exposed to help the code manipulation. Compilation is generally defined in two steps : analysis and synthesis. The <a href="http://wiki.eclipse.org/FAQ_What_is_an_AST%3F">AST</a> is the analyzed version of&nbsp; a program organized as a tree connecting declarations and definitions. A specific <a href="http://help.eclipse.org/juno/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Fguide%2Fjdt_int_model.htm">API called the Java model</a> provides an abstraction layer for the AST. The C Development Tools (CDT) <a href="http://www.ibm.com/developerworks/library/os-ecl-cdt3/">also include an AST parser</a>.
</p>
<p>
With such informations, the IDE is in Java able to perform complex operations on the code design. Functions exposed in the <a href="http://help.eclipse.org/juno/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fref-menu-refactor.htm">refactor menu</a> take advantage of the Eclipse AST parser.
</p>
<p>
The compilation performed using the Eclipse AST is reliable. Since tomcat 5.5, it is <a href="http://tomcat.apache.org/tomcat-5.5-doc/jasper-howto.html">used by the Jasper engine to compile JSPs as servlets</a>. This is why, since this version, the servlet container does not require any longer a JDK to run.
</p>
<p>
You should be careful when compiling with Eclipse : there are a few differences when compiling with the JDK (especially on generics transtyping).
</p>