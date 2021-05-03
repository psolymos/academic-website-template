---
title: Publications
layout: academic
author_profile: true
---

Selectors will come here:

- Years: {% for y in site.data.categories.publications.years %} {{ y }}{% endfor %}
- Types: {% for ty in site.data.categories.publications.types %} {{ ty }}{% endfor %}
- Authorship: {% for au in site.data.categories.publications.authorship %} {{ au }}{% endfor %}
- Types: {% for st in site.data.categories.publications.status %} {{ st }}{% endfor %}

{% for yr in site.data.categories.publications.years %}
<h2 id="year-{{ yr }}">{{ yr }}</h2>
<ul>
{% for ms in site.data.publications %}{% if ms.year == yr %}
  <li class="publ-type-{{ ms.type }} publ-auth-{{ ms.authorship }} publ-status-{{ ms.status }}">
    {{ ms.text }}{% if ms.preprint %}&mdash; <a href="{{ ms.preprint }}">Preprint</a>{% endif %}{% if ms.datarepo %}&mdash; <a href="{{ ms.datarepo }}">Data repository</a>{% endif %}{% if ms.rpackagename %}&mdash; <a href="{{ ms.rpackagelink }}">{{ ms.rpackagename }}</a>{% endif %}{% if ms.webappname %}&mdash; <a href="{{ ms.webapplink }}">{{ ms.webappname }}</a>{% endif %}{% if ms.doi %}<div data-badge-popover="bottom" style="display: inline-block;" data-badge-type="4" data-doi="{{ ms.doi }}" data-hide-no-mentions="true" class="altmetric-embed"></div>{% endif %}
    </li>
{% endif %}{% endfor %}
</ul>
{% endfor %}
<script type='text/javascript' src='https://d1bxh8uas1mnw7.cloudfront.net/assets/embed.js'></script>
