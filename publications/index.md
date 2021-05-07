---
title: Publications
layout: academic
author_profile: true
---


<!-- 
  {% for yr in site.data.categories.publications.years %}
  <h2 id="year-{{ yr }}">{{ yr }}</h2>
  <ul>{% for ms in site.data.publications %}{% if ms.year == yr %}
    <li id="publ-id-{{ ms.id }}" class="publ publ-type-{{ ms.type }} publ-auth-{{ ms.authorship }} publ-status-{{ ms.status }}">
      {{ ms.text }}{% if ms.preprint %}&mdash; <a href="{{ ms.preprint }}">Preprint</a>{% endif %}{% if ms.datarepo %}&mdash; <a href="{{ ms.datarepo }}">Data repository</a>{% endif %}{% if ms.rpackagename %}&mdash; <a href="{{ ms.rpackagelink }}">{{ ms.rpackagename }}</a>{% endif %}{% if ms.webappname %}&mdash; <a href="{{ ms.webapplink }}">{{ ms.webappname }}</a>{% endif %}{% if ms.doi %} <div data-badge-popover="bottom" style="display: inline-block;" data-badge-type="4" data-doi="{{ ms.doi }}" data-hide-no-mentions="true" class="altmetric-embed"></div>{% endif %}
      </li>{% endif %}{% endfor %}
  </ul>
  {% endfor %}
-->


<!-- {% raw %} -->
<div id="app">

    <p><br></p>
    <p style="width:60%;">
        <Slider
          v-model="yearslider.value"
          v-bind="yearslider"
        ></Slider>
    </p>

    <ul>
        <li class="checkboxlist">
        Type
        <label class="container">Empirical
            <input type="checkbox" v-model="show.empirical">
            <span class="checkmark"></span>
        </label>
        <label class="container">Methods
            <input type="checkbox" v-model="show.methods">
            <span class="checkmark"></span>
        </label>
        </li>
        <li class="checkboxlist">
            Authorship
            <label class="container">Fist
                <input type="checkbox" v-model="show.first">
                <span class="checkmark"></span>
            </label>
            <label class="container">Senior
                <input type="checkbox" v-model="show.last">
                <span class="checkmark"></span>
            </label>
        </li>
        <li class="checkboxlist">
            Status
            <label class="container">Published
                <input type="checkbox" v-model="show.published">
                <span class="checkmark"></span>
            </label>
            <label class="container">In preparation
                <input type="checkbox" v-model="show.inprep">
                <span class="checkmark"></span>
            </label>
        </li>
    </ul>
    
      <!-- <div class="output">Year range: {{ yearslider.value }}</div>
      <div>All years: {{ allyears }}</div>
      <div>Show: {{ show }}</div> -->
      
      

      <div v-for="yr in [...new Set(publ.map(a => a.year))].sort().reverse()">
        <h2>{{ yr }}</h2>
        <ul class="publist">
            <div v-for="pub in publ.filter(a => (a.year === yr))">
            <li class="publist">{{ pub.text }}
            <div v-if="pub.preprint">&mdash; <a href="{{ pub.preprint }}">Preprint</a></div>
            <div v-if="pub.datarepo">&mdash; <a href="{{ pub.datarepo }}"></a></div>
            <div v-if="pub.rpackagename">&mdash; <a href="{{ pub.rpackagelink }}">{{ pub.rpackagename }}</a></div>
            <div v-if="pub.webappname">&mdash; <a href="{{ pub.webapplink }}">{{ pub.webappname }}</a></div>
            <div v-if="pub.doi"><div data-badge-popover="bottom" style="display: inline-block;" data-badge-type="4" data-doi="{{ pub.doi }}" data-hide-no-mentions="true" class="altmetric-embed"></div></div>
            </li>
            </div>
        </ul>
      </div>
  
</div>
<!-- {% endraw %} -->

<script>
// publication list
var p = [
        {% for ms in site.data.publications %}{
          "id": "{{ ms.id }}",
          "text": "{{ ms.text }}",
          "year": {{ ms.year }},
          "type": "{{ ms.type }}",
          "authorship": "{{ ms.authorship }}",
          "status": "{{ ms.status }}",
          "preprint": "{{ ms.preprint }}",
          "datarepo": "{{ ms.datarepo }}",
          "rpackagename": "{{ ms.rpackagename }}",
          "rpackagelink": "{{ ms.rpackagelink }}",
          "webappname": "{{ ms.webappname }}",
          "webapplink": "{{ ms.webapplink }}",
          "doi": "{{ ms.doi }}"
        }{% unless forloop.last %},{% endunless %}
      {% endfor %}];
// unique years
var yrs = [...new Set(p.map(a => a.year))].sort().reverse();
//vue app
const app = Vue.createApp({
  data: () => ({
    yearslider: {
        value: [Math.min(...yrs), Math.max(...yrs)],
        min: Math.min(...yrs),
        max: Math.max(...yrs),
    },
    pubs: p,
    allyears: yrs,
    show: {
        empirical: false,
        methods: false,
        first: false,
        last: false,
        published: false,
        inprep: false,
    },
  }),
  computed: {
    publ: function () {
        var x = [];
        for (i = 0; i < this.pubs.length; i++) {
            let add = false;
            // none is checked: show all
            if (!this.show.empirical && !this.show.methods && !this.show.first &&!this.show.last && !this.show.published && !this.show.inprep) {
              add = true;
            } else {
              // type
              if (this.show.empirical && this.pubs[i].type == "empirical")
                  add = true;
              if (this.show.methods && this.pubs[i].type == "methods")
                  add = true;
              // authorship
              if (this.show.first && this.pubs[i].authorship == "first")
                  add = true;
              if (this.show.last && this.pubs[i].authorship == "last")
                  add = true;
              // status
              if (this.show.published && this.pubs[i].status == "published")
                  add = true;
              if (this.show.inprep && this.pubs[i].status != "published")
                  add = true;
            }
            if (add) {
                if (this.pubs[i].year < this.yearslider.value[0]) {
                    add = false;
                }
                if (this.pubs[i].year > this.yearslider.value[1]) {
                    add = false;
                }
            }
            if (add)
                x[i] = this.pubs[i];
        }
        return x
    }
  }
})
// slider component
app.component('Slider', VueformSlider)
app.mount('#app')
</script>
