---
layout: post 
title: "SysML Callout and UML"
categories:
  - Stackoverflow
  - UML
  - SysML
resource: true
---
<div>
<p>
Recently, I participated in a <a href="http://stackoverflow.com/q/28084190/1207019">Stackoverflow exchange about the SysML <em>Callout</em> concept</a>. The exchange was started in a wrong direction: the initial question was only about the UML language. This was a misconception as the <em>Callout</em> node is a <a href="http://en.wikipedia.org/wiki/Systems_Modeling_Language">SysML</a> concept and that led to an inappropriate accepted answer which was in fact a non answer.
</p>
<p>
I write this blog post because I think the topic is an important element in modeling. SysML is a UML profile defined in the frame of the OMG. The <a href="http://www.omg.org/spec/SysML/1.3/">SysML 1.3 formal specification</a> poorly defines the term as the effective conceptual definition appears in Annex A, p. 168:
</p>
<pre>The callout notation provides a mechanism for representing relationships between model elements that appear on different diagram kinds.</pre>
<p>
Things become more complex to find the proper way to render a <em>Callout</em>. More indications are available in the <em>Allocation</em> section (p. 129):
</p>
<pre>The allocation relationship can provide an effective means for navigating the model by establishing cross relationships, and ensuring the various parts of the model are properly integrated.</pre>
<p>Later (p. 131):</p>
<pre>An «allocate» property callout uses the same shorthand notation as the «allocate» property compartment. This notation is also shown in Table 15.1.</pre>
<p>Here is the table explaining the notation of allocations:</p>
<img src="/assets/images/allocation.png" style="border-style: solid;" />
<p>
To be synthetic, relationships between model elements that appear on different diagram kinds are an important element of models. But the representation is, in my opinion, not very simple and clear.
</p>
</div>