---
layout: page
permalink: /research/
title: Research
nav: true
nav_order: 2
---

{% assign research_interests = site.data.research | where: "title", "Research Interests" | first %}
{% assign funding_grants = site.data.research | where: "title", "Funding &amp; Grants" | first %}
{% assign honors_awards = site.data.research | where: "title", "Honors &amp; Awards" | first %}

<div class="research-page">
  {% if research_interests %}
    <section class="research-section">
      <div class="research-section-rail">
        <h2 class="research-section-title">{{ research_interests.title }}</h2>
      </div>

      <div class="research-section-content">
        <div class="research-interest-list">
          {% for topic in research_interests.contents %}
            <article class="research-interest-item">
              <h3 class="research-interest-title">{{ topic.title }}</h3>
              <div class="research-interest-details">
                {% if topic.items %}
                  <ul class="research-interest-points">
                    {% for item in topic.items %}
                      <li>{{ item }}</li>
                    {% endfor %}
                  </ul>
                {% endif %}
              </div>
            </article>
          {% endfor %}
        </div>
      </div>
    </section>
  {% endif %}

  {% if funding_grants %}
    <section class="research-section">
      <div class="research-section-rail">
        <h2 class="research-section-title">{{ funding_grants.title }}</h2>
      </div>

      <div class="research-section-content">
        <div class="research-project-list">
          {% for grant in funding_grants.contents %}
            {% assign grant_year_parts = grant.year | split: ' - ' %}
            {% assign grant_year_from = grant_year_parts[0] | strip %}
            {% assign grant_year_to = grant_year_parts[1] | default: '' | strip %}

            <article class="research-project-item">
              <div class="research-project-meta">
                {% if grant_year_to != '' %}
                  <span class="research-project-start">{{ grant_year_from }}</span>
                  <span class="research-project-divider">to</span>
                  <span class="research-project-end">{{ grant_year_to }}</span>
                {% else %}
                  <span class="research-project-single">{{ grant.year }}</span>
                {% endif %}
              </div>

              <div class="research-project-body">
                {% if grant.title %}
                  <h3 class="research-project-title">{{ grant.title }}</h3>
                {% endif %}

                {% if grant.description %}
                  {% if grant.description.first %}
                    <p class="research-project-source">{{ grant.description.first }}</p>
                  {% endif %}

                  {% if grant.description.size > 1 %}
                    <p class="research-project-role">{{ grant.description[1] }}</p>
                  {% endif %}

                  {% if grant.description.size > 2 %}
                    <ul class="research-project-notes">
                      {% for item in grant.description offset:2 %}
                        <li>{{ item }}</li>
                      {% endfor %}
                    </ul>
                  {% endif %}
                {% endif %}
              </div>
            </article>
          {% endfor %}
        </div>
      </div>
    </section>
  {% endif %}

  {% if honors_awards %}
    <section class="research-section">
      <div class="research-section-rail">
        <h2 class="research-section-title">{{ honors_awards.title }}</h2>
      </div>

      <div class="research-section-content">
        <div class="research-award-list">
          {% for award_group in honors_awards.contents %}
            <article class="research-award-item">
              <div class="research-award-meta">
                <span class="research-award-year">{{ award_group.year }}</span>
              </div>

              <div class="research-award-body">
                {% if award_group.items %}
                  <ul class="research-award-points">
                    {% for item in award_group.items %}
                      <li>{{ item }}</li>
                    {% endfor %}
                  </ul>
                {% endif %}
              </div>
            </article>
          {% endfor %}
        </div>
      </div>
    </section>
  {% endif %}
</div>
