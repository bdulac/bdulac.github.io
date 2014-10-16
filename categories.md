---
layout: page
title: Categories
permalink: /categories/
---
<div>
<p>
These categories are detailing specific subjects. Each individual page don't try to be a documentation, only a gathering of relative posts enriched with some static content.
</p>
<ul>
{% for myPage in site.pages %}
	{% if myPage.categoryPage != null %}
	<li><a href="{{ myPage.url }}">{{ myPage.categoryPage }}</a></li>
	{% endif %}
{% endfor %}
</ul>
</div>