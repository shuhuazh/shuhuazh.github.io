---
layout: page
permalink: /research/
title: Research
nav: true
nav_order: 2
---

<div class="post">
    <article>
    <div class="cv">
        {% for entry in site.data.research %}
        <div class="card mt-3 p-3">
            <h3 class="card-title font-weight-medium">{{ entry.title }}</h3>
            <div>
                {% if entry.type == "list" %}
                    {% include cv/list.liquid %}
                {% elsif entry.type == "map" %}
                    {% include cv/map.liquid %}
                {% elsif entry.type == "nested_list" %}
                    {% include cv/nested_list.liquid %}
                {% elsif entry.type == "time_table" %}
                    {% include cv/time_table.liquid %}
                {% else %}
                    {{ entry.contents }}
                {% endif %}
            </div>
        </div>
        {% endfor %}
        </div>
    </article>
</div>