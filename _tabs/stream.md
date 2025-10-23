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
