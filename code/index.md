---
title: Code
layout: academic
author_profile: true
---

<!-- https://vuejsexamples.com/vue-3-slider-component-with-multihandles-and-formatting/ -->
<script src="https://unpkg.com/vue@3.0.4/dist/vue.global.prod.js"></script>
<script src="https://unpkg.com/@vueform/slider"></script>

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
    
      <div class="output">Year range: {{ yearslider.value }}</div>
      <div>All years: {{ allyears }}</div>
      <div>Show: {{ show }}</div>
      
      

      <div v-for="yr in [...new Set(publ.map(a => a.year))].sort().reverse()">
        <h2>{{ yr }}</h2>
        <ul class="publist">
            <div v-for="pub in publ.filter(a => (a.year === yr))">
            <li class="publist">{{ pub.text }} &ndash; links and stuff comes here ...</li>
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

<style>
li.checkboxlist{
    list-style: none; 
    display:inline-block;
    padding-left: 15px;
    padding-right: 15px;
}
ul.publist{
    list-style: none; 
    padding-left: 0;
}
li.publist{
    margin-bottom: 1.5em;
}

 /* Customize the label (the container) */
 .container {
  display: block;
  position: relative;
  padding-left: 25px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 14px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 18px;
  width: 18px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #52adc8;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 8px;
  top: 4px;
  width: 4px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

/* Customized css from here https://unpkg.com/@vueform/slider@1.0.5/themes/default.css */
.slider-target,.slider-target *{-webkit-touch-callout:none;-webkit-tap-highlight-color:rgba(0,0,0,0);-webkit-user-select:none;touch-action:none;-ms-user-select:none;-moz-user-select:none;user-select:none;box-sizing:border-box}
.slider-target{position:relative}
.slider-base,.slider-connects{width:100%;height:100%;position:relative;z-index:1}
.slider-connects{overflow:hidden;z-index:0}
.slider-connect,.slider-origin{will-change:transform;position:absolute;z-index:1;top:0;right:0;-ms-transform-origin:0 0;-webkit-transform-origin:0 0;-webkit-transform-style:preserve-3d;transform-origin:0 0;transform-style:flat}
.slider-connect{height:100%;width:100%}
.slider-origin{height:10%;width:10%}
.slider-txt-dir-rtl.slider-horizontal .slider-origin{left:0;right:auto}
.slider-vertical .slider-origin{width:0}
.slider-horizontal .slider-origin{height:0}
.slider-handle{-webkit-backface-visibility:hidden;backface-visibility:hidden;position:absolute}.slider-touch-area{height:100%;width:100%}
.slider-state-tap .slider-connect,.slider-state-tap .slider-origin{transition:transform .3s}
.slider-state-drag *{cursor:inherit!important}
.slider-horizontal{height:6px}
.slider-horizontal .slider-handle{width:16px;height:16px;top:-6px;right:-8px}
.slider-vertical{width:6px;height:300px}
.slider-vertical .slider-handle{width:16px;height:16px;top:-8px;right:-6px}
.slider-txt-dir-rtl.slider-horizontal .slider-handle{left:-8px;right:auto}
.slider-base{background-color:#d4e0e7}
.slider-base,.slider-connects{border-radius:3px}
.slider-connect{background:#52adc8;cursor:pointer}
.slider-draggable{cursor:ew-resize}
.slider-vertical .slider-draggable{cursor:ns-resize}
.slider-handle{width:16px;height:16px;border-radius:50%;background:#fff;border:0;right:-8px;box-shadow:.5px .5px 2px 1px rgba(0,0,0,.32);cursor:-webkit-grab;cursor:grab}.slider-handle:focus{outline:none}.slider-active{box-shadow:.5px .5px 2px 1px rgba(0,0,0,.42);cursor:-webkit-grabbing;cursor:grabbing}[disabled] .slider-connect{background:#b8b8b8}[disabled].slider-handle,[disabled] .slider-handle,[disabled].slider-target{cursor:not-allowed}[disabled] .slider-tooltip{background:#b8b8b8;border-color:#b8b8b8}.slider-tooltip{position:absolute;display:block;font-size:14px;font-weight:500;white-space:nowrap;padding:2px 5px;min-width:20px;text-align:center;color:#fff;border-radius:5px;border:1px solid #52adc8;background:#52adc8}.slider-horizontal .slider-tooltip{transform:translate(-50%);left:50%;bottom:24px}.slider-horizontal .slider-tooltip:before{content:"";position:absolute;bottom:-10px;left:50%;width:0;height:0;border:5px solid transparent;border-top-color:inherit;transform:translate(-50%)}.slider-vertical .slider-tooltip{transform:translateY(-50%);top:50%;right:24px}.slider-vertical .slider-tooltip:before{content:"";position:absolute;right:-10px;top:50%;width:0;height:0;border:5px solid transparent;border-left-color:inherit;transform:translateY(-50%)}.slider-horizontal .slider-origin>.slider-tooltip{transform:translate(50%);left:auto;bottom:14px}.slider-vertical .slider-origin>.slider-tooltip{transform:translateY(-18px);top:auto;right:18px}.slider-pips,.slider-pips *{box-sizing:border-box}.slider-pips{position:absolute;color:#999}.slider-value{position:absolute;white-space:nowrap;text-align:center}.slider-value-sub{color:#ccc;font-size:10px}.slider-marker{position:absolute;background:#ccc}.slider-marker-large,.slider-marker-sub{background:#aaa}.slider-pips-horizontal{padding:10px 0;height:80px;top:100%;left:0;width:100%}.slider-value-horizontal{transform:translate(-50%,50%)}.slider-rtl .slider-value-horizontal{transform:translate(50%,50%)}.slider-marker-horizontal.slider-marker{margin-left:-1px;width:2px;height:5px}.slider-marker-horizontal.slider-marker-sub{height:10px}.slider-marker-horizontal.slider-marker-large{height:15px}.slider-pips-vertical{padding:0 10px;height:100%;top:0;left:100%}.slider-value-vertical{transform:translateY(-50%);padding-left:25px}.slider-rtl .slider-value-vertical{transform:translateY(50%)}.slider-marker-vertical.slider-marker{width:5px;height:2px;margin-top:-1px}.slider-marker-vertical.slider-marker-sub{width:10px}.slider-marker-vertical.slider-marker-large{width:15px}
</style>
