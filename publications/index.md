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
<style>
[slider] {
  width: 300px;
  position: relative;
  height: 5px;
  margin: 45px 0 10px 0;
}

[slider] > div {
  position: absolute;
  left: 13px;
  right: 15px;
  height: 5px;
}
[slider] > div > [inverse-left] {
  position: absolute;
  left: 0;
  height: 5px;
  border-radius: 10px;
  background-color: #CCC;
  margin: 0 7px;
}

[slider] > div > [inverse-right] {
  position: absolute;
  right: 0;
  height: 5px;
  border-radius: 10px;
  background-color: #CCC;
  margin: 0 7px;
}


[slider] > div > [range] {
  position: absolute;
  left: 0;
  height: 5px;
  border-radius: 14px;
  background-color: #d02128;
}

[slider] > div > [thumb] {
  position: absolute;
  top: -7px;
  z-index: 2;
  height: 20px;
  width: 20px;
  text-align: left;
  margin-left: -11px;
  cursor: pointer;
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.4);
  background-color: #FFF;
  border-radius: 50%;
  outline: none;
}

[slider] > input[type=range] {
  position: absolute;
  pointer-events: none;
  -webkit-appearance: none;
  z-index: 3;
  height: 14px;
  top: -2px;
  width: 100%;
  opacity: 0;
}

div[slider] > input[type=range]:focus::-webkit-slider-runnable-track {
  background: transparent;
  border: transparent;
}

div[slider] > input[type=range]:focus {
  outline: none;
}

div[slider] > input[type=range]::-webkit-slider-thumb {
  pointer-events: all;
  width: 28px;
  height: 28px;
  border-radius: 0px;
  border: 0 none;
  background: red;
  -webkit-appearance: none;
}

div[slider] > input[type=range]::-ms-fill-lower {
  background: transparent;
  border: 0 none;
}

div[slider] > input[type=range]::-ms-fill-upper {
  background: transparent;
  border: 0 none;
}

div[slider] > input[type=range]::-ms-tooltip {
  display: none;
}

[slider] > div > [sign] {
  opacity: 0;
  position: absolute;
  margin-left: -11px;
  top: -39px;
  z-index:3;
  background-color: #d02128;
  color: #fff;
  width: 28px;
  height: 28px;
  border-radius: 28px;
  -webkit-border-radius: 28px;
  align-items: center;
  -webkit-justify-content: center;
  justify-content: center;
  text-align: center;
}

[slider] > div > [sign]:after {
  position: absolute;
  content: '';
  left: 0;
  border-radius: 16px;
  top: 19px;
  border-left: 14px solid transparent;
  border-right: 14px solid transparent;
  border-top-width: 16px;
  border-top-style: solid;
  border-top-color: #d02128;
}

[slider] > div > [sign] > span {
  font-size: 12px;
  font-weight: 700;
  line-height: 28px;
}

[slider]:hover > div > [sign] {
  opacity: 1;
}
</style>
<div slider id="slider-distance">
  <div>
    <div inverse-left style="width:70%;"></div>
    <div inverse-right style="width:70%;"></div>
    <div range style="left:0%;right:0%;"></div>
    <span thumb style="left:0%;"></span>
    <span thumb style="left:100%;"></span>
    <div sign style="left:0%;">
      <span id="value">0</span>
    </div>
    <div sign style="left:100%;">
      <span id="value">100</span>
    </div>
  </div>
  <input type="range" value="0" max="100" min="0" step="1" oninput="
  this.value=Math.min(this.value,this.parentNode.childNodes[5].value-1);
  let value = (this.value/parseInt(this.max))*100
  var children = this.parentNode.childNodes[1].childNodes;
  children[1].style.width=value+'%';
  children[5].style.left=value+'%';
  children[7].style.left=value+'%';children[11].style.left=value+'%';
  children[11].childNodes[1].innerHTML=this.value;" />

  <input type="range" value="100" max="100" min="0" step="1" oninput="
  this.value=Math.max(this.value,this.parentNode.childNodes[3].value-(-1));
  let value = (this.value/parseInt(this.max))*100
  var children = this.parentNode.childNodes[1].childNodes;
  children[3].style.width=(100-value)+'%';
  children[5].style.right=(100-value)+'%';
  children[9].style.left=value+'%';children[13].style.left=value+'%';
  children[13].childNodes[1].innerHTML=this.value;" />
</div>

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
