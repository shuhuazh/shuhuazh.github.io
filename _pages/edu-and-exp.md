---
layout: page
permalink: /education-and-experience/
title: Education &amp; Experience
nav: true
nav_order: 1
---

<div class="post">
    <article>
    <div class="cv">
        {% for entry in site.data.edu-and-exp %}
        <div class="card mt-3 p-3">
            <h3 class="card-title font-weight-medium">{{ entry.title }}</h3>
            <div>
                {% if entry.type == "list" %}
                    {% include cv/list.html %}
                {% elsif entry.type == "map" %}
                    {% include cv/map.html %}
                {% elsif entry.type == "nested_list" %}
                    {% include cv/nested_list.html %}
                {% elsif entry.type == "time_table" %}
                    {% include cv/time_table.html %}
                {% else %}
                    {{ entry.contents }}
                {% endif %}
            </div>
        </div>
        {% endfor %}
        </div>
    </article>
</div>