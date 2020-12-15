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

Kim, J., Kim, C.\*, Han, H., __Cho, C.J.__, Yeom, W., Lee, S.Q\*, Choi, J.H.\* (2020), A Bird’s Eye View of Brain Activity in
Socially Interacting Mice through Mobile Edge Computing (MEC), **_Science Advances_**, 6(49), eabb9841.


Lee, Y., __Cho, C.J.\*__, Kim, J., Kim, J.H., Han, H., Ahn, W., Choi, J.H. (2020), Investigation of hierarchy-dependency in
the intragroup vigilance convergence and transmission, the 23rd annual meeting of **_the Korean Society for Brain
and Neural Sciences, poster presentation_**. _-- selected as excellent poster_

(\* equal contribution)
