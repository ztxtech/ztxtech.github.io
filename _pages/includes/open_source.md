# Open Sources Project

Projects that have shaped how I think about evidence, time-series modeling, recursive self-improvement, and reproducible experimentation, listed from newest to oldest.

<ol class="opensource-timeline">
{% for project in site.data.open_source_projects %}
  {% assign star_badge = "https://img.shields.io/github/stars/" | append: project.repository | append: "?style=flat-square&amp;logo=github&amp;logoColor=white&amp;label=stars&amp;labelColor=4b5563&amp;color=2f855a" %}
  <li class="opensource-project">
    <time class="opensource-project__period" datetime="{{ project.date_iso }}">{{ project.date }}</time>
    <article class="opensource-project__content">
      <header class="opensource-project__header">
        <div class="opensource-project__identity">
          <h3><a href="{{ project.url }}">{{ project.name }}</a></h3>
          <span class="opensource-project__relationship">{{ project.kind }}</span>
          <code>{{ project.repository }}</code>
        </div>
        <a
          class="opensource-project__stars"
          href="https://github.com/{{ project.repository }}/stargazers"
          aria-label="{{ project.name }} stars on GitHub"
        >
          <img src="{{ star_badge }}" alt="{{ project.name }} stars on GitHub" width="88" height="20" loading="lazy">
        </a>
      </header>
      <p class="opensource-project__summary">{{ project.summary }}</p>
      <ul class="opensource-project__highlights">
        {% for feature in project.features %}
        <li>{{ feature }}</li>
        {% endfor %}
      </ul>
      <footer class="opensource-project__links">
        <a href="{{ project.url }}">
          <i class="fab fa-github" aria-hidden="true"></i>
          Source
        </a>
        {% if project.website_url %}
        <a href="{{ project.website_url }}">
          <i class="fas fa-external-link-alt" aria-hidden="true"></i>
          {{ project.website_label }}
        </a>
        {% endif %}
      </footer>
    </article>
  </li>
{% endfor %}
</ol>
