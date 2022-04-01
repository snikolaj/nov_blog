---
layout: page
title: "Featured Projects"
description: "Projects which I particularly enjoyed, am proud of, or are unique"
permalink: /featured/
---
<h3>My featured projects:</h3>
<ul>
{% for project in site.data.category_data.featured_projects %}
<li>
<h4><a href="{{ project.link }}">{{ project.name }}</a></h4>
{{ project.description }}
</li>
<br>
{% endfor %}
</ul>
