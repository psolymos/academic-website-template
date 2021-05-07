---
title: Code
layout: academic
author_profile: true
---

<!-- {% raw %} -->
<div id="app">
    <div>
      <ul>
        <li class="checkboxlist">
        <label class="container">R package
            <input type="checkbox" v-model="show.rpkg">
            <span class="checkmark"></span>
        </label>
        </li>
        <li class="checkboxlist">
        <label class="container">Stata module
            <input type="checkbox" v-model="show.stata">
            <span class="checkmark"></span>
        </label>
        </li>
        <li class="checkboxlist">
            <label class="container">GUI
                <input type="checkbox" v-model="show.gui">
                <span class="checkmark"></span>
            </label>
        </li>
        <li class="checkboxlist">
            <label class="container">Statistics
                <input type="checkbox" v-model="show.statistics">
                <span class="checkmark"></span>
            </label>
        </li>
        <li class="checkboxlist">
            <label class="container">Psychology
                <input type="checkbox" v-model="show.psychology">
                <span class="checkmark"></span>
            </label>
        </li>
      </ul>
    </div>
    <p>{{ show }}</p>
    <p>{{ softw }}</p>
    <div v-for="s in softw">
        <h3>{{ s.name }}</h3>
        <p>{{ s.description }}</p>
        <p><a v-bind:href="s.link">{{ s.type }}</a> / {{ s.domain }}</p>
    </div>
</div>
<!-- {% endraw %} -->

<script>
// software list
var sw = [
        {% for s in site.data.software %}{
          "name": "{{ s.name }}",
          "description": "{{ s.description }}",
          "link": "{{ s.link }}",
          "type": "{{ s.type }}",
          "domain": "{{ s.domain }}"
        }{% unless forloop.last %},{% endunless %}
      {% endfor %}];
//vue app
const app = Vue.createApp({
  data: () => ({
    s: sw,
    show: {
        rpkg: false,
        stata: false,
        gui: false,
        statistics: false,
        psychology: false,
    },
  }),
  computed: {
    softw: function () {
        var x = [];
        for (i = 0; i < this.s.length; i++) {
            let add = false;
            // none is checked: show all
            if (!this.show.rpkg && !this.show.stata && !this.show.gui &&!this.show.statistics && !this.show.psychology) {
              add = true;
            } else {
              // type
              if (this.show.rpkg && this.s[i].type == "R package")
                  add = true;
              if (this.show.stata && this.s[i].type == "Stats module")
                  add = true;
              if (this.show.gui && this.s[i].type == "GUI")
                  add = true;
              // domain
              if (this.show.statistics && this.s[i].domain == "Statistics")
                  add = true;
              if (this.show.psychology && this.s[i].domain == "Psychology")
                  add = true;
            }
            if (add)
                x[i] = this.s[i];
        }
        return x
    }
  }
})
app.mount('#app')
</script>
