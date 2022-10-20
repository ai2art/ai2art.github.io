---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
list_title: 日志
list_title_1: 文章列表
list_title_2: 项目列表
---

<div class="home">
  {%- if site.posts.size > 0 -%}
    <h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>
    <ul class="post-list">
      {%- for post in site.posts -%}
      <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}
      </li>
      {%- endfor -%}
    </ul>
  {%- endif -%}

  {%- if site.pages.size > 0 -%}
    <h2 class="post-list-heading">{{ page.list_title_1 | default: "Posts" }}</h2>
    <ul class="post-list">
      {% for page in site.pages %}
      {% if page.article == true and page.draft == null %}
      <li>
        <h2>
          <a class="post-link" href="{{ page.url | relative_url }}">{{ page.title | escape }}</a>
        </h2>
      </li>
      {% endif %}
      {% endfor %}
    </ul>
  {%- endif -%}

  {%- if site.pages.size > 0 -%}
    <h2 class="post-list-heading">{{ page.list_title_2 | default: "Posts" }}</h2>
    <ul class="post-list">
      {% for page in site.pages %}
      {% if page.project == true and page.draft == null %}
      <li>
        <h2>
          <a class="post-link" href="{{ page.url | relative_url }}">{{ page.title | escape }}</a>
        </h2>
      </li>
      {% endif %}
      {% endfor %}
    </ul>
  {%- endif -%}
</div>