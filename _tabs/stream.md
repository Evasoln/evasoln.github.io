---
layout: page
title: 碎碎念
icon: "fa-brands fa-weibo"
order: 2
permalink: /stream/
render_with_liquid: true
---

{% raw %}
<style>
/* === 展开/收起按钮：明暗模式都清晰 === */
.feed-toggle,
.feed-collapse {
  display: inline-block;
  margin-top: 6px;
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 0.85rem;
  line-height: 1.6;
  cursor: pointer;
  user-select: none;
  transition: background .2s ease, color .2s ease, transform .1s ease, border-color .2s ease;

  /* 默认描边按钮 */
  background: transparent;
  color: var(--theme-color);
  border: 1px solid var(--theme-color);
}
.feed-toggle:hover,
.feed-toggle:focus {
  background: var(--theme-color);
  color: #fff;
  transform: translateY(-1px);
}
.feed-collapse {
  color: var(--text-muted-color);
  border-color: var(--text-muted-color);
}
.feed-collapse:hover,
.feed-collapse:focus {
  background: var(--text-muted-color);
  color: #fff;
  transform: translateY(-1px);
}
</style>
{% endraw %}

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
