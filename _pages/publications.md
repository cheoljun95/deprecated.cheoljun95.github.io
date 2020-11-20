---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}

Kim, J., Kim, C.*, Han, H., Cho, C.J., Yeom, W., Lee, S.Q*, Choi, J.H.*, A Bird’s Eye View of Brain Activity in
Socially Interacting Mice through Mobile Edge Computing (MEC), Science Advances, In press (2020)

Lee, Y. Cho, C.J.*, Kim, J., Kim, J.H., Han, H., Ahn, W., Choi, J.H., Investigation of hierarchy-dependency in
the intragroup vigilance convergence and transmission, the 23rd annual meeting of the Korean Society for Brain
and Neural Sciences, poster presentation (2020), selected as excellent poster (* equal contribution)
