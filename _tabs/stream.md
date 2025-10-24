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

/* —— 基础按钮可读性提升 —— */
.feed-toggle,
.feed-collapse {
  display: inline-flex;
  align-items: center;
  gap: .35rem;
  margin-top: 8px;
  padding: 6px 12px;
  border-radius: 8px;
  font-size: .9rem;
  line-height: 1.6;
  cursor: pointer;
  user-select: none;
  border: 1px solid transparent;
  box-shadow: 0 1px 0 rgba(0,0,0,.04);
  transition: background .2s ease, border-color .2s ease, transform .1s ease, box-shadow .2s ease;
}
.feed-toggle:hover,
.feed-collapse:hover { transform: translateY(-1px); }

/* 键盘无障碍 */
.feed-toggle:focus-visible,
.feed-collapse:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 3px;
  border-radius: 10px;
}

/* 小箭头图标 */
.feed-toggle::after { content: "⌄"; font-size: .95em; }
.feed-collapse::after { content: "⌃"; font-size: .95em; }

/* —— 深色模式（沿用主题主色） —— */
@media (prefers-color-scheme: dark) {
  .feed-toggle   { background: var(--theme-color); color: #fff; border-color: rgba(255,255,255,.15); }
  .feed-toggle:hover { background: var(--btn-bg-hover); }
  .feed-collapse { background: var(--text-muted-color); color: #fff; border-color: rgba(255,255,255,.15); }
}

/* —— 浅色模式（显著提亮与描边） —— */
@media (prefers-color-scheme: light) {
  /* 展开：蓝色主按钮 */
  .feed-toggle {
    background: #2563eb;          /* 强对比纯色 */
    color: #fff;
    border-color: #1d4ed8;
    box-shadow: 0 2px 6px rgba(37,99,235,.18);
  }
  .feed-toggle:hover { background: #1d4ed8; border-color: #1e40af; }

  /* 收起：中性灰按钮 */
  .feed-collapse {
    background: #334155;
    color: #fff;
    border-color: #1f2937;
    box-shadow: 0 2px 6px rgba(51,65,85,.18);
  }
  .feed-collapse:hover { background: #1f2937; border-color: #111827; }
}

/* 若你的主题不跟随系统，而是用 data-mode 切换，可再加这两组选择器覆盖： */
html[data-mode="light"] .feed-toggle  { background:#2563eb; color:#fff; border-color:#1d4ed8; box-shadow:0 2px 6px rgba(37,99,235,.18); }
html[data-mode="light"] .feed-toggle:hover { background:#1d4ed8; border-color:#1e40af; }
html[data-mode="light"] .feed-collapse { background:#334155; color:#fff; border-color:#1f2937; box-shadow:0 2px 6px rgba(51,65,85,.18); }
html[data-mode="light"] .feed-collapse:hover { background:#1f2937; border-color:#111827; }
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
      <a href="{{ post.url }}" class="feed-short" style="text-decoration:none;color:inherit;">
        {{ short }}
      </a>

       <!-- 新增“阅读全文”跳转按钮 -->
      <a href="{{ post.url }}" class="feed-readmore" style="color: var(--theme-color); font-weight: 500; margin-left: 6px;">→ 阅读全文</a>

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
      {% assign cos_base = site.cos_img_base | default: "" %}
      
      <div class="feed-photos">
        {% for img in post.photos %}
          {% assign src = img.url | default: img.src | default: img | strip %}
          {% assign alt = img.alt | default: "photo" %}
          
          {% if src != "" %}
            {% comment %} 1) 先把相对/绝对路径拼成 full {% endcomment %}
            {% if src contains '://' %}
              {% assign full = src %}
            {% else %}
              {% assign first = src | slice: 0, 1 %}
              {% if first == '/' %}
                {% assign full = cos_base | append: src %}
              {% else %}
                {% assign full = cos_base | append: '/' | append: src %}
              {% endif %}
            {% endif %}
    
            {% comment %} 2) 列表页加缩略图参数（若原本无 ?） {% endcomment %}
            {% if full contains '?' %}
              {% assign final = full %}
            {% else %}
              {% assign final = full | append: '?imageMogr2/thumbnail/960x/format/webp/quality/85' %}
            {% endif %}

            <img src="{{ full }}" alt="{{ alt | escape }}" loading="lazy" decoding="async">
          {% endif %}
        {% endfor %}
      </div>
    {% endif %}
  </article>
{% endfor %}
</div>
