---
layout: archive
title: 分门别类
permalink: /archive
---

> 关于世界与市场，关于技术与力量。

作者：Haiyung

邮箱：huhaiyung@gmail.com

推特：huhaiyung

微信：huhaiyung

座右铭：
- 拥抱市场(stay hungry)，拥抱变化(stay foolish)。


{% for post in site.posts  %}{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% capture this_month %}{{ post.date | date: "%m" }}{% endcapture %}
{% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
{% capture next_month %}{{ post.previous.date | date: "%m" }}{% endcapture %}
{% if forloop.first %}<legend id="{{this_year}}">{{this_year}}</legend><ul>{% endif %}
<p><span>{{ post.date | date: "%Y-%m-%d" }}</span> <a class="pjaxlink" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></p>
{% if forloop.last %}</ul>{% else %}{% if this_year != next_year %}</ul><legend id="{{next_year}}">{{next_year}}</legend><ul>{% endif %}{% endif %}
{% endfor %} 