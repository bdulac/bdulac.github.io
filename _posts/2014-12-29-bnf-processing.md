---
layout: post 
title: "Backus-Naur Form (BNF) processing"
categories:
  - BNF
  - Processing
  - ANTLR
  - ēmaitijǭ
  - Point of view
---
<div itemprop="about" itemscope itemtype="http://schema.org/SoftwareApplication">
<p>
I recently resurrected on my spare time an old idea: a tool to transform a <em>Backus-Naur Form</em> (<a href="http://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form">BNF</a>) grammar to <a href="http://www.antlr.org/">ANTLR</a>. The purpose was to easily generate a parser from an initial BNF. In mind was the conversion of a <a href="http://docs.oracle.com/javaee/6/tutorial/doc/bnbuf.html">JPQL query string</a> (that link shows the initial BNF) to <a href="http://docs.oracle.com/javaee/6/tutorial/doc/gjitv.html">Criteria objects</a>. I was previously surprised not to find such a tool available as open source. Here started <a href="https://github.com/bdulac/emaitijo/">ēmaitijǭ</a>. Simple was the idea, humble was the ambition: at first glance only characters replacements.
</p>
<p>
Limited was my experience in text parsing. A first idea was to convert the grammar of BNF in BNF available in the Wikipedia article to ANTLR in order to generate a parser for the transformation tool itself. A tank to move move a pineapple was my opinion: I chose to process the initial file in a single class. The early ANTLR grammars where generated a few minutes later. Unfortunately, these grammars failed generation with ANTLR with many errors in the output. I had to write a parser: the BNF BNF to ANTLR manual transformation was finally a good option. 
</p>
<p>
A few hours later, my parser did the same job as the single text transformation class. And as many errors in the ANTLR output. I had a look at the JPQL BNF input. Here where is a single mysterious expression that challenged me:
</p>
<pre>{AVG |MAX |MIN |SUM} ([DISTINCT] state_field_path_expression) | COUNT ([DISTINCT] identification_variable | state_field_path_expression | single_valued_association_path_expression)
</pre>
<p>
First problem. <b>I was abused by the parentheses</b>: used to common programming languages, I first considered these characters as grouping symbols, such as in <a href="http://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_Form">Extended BNF</a>: what a mistake, these where literal characters in the expression. 
</p>
<p>
In that section of the expression comes another issue:
</p>
<pre>([DISTINCT] state_field_path_expression)</pre>
<p>Second problem. In <em>Extended</em> BNF, literals are clearly identified with quotes. This is not the rule in standard BNF. <b>How can the parser make the distinction between the parentheses literals and the expressions</b> (<em>[DISTINCT]</em> and <em>state_field_path_expression</em>) because of concatenation ?
</p>
</div>