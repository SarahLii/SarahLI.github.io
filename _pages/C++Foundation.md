---
layout: archive
title: "C++ Foundation"
permalink: /cpp/
author_profile: true
---
Recording my C++ study process here, and welcome to correct or have a conservation!

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
