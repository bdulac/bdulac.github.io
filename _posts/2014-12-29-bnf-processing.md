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
I recently resurrected on my spare time an old idea: a tool to transform a <em>Backus-Naur Form</em> (<a href="http://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form">BNF</a>) grammar to <a href="http://www.antlr.org/">ANTLR</a>. The purpose was to easily generate a parser from an initial BNF grammar. In mind was the conversion of a <a title="This link shows the initial BNF" href="http://docs.oracle.com/javaee/6/tutorial/doc/bnbuf.html">JPQL query string</a> to <a href="http://docs.oracle.com/javaee/6/tutorial/doc/gjitv.html">Criteria objects</a>. I was previously surprised not to find such a grammar conversion tool available as open source. Here started <a itemprop="url" href="https://github.com/bdulac/emaitijo/">ēmaitijǭ</a>. Simple was the idea, humble was the ambition: at first glance only characters replacements.
</p>
<p>
Limited was my experience in text parsing. A first idea was to convert the BNF definition available <a href="http://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form#Further_examples">in the Wikipedia article</a> as a grammar of BNF rules to an ANTLR grammar in order to generate a parser for the transformation tool itself. Such a movement seemed to me too complicated: I chose to process the initial file in a single class. The early ANTLR grammars where generated a few minutes later. Unfortunately, these grammars failed generation with ANTLR with many errors in the output. I finally came back to the idea of a traditional parsing tool but wrote it by myself: the initial ANTLR generation plan would have been the right.
</p>
<p>
A few hours later, my parser did the same job as the single text transformation class. And as a result there where as many errors in the ANTLR output. I had a look at the JPQL BNF input. Here is a single expression that challenged me:
</p>
<pre>{AVG |MAX |MIN |SUM} ([DISTINCT] state_field_path_expression) | COUNT ([DISTINCT] identification_variable | state_field_path_expression | single_valued_association_path_expression)
</pre>
<p>
Reading properly was the first problem. I was <b>abused by the parentheses</b>: used to common programming languages, I first considered these characters as <b>grouping symbols</b>, such as in <a href="http://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_Form">Extended BNF</a>. What a mistake: these where literal characters in the expression. As a consequence, the parser did not read the sequence properly. Just a bug: easy to solve.
</p>
<p>
In the following section of the expression comes another issue:
</p>
<pre>([DISTINCT] state_field_path_expression)</pre>
<p>Syntax was my second problem. In <em>Extended</em> BNF, literals are clearly identified with quotes. This is not the rule in standard BNF. Because of concatenation, <b>how can the parser make the distinction between the parentheses literals and the expressions to be interpreted</b> (in that case <em>[DISTINCT]</em> and <em>state_field_path_expression</em>) ?
</p>
<p>
I did not solve properly that problem and modified the input BNF: just introduced a whitespace after and before each parenthesis. After all, ēmaitijǭ was probably not a very good idea in the first place.
<span itemscope itemtype="http://schema.org/ScholarlyArticle">
  <span itemprop="author" itemscope itemtype="http://schema.org/Person">
    <a href="http://en.wikipedia.org/wiki/Donald_Knuth">Donald Knuth</a>
    <link itemprop="sameAs" href="http://en.wikipedia.org/wiki/Donald_Knuth" />
    <meta itemprop="givenName" content="Donald" />
    <meta itemprop="familyName" content="Knuth" />
  </span>
  <link itemprop="sameAs" href="http://dx.doi.org/10.1145/355588.365140" />
  <a href="http://dx.doi.org/10.1145/355588.365140">
    said
  </a>
</span>
about the form of BNF that it was <em> "not a normal form in the conventional sense"</em>. This is probably why such a tool was not available online before. A main problem is that there is no strict definition of BNF.
</p>
<p>
BNF is largely more used than EBNF in formal definitions. Is the literal limitation a real problem ? As a conclusion, if it was definitely stated that <b>literals and other expression terms should be delimited with whitespaces</b> (instead of quotes or anything else), wouldn't it simplify the use of BNF for anyone ? Well, I hear the coming problem: it wouldn't be possible to express whitespaces in a grammar. But is there a real need to specify sharply whitespaces in a grammar ? The background problem is that BNF grammar definition, because of its origins, is fuzzy and its current use is approximative.
</p>
</div>
