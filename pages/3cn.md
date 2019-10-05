---
layout: cndefault
permalink: /cn/
title: 你好世界
---

<article>
    <blockquote>
        <p>拥抱市场，拥抱变化。</p>
    </blockquote>
</article>

<p style="text-align:left;margin-top:1.2em;margin-bottom:0;">
    <b>文章 </b>| 按<a href="/cntags">文章分类</a>浏览 
</p>
---

<table>
    {% for post in site.categories.cn %}
    <tr id="blog-table">
        <td>{{ post.date | date: "%Y-%m-%d" }}</td>
        <td><a class="post-list-item" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></td>
    </tr>
    {% endfor %}
</table>
<hr>
<p>博文<a href="/cnarchive">归档</a></p>
