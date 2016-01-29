---
layout: post 
title: "A Lucene-based map"
categories:
  - Java
resource: true
---
<p>
Last year I needed to store strings in a <em><a href="https://docs.oracle.com/javase/7/docs/api/java/util/Map.html">Java Map</a></em> using a limited memory.
</p>
<p>
The solution was rather simple: using a <em><a href="https://lucene.apache.org/core/">Lucene</a></em> index to store the content on disk. This would provide interesting access performances. Here is the source:
</p>
<p>
<script src="https://gist.github.com/bdulac/2ba47e38b383fb885427.js"></script>
</p>