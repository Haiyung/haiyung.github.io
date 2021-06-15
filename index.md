---
layout: home
title: Haiyung's Personal Website
permalink: /
---

<div id="itemList">
    {% for post in site.posts %}
        <div class="topicItem">
            <div class="article-eyebrow">
                <time class="uni-timesince">
                    {{ post.date | date: "%Y年%m月%d日" }}
                </time>
                /
                {{ post.tags }}
            </div>
            <h2 class="article-title">
                <a href="{{ post.url }}">
                    {{ post.title }}
                </a>
            </h2>
        </div>
    {% endfor %}
</div>