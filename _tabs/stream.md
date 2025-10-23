---
layout: page
title: 碎碎念
icon: "fa-brands fa-weibo"
order: 2
permalink: /stream/
render_with_liquid: true
---

<style>
.feed {
  max-width: 860px;
  margin: 0 auto;
}
.feed-card {
  border: 1px solid var(--blockquote-border-color);
  background: var(--card-bg);
  border-radius: 12px;
  padding: 14px 16px;
  margin: 14px 0;
  box-shadow: var(--card-shadow);
  transition: background 0.2s ease;
}
.feed-card:hover { background: var(--btn-bg-hover); }
.feed-time {
  font-size: .85rem;
  color: var(--text-muted-color);
  display: inline-flex;
  align-items: center;
  gap: .35rem;
}
.feed-content { margin-top: .35rem; line-height: 1.75; }

.feed-photos {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 6px;
  margin-top: .5rem;
}
.feed-photos img {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 8px;
}

.feed-more { display: none; }
.feed-card.expanded .feed-more {
  display: block;
  max-height: 600px;
  overflow-y: auto;
}
.feed-card.expanded .feed-short { display: none; }
.feed-card.expanded .feed-toggle { display: none; }
.feed-card:not(.expanded) .feed-collapse { display: none; }

/* === 新增更明显的按钮样式 === */
.feed-toggle,
.feed-collapse {
  display: inline-block;
  margin-top: 6px;
  padding: 4px 10px;
  border-radius: 6px;
  background: var(--theme-color);
  color: #fff;
  font-size: 0.85rem;
  line-height: 1.6;
  cursor: pointer;
  transition: background 0.2s ease, transform 0.1s ease;
  user-select: none;
}
.feed-toggle:hover,
.feed-collapse:hover {
  background: var(--btn-bg-hover);
  transform: translateY(-1px);
}
.feed-collapse {
  margin-top: 10px;
  background: var(--text-muted-color);
}
</style>

<div class="feed">
{% assign items = site.statuses | default: site.posts %}
{% assign items = items | where_exp: "p", "p.categories contains '碎碎念' or p.collection == 'statuses'" | sort: 'date' | reverse %}
{% for post in items limit: 60 %}
  <article class="feed-card h-entry">
    <div class="feed-time">
      {{ post.date | date: "%Y-%m-%d %H:%M" }}{% if post.location %} · {{ post.location }}{% endif %}
    </div>

    <div class="feed-content e-content">
      {% assign html  = post.content | markdownify %}
      {% assign short = html | strip_html | strip_newlines | truncate: 160, "" %}
      <span class="feed-short">{{ short }}</span>

      {% if html.size > 160 %}
        <span class="feed-toggle" role="button" tabindex="0"
          onclick="this.closest('.feed-card').classList.add('expanded')">展开全文</span>

        <div class="feed-more">
          {{ html }}
          <div style="margin-top:.5rem;">
            <span class="feed-collapse" role="button" tabindex="0"
              onclick="const c=this.closest('.feed-card'); c.classList.remove('expanded'); c.scrollIntoView({behavior:'smooth', block:'start'});">收起</span>
          </div>
        </div>
      {% endif %}
    </div>

    {% if post.photos %}
      <div class="feed-photos">
        {% for img in post.photos %}
          <img src="{{ img | strip }}" loading="lazy" alt="photo">
        {% endfor %}
      </div>
    {% endif %}
  </article>
{% endfor %}
</div>
