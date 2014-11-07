--- 
layout: post 
title: 'Eclipse JDT: how to go from an IJavaElement to an ASTNode ?'
categories:
  - Java
  - AST
  - Eclipse
  - JDT
resource: true
--- 
<p>
I previously wrote about <a href="http://bdulac.github.io/note/java-compilation-with-the-eclipse-ide/"><em>Java</em> compilation with the Eclipse IDE</a>. The JDT include several representations of the language components.
</p>
<ul>
    <li>
    	The <a href="http://www.eclipse.org/articles/article.php?file=Article-JavaCodeManipulation_AST/">AST</a> is a sharp representation of programs used for compilation
    </li>
	<li>The <a href="http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Fguide%2Fjdt_int_model.htm">Java model</a> is a more abstract object representation of the Java elements 
	</li>
</ul>
<p>
I needed to get the Javadoc text for a Java element. Unfortunately, the method to retrieve attached Javadoc <a href="http://help.eclipse.org/indigo/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FIJavaElement.html">always return null</a> for source documents. Therefore I needed to go from the <a href="http://help.eclipse.org/indigo/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FIJavaElement.html">IJavaelement</a> interface to the <a href="http://help.eclipse.org/juno/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FASTNode.html">ASTNode</a> representation. The <a href="https://wiki.eclipse.org/JDT/FAQ#From_an_IJavaElement_to_its_declaring_ASTNode">official documentation</a> is a bit light on that point: a first step is to get the proper compilation unit. Here is the final code:   
</p>
<pre>		// Fetch the Java model compilation unit
		ICompilationUnit cUnit = javaElement.getCompilationUnit();
		// Note the simple name of the java element in the compilation unit
		String simpleName = javaElement.getElementName();
		// Parse the source
		ASTParser parser = ASTParser.newParser(AST.JLS3);
		parser.setSource(cUnit);
		parser.setResolveBindings(true);
		// Fetch the AST node for the compilation unit
		ASTNode unitNode = parser.createAST(new NullProgressMonitor());
		// It should be an AST compilation unit
		if(unitNode instanceof CompilationUnit) {
			CompilationUnit sourceUnit = (CompilationUnit)unitNode;
			ASTNode elementNode = findDeclaringNode(simpleName);
		}</pre>