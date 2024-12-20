---
layout: archive
title: Archive - Haiyung's Personal Website
permalink: /archive
---

> 关于世界与市场，关于技术与力量。

<div class="archive-author">
<p>作者：Haiyung</p>

<p>推特：hhyplus</p>

<p>邮箱：hhyplus@163.com</p>
</div>

<div class="archive-buttons">
  {% capture tags %}
    {% for tag in site.tags %}
      {{ tag[1].size | plus: 1000 }}#{{ tag[0] }}#{{ tag[1].size }}
    {% endfor %}
  {% endcapture %}

  {% assign sortedtags = tags | split:' ' | sort %}

  {% for tag in sortedtags reversed %}
    {% assign tagitems = tag | split: '#' %}
      <div class="archive-sub-button">
        <a href="#{{ tagitems[1] }}" class="archive-sub-button-text">{{ tagitems[1] }}</a>
        <span class="archive-sub-button-content">({{ tagitems[2] }})</span>
      </div>
 
  {% endfor %}
</div>

{% for tag in site.tags %}
  <div class="archive-main">
    <div class="archive-tag-head">
        <svg class="bi bi-layout-text-sidebar-reverse" width="1.2em" height="1.2em" viewBox="0 0 16 16" fill="#A6A6A6" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" d="M2 1h12a1 1 0 011 1v12a1 1 0 01-1 1H2a1 1 0 01-1-1V2a1 1 0 011-1zm12-1a2 2 0 012 2v12a2 2 0 01-2 2H2a2 2 0 01-2-2V2a2 2 0 012-2h12z" clip-rule="evenodd"/>
          <path fill-rule="evenodd" d="M5 15V1H4v14h1zm8-11.5a.5.5 0 00-.5-.5h-5a.5.5 0 000 1h5a.5.5 0 00.5-.5zm0 3a.5.5 0 00-.5-.5h-5a.5.5 0 000 1h5a.5.5 0 00.5-.5zm0 3a.5.5 0 00-.5-.5h-5a.5.5 0 000 1h5a.5.5 0 00.5-.5zm0 3a.5.5 0 00-.5-.5h-5a.5.5 0 000 1h5a.5.5 0 00.5-.5z" clip-rule="evenodd"/>
        </svg>
        <span id="{{ tag | first }}">{{ tag | first }}</span>
    </div>
    <div class="archive-article-item">
        {% for posts in tag %}
            {% for post in posts %}
                {% if post.url %}
                    <div class="item-row">
                        <svg class="bi bi-circle" width="0.4em" height="0.8em" viewBox="0 0 16 16" fill="#A6A6A6" xmlns="http://www.w3.org/2000/svg">
                          <path fill-rule="evenodd" d="M8 15A7 7 0 108 1a7 7 0 000 14zm0 1A8 8 0 108 0a8 8 0 000 16z" clip-rule="evenodd"/>
                        </svg>
                        <a class="item-url" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
                        <div class="date">
                            <span>
                                {{ post.date | date: "%Y-%m-%d" }}
                            </span>
                        </div>
                    </div>
                {% endif %}
            {% endfor %}
        {% endfor %}
    </div>
  </div>
{% endfor %}

<blockquote class="archive-bq">
  <p>Stay hungry. Stay foolish.</p>
  <p>拥抱市场，拥抱变化。面朝大海，心向未来。</p>
</blockquote>