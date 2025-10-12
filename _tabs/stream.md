---
title: 随手记 
icon: fas fa-stream
order: 3
---

<style>
/* —— 信息流样式（仅作用于本页） —— */
.feed {max-width: 860px;}
.feed-card{
  border: 1px solid var(--blockquote-border-color);
  background: var(--card-bg);
  border-radius: 12px;
  padding: 14px 16px;
  margin: 14px 0;
  box-shadow: var(--card-shadow);
}
.feed-time{
  font-size: .85rem; color: var(--text-muted-color);
  display: inline-flex; align-items:center; gap:.35rem;
}
.feed-time:before{
  content: ""; display:inline-block; width:8px; height:8px; border-radius:50%;
  background: var(--theme-color); box-shadow: 0 0 0 2px var(--tag-shadow);
}
.feed-content{ margin-top: .35rem; line-height: 1.75; }
.feed-photos{ display:grid; grid-template-columns: repeat(3,1fr); gap:6px; margin-top:.5rem; }
.feed-photos img{ width:100%; height:100%; object-fit:cover; border-radius:8px; }
.feed-actions{ margin-top: .4rem; display:flex; gap:.8rem; font-size:.9rem; color:var(--text-muted-color);}
.feed-more{ display:none; }
.feed-card.expanded .feed-more{ display:inline; }
.feed-card.expanded .feed-toggle{ display:none; }
.feed-toggle{ cursor:pointer; color: var(--theme-color); }
</style>

<div class="feed">
{% assign items = site.statuses | default: site.posts | where_exp: "p", "p.categories contains '随手记' or p.collection == 'statuses'" | sort: "date" | reverse %}

{% for post in items limit: 60 %}
  <article class="feed-card h-entry" id="s-{{ post.id | slugify }}">
    <div class="feed-time">
      <i class="far fa-clock"></i>
      {{ post.date | date: "%Y-%m-%d %H:%M" }}
      {% if post.location %} · <i class="fas fa-location-dot"></i> {{ post.location }}{% endif %}
    </div>

    <div class="feed-content e-content">
      {%- assign plain = post.content | markdownify -%}
      {%- assign short = plain | strip_newlines | truncate: 160, "" -%}
      <span class="feed-short">{{ short }}</span>
      {% if plain.size > 160 %}
        <span class="feed-toggle" onclick="this.closest('.feed-card').classList.add('expanded')">展开</span>
        <span class="feed-more">{{ plain }}</span>
      {% endif %}
    </div>

    {% if post.photos %}
      <div class="feed-photos">
        {% for img in post.photos %}
          <a href="{{ img }}" target="_blank" rel="noopener">
            <img src="{{ img }}" loading="lazy" alt="photo">
          </a>
        {% endfor %}
      </div>
    {% endif %}

    <div class="feed-actions">
      <a href="{{ post.url | relative_url }}"><i class="far fa-link"></i> 永久链接</a>
      {% if post.comments != false and site.comments.provider %}<a href="{{ post.url | relative_url }}#post-comments"><i class="far fa-comment"></i> 评论</a>{% endif %}
    </div>
  </article>
{% endfor %}
</div>
