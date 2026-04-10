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
  <section class="research-intro">
    <div class="research-intro-copy">
      <p class="research-kicker">Research Program</p>
      <h2 class="research-intro-title">Data-driven control for nonlinear, networked, and autonomous systems.</h2>
      <p class="research-intro-lead">
        Current work centers on model-free and iterative learning methods, distributed coordination and estimation,
        resilient control under communication constraints and attacks, and control-oriented autonomy for vehicles and marine systems.
      </p>
    </div>

    {% if research_interests %}
      <div class="research-intro-focus">
        <div class="research-intro-focus-label">Focus Areas</div>
        <ul class="research-intro-focus-list">
          {% for topic in research_interests.contents %}
            <li>{{ topic.title }}</li>
          {% endfor %}
        </ul>
      </div>
    {% endif %}
  </section>

  {% if research_interests %}
    <section class="research-section research-interests-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ research_interests.title }}</h2>
        <p class="research-section-note">Themes are organized by method, system setting, and application domain.</p>
      </div>

      <div class="research-theme-list">
        {% for topic in research_interests.contents %}
          <article class="research-theme-item">
            <div class="research-theme-index">
              {% if forloop.index < 10 %}0{% endif %}{{ forloop.index }}
            </div>
            <div class="research-theme-content">
              <h3 class="research-theme-title">{{ topic.title }}</h3>
              {% if topic.items %}
                <ul class="research-theme-points">
                  {% for item in topic.items %}
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

  {% if funding_grants %}
    <section class="research-section research-grants-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ funding_grants.title }}</h2>
        <p class="research-section-note">Project title, funding source, and research role.</p>
      </div>

      <div class="research-project-list">
        {% for grant in funding_grants.contents %}
          {% assign grant_year_parts = grant.year | split: ' - ' %}
          {% assign grant_year_from = grant_year_parts[0] | strip %}
          {% assign grant_year_to = grant_year_parts[1] | default: '' | strip %}
          {% assign grant_display_title = grant.title | strip %}
          {% assign hide_grant_title = false %}
          {% if grant_display_title == '' or grant_display_title == 'xxxxxx' %}
            {% assign hide_grant_title = true %}
          {% endif %}

          <article class="research-project-item">
            <div class="research-project-time">
              {% if grant_year_to != '' %}
                <span class="research-project-start">{{ grant_year_from }}</span>
                <span class="research-project-divider">to</span>
                <span class="research-project-end">{{ grant_year_to }}</span>
              {% else %}
                <span class="research-project-single">{{ grant.year }}</span>
              {% endif %}
            </div>

            <div class="research-project-body">
              {% unless hide_grant_title %}
                <h3 class="research-project-title">{{ grant.title }}</h3>
              {% endunless %}

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
    </section>
  {% endif %}

  {% if honors_awards %}
    <section class="research-section research-awards-section">
      <div class="research-section-heading">
        <h2 class="research-section-title">{{ honors_awards.title }}</h2>
        <p class="research-section-note">A compact record of major recognitions and academic distinctions.</p>
      </div>

      <div class="research-awards-rail">
        {% for award_group in honors_awards.contents %}
          <article class="research-award-item">
            <div class="research-award-year">{{ award_group.year }}</div>
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
    </section>
  {% endif %}
</div>
