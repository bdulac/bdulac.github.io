---
layout: post
title: "Decoding simple JDT signatures"
categories:
  - Eclipse platform
  - Java
resource: true
---
<p>
The JDT sometimes returns simplified type signatures, for example the <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IMethod.html#getParameterTypes--">IMethod#getParameterTypes()</a></em> method can return values such as <em>QString</em> instead of <em>java.lang.String</em>.
</p>
<p>
To decode such values, the <em><a href="http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2FSignature.html">org.eclipse.jdt.core.Signature</a></em> class provides utility functions. <em><a href="http://help.eclipse.org/luna/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/Signature.html#getSignatureSimpleName-java.lang.String-">Signature#getSignatureSimpleName(String)</a></em> transforms <em>QString</em> into the simple name, i.e. <em>String</em>.
</p>
<p>To get the full name, the containing type allows to resolve the simple name. <em><a href="http://help.eclipse.org/juno/topic/org.eclipse.jdt.doc.isv/reference/api/org/eclipse/jdt/core/IType.html#resolveType(java.lang.String)">IType#resolveType(String)</a></em> transforms this simple name using the imports of the containing type. The result is an array with two dimensions. The first one is for the case where there are multiple answers possible. The second one separates the name of the package and the simple name.
</p>
<p>
The following code returns the first full name of a method return type:
</p>
<pre>
	String name = method.getReturnType();
	String simpleName = Signature.getSignatureSimpleName(name);
	IType type = method.getDeclaringType();
	String[][] allResults = type.resolveType(simpleName);
	String fullName = null;
	if(allResults != null) {
		String[] nameParts = allResults[0];
		if(nameParts != null) {
			fullName = new String();
			for(int i=0 ; i < nameParts.length ; i++) {
				if(fullName.length() > 0) {
					fullName += '.';
				}
				if(nameParts[i] != null) {
					fullName += nameParts[i];
				}
			}
		}
	}
	return name;</pre>
<p>
An <a href="http://stackoverflow.com/a/27777064/1207019">exchange on stackoverflow</a> details the code for parameters types full names.
</p>
