---
title: Publications
layout: academic
author_profile: true
---

<!-- selectors -->
<aside class="sidebar__control sticky">
  <p><div class="btn btn--selected select-all">Show all</div></p>
  <p>{% for v in site.data.categories.publications.types %}<div class="btn btn--unselected select-type-{{ v.id }}">{{ v.name }}</div>{% endfor %}</p>
  <p>{% for v in site.data.categories.publications.authorship %}<div class="btn btn--unselected select-type-{{ v.id }}">{{ v.name }}</div>{% endfor %}</p>
  <p>{% for v in site.data.categories.publications.status %}<div class="btn btn--unselected select-type-{{ v.id }}">{{ v.name }}</div>{% endfor %}</p>
</aside>

<!-- slider for years -->

<script src="https://cdnjs.cloudflare.com/ajax/libs/noUiSlider/12.0.0/nouislider.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/noUiSlider/12.0.0/nouislider.min.css"/>
<div id="slider"></div>
<script>
var slider = document.getElementById('slider');
noUiSlider.create(slider, {
    start: [20, 80],
    step: 1,
    tooltips: [true, true]
    connect: true,
    range: {
        'min': [2016],
        'max': [2021]
    }
});
</script>

<!-- listing -->
{% for yr in site.data.categories.publications.years %}
<h2 id="year-{{ yr }}">{{ yr }}</h2>
<ul>
{% for ms in site.data.publications %}{% if ms.year == yr %}
  <li class="publ-type-{{ ms.type }} publ-auth-{{ ms.authorship }} publ-status-{{ ms.status }}">
    {{ ms.text }}{% if ms.preprint %}&mdash; <a href="{{ ms.preprint }}">Preprint</a>{% endif %}{% if ms.datarepo %}&mdash; <a href="{{ ms.datarepo }}">Data repository</a>{% endif %}{% if ms.rpackagename %}&mdash; <a href="{{ ms.rpackagelink }}">{{ ms.rpackagename }}</a>{% endif %}{% if ms.webappname %}&mdash; <a href="{{ ms.webapplink }}">{{ ms.webappname }}</a>{% endif %}{% if ms.doi %} <div data-badge-popover="bottom" style="display: inline-block;" data-badge-type="4" data-doi="{{ ms.doi }}" data-hide-no-mentions="true" class="altmetric-embed"></div>{% endif %}
    </li>
{% endif %}{% endfor %}
</ul>
{% endfor %}
<script type='text/javascript' src='https://d1bxh8uas1mnw7.cloudfront.net/assets/embed.js'></script>
