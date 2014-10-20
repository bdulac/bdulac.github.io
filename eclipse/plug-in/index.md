---
layout: page
title: Eclipse plug-in development
article: true
resource: true
categories:
  - Eclipse
  - Plug-in
---
<div>
<h2>Decode simple JDT signatures</h2>
<p>
The JDT sometimes returns simplified type signatures, for example the <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IMethod.html#getParameterTypes--">IMethod#getParameterTypes()</a></em> method can return values such as <em>QString</em> instead of <em>java.lang.String</em>. To decode such values, the <em><a href="http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FSignature.html">org.eclipse.jdt.core.Signature</a></em> class provides utility functions. <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/Signature.html#getSignatureSimpleName-java.lang.String-">Signature#getSignatureSimpleName(String)</a></em> transforms <em>QString</em> into the simple name, i.e. <em>String</em>. To get the full name, the containing type allows to resolve the simple name. <em><a href="http://help.eclipse.org/juno/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IType.html#resolveType(java.lang.String)">IType#resolveType(String)</a></em> transforms this simple name using the imports of the containing type. The result is an array with two dimensions. The first one is for the case where there are multiple answers possible. The second one separates the name of the package and the simple name. The following code returns the first full name of a method return type.
</p>
<pre>
	String name = method.getReturnType();
	String simpleName = Signature.getSignatureSimpleName(name);
	IType type = method.getTypeRoot();
	String[][] allResults = type.resolveType(simpleName);
	String fullName = null;
	if(allResults != null) {
		String[] nameParts = allResults[0];
		if(nameParts != null) {
			fullName = new String();
			for(int i=0 ; i < nameParts.length ; i++) {
				if(name.length() > 0) {
					name += '.';
				}
				if(nameParts[i] != null) {
					name += nameParts[i];
				}
			}
		}
	}
	return name;</pre>
</div>
<div>
<h2>Programmatically refactor with the JDT</h2>
<p>
Using the internal <a href="http://git.eclipse.org/c/jdt/eclipse.jdt.ui.git/plain/org.eclipse.jdt.ui/core%20refactoring/org/eclipse/jdt/internal/corext/refactoring/rename/">rename package</a> is not a very good idea (discouraged access warning). There is an <a href="http://www.eclipse.org/articles/article.php?file=Article-Unleashing-the-Power-of-Refactoring/index.html">official documentation</a> on that topic. A <a href="http://stackoverflow.com/questions/9129689/is-there-any-eclipse-refactoring-api-that-i-can-call-programmatically">stackoverflow exchange</a> also mentions interesting informations.
</p>
</div>