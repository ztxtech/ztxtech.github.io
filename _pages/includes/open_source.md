# Open Sources Project

A mix of my projects and external references, ranked by GitHub stars. Dates are kept as context.

<ol class="opensource-timeline">
{% assign projects = site.data.open_source_projects | sort: "star_sort" | reverse %}
{% for project in projects %}
  {% assign star_badge = "https://img.shields.io/github/stars/" | append: project.repository | append: "?style=flat-square&amp;logo=github&amp;logoColor=white&amp;label=stars&amp;labelColor=4b5563&amp;color=2f855a" %}
  <li class="opensource-project">
    <time class="opensource-project__period" datetime="{{ project.date_iso }}">{{ project.date }}</time>
    <article class="opensource-project__content">
      <header class="opensource-project__header">
        <div class="opensource-project__identity">
          <h3><a href="{{ project.url }}">{{ project.name }}</a></h3>
          <div class="opensource-project__meta">
            <span class="opensource-project__relationship opensource-project__relationship--{{ project.relationship_tone }}">{{ project.relationship }}</span>
            <span class="opensource-project__kind">{{ project.kind }}</span>
          </div>
          <code>{{ project.repository }}</code>
          <ul class="opensource-project__labels" aria-label="Application labels">
            {% for label in project.labels %}
            <li>{{ label }}</li>
            {% endfor %}
          </ul>
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
      <p class="opensource-project__data">
        <span>Data</span>
        {{ project.dataset_scope }}
      </p>
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
