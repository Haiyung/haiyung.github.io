---
layout: archive
title: 分门别类
permalink: /archive
---

> 关于世界与市场，关于技术与力量。

作者：Haiyung

推特：huhaiyung

邮箱：huhaiyung@gmail.com


{% for tag in site.tags %}
  <div>
	<legend id="{{ tag | first }}">{{ tag | first }}</legend>
	<ul>
	    {% for posts in tag %}
	        {% for post in posts %}
	            {% if post.url %}
                    <p>
                        <a class="pjaxlink" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
                        <span>{{ post.date | date: "%Y-%m-%d" }}</span>
                    </p>
                {% endif %}
            {% endfor %}
        {% endfor %}
    </ul>
  </div>
{% endfor %}

> 拥抱市场，拥抱变化。stay hungry,stay foolish.