---
layout: page
permalink: /research/
title: Research
nav: true
nav_order: 2
---

{% assign research_interests = site.data.research | where: "title", "Research Interests" | first %}
{% assign funding_grants = site.data.research | where: "title", "Funding &amp; Grants" | first %}
{% assign honors_awards = site.data.research | where: "title", "Honors and Awards" | first %}

<div class="research-page">
  {% if research_interests %}
    <section class="research-section research-interests-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ research_interests.title }}</h2>
        <p class="research-section-note">Core themes, representative problems, and linked publications.</p>
      </div>

      <div class="research-interest-grid">
        {% for topic in research_interests.contents %}
          <article class="research-interest-item">
            <h3 class="research-interest-title">{{ topic.title }}</h3>
            {% if topic.items %}
              <ul class="research-interest-list">
                {% for item in topic.items %}
                  <li>{{ item }}</li>
                {% endfor %}
              </ul>
            {% endif %}
          </article>
        {% endfor %}
      </div>
    </section>
  {% endif %}

  {% if funding_grants %}
    <section class="research-section research-grants-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ funding_grants.title }}</h2>
        <p class="research-section-note">Selected grants, funding sources, and project roles.</p>
      </div>

      <div class="research-timeline">
        {% for grant in funding_grants.contents %}
          {% assign grant_year_parts = grant.year | split: ' - ' %}
          {% assign grant_year_from = grant_year_parts[0] | strip %}
          {% assign grant_year_to = grant_year_parts[1] | default: '' | strip %}

          <article class="research-timeline-item{% if forloop.first %} is-first{% endif %}{% if forloop.last %} is-last{% endif %}">
            <div class="research-timeline-time">
              {% if grant_year_to != '' %}
                <span class="research-timeline-start">{{ grant_year_from }}</span>
                <span class="research-timeline-divider">to</span>
                <span class="research-timeline-end">{{ grant_year_to }}</span>
              {% else %}
                <span class="research-timeline-single">{{ grant.year }}</span>
              {% endif %}
            </div>

            <div class="research-timeline-marker" aria-hidden="true">
              <span></span>
            </div>

            <div class="research-timeline-content">
              {% if grant.title %}
                <h3 class="research-timeline-title">{{ grant.title }}</h3>
              {% endif %}

              {% if grant.description %}
                <ul class="research-timeline-list">
                  {% for item in grant.description %}
                    <li>{{ item }}</li>
                  {% endfor %}
                </ul>
              {% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    </section>
  {% endif %}

  {% if honors_awards %}
    <section class="research-section research-awards-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ honors_awards.title }}</h2>
        <p class="research-section-note">Recognitions grouped by year.</p>
      </div>

      <div class="research-awards-list">
        {% for award_group in honors_awards.contents %}
          <article class="research-awards-item">
            <div class="research-awards-year">{{ award_group.year }}</div>
            <div class="research-awards-content">
              {% if award_group.title %}
                <h3 class="research-awards-title">{{ award_group.title }}</h3>
              {% endif %}

              {% if award_group.items %}
                <ul class="research-awards-points">
                  {% for item in award_group.items %}
                    <li>{{ item }}</li>
                  {% endfor %}
                </ul>
              {% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    </section>
  {% endif %}
</div>
