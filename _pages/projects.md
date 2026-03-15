---
layout: page
title: projects
permalink: /projects/
description: A curated showcase of my research and engineering projects in AI, Machine Learning, and Agentic Systems.
nav: true
nav_order: 1
display_categories: [work, fun]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
  {% assign sorted_projects = site.projects | sort: "importance" %}
  
  <ul class="post-list">
    {% for project in sorted_projects %}
      <li>
        <div class="row">
          <div class="col-sm-9">
            <h3>
              <a class="post-title" href="{{ project.url | relative_url }}">{{ project.title }}</a>
            </h3>
            <p>{{ project.description }}</p>
            <p class="post-meta">
              {% if project.date %}
                {{ project.date | date: '%B %d, %Y' }}
              {% endif %}
              {% if project.github %}
                &nbsp; &middot; &nbsp; 
                <a href="{{ project.github }}" target="_blank" class="text-muted">
                  <i class="fa-brands fa-github"></i> github
                </a>
              {% endif %}
            </p>
          </div>
          {% if project.img %}
            <div class="col-sm-3">
              <img class="card-img" src="{{ project.img | relative_url }}" style="object-fit: cover; height: 90%" alt="image">
            </div>
          {% endif %}
        </div>
      </li>
    {% endfor %}
  </ul>
</div>
