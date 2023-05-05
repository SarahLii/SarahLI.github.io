---
layout: archive
title: "C++ Foundation"
permalink: /C++Foundation/
author_profile: true
---
% modify this from Publication
{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
