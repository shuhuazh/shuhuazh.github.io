---
layout: page
permalink: /education-and-experience/
title: Education &amp; Experience
nav: true
nav_order: 1
---

<div class="edu-exp-page">
  {% for entry in site.data.edu-and-exp %}
    {% include cv/edu_exp_timeline.liquid %}
  {% endfor %}
</div>
