---
layout: page
permalink: /repositories/
title: repositories
description: 
nav: true
nav_order: 4
---

## GitHub users

{% if site.data.repositories.github_users %}

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    <p><a href="https://github.com/{{ user }}" target="_blank" rel="noopener">{{ user }}</a></p>
  {% endfor %}
</div>

{% endif %}

---

## GitHub Repositories

{% if site.data.repositories.github_repos %}
  <div class="repositories">
    {% for repo in site.data.repositories.github_repos %}
      <p><a href="{{ repo.url }}" target="_blank" rel="noopener">{{ repo.name }}</a></p>
    {% endfor %}
  </div>
{% endif %}

---

## GitLab Users

{% if site.data.repositories.gitlab_users %}
  <div class="repositories">
    {% for user in site.data.repositories.gitlab_users %}
      <p><a href="{{ user }}" target="_blank" rel="noopener">{{ user }}</a></p>
    {% endfor %}
  </div>
{% endif %}

---
## GitLab Repositories

{% if site.data.repositories.gitlab_repos %}
  <div class="repositories">
    {% for repo in site.data.repositories.gitlab_repos %}
      <p><a href="{{ repo.url }}" target="_blank" rel="noopener">{{ repo.name }}</a></p>
    {% endfor %}
  </div>
{% endif %}



