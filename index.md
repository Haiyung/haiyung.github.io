---
layout: default
title: 你好世界
---

<article>
<blockquote><p> 
Stay hungry. Stay foolish.
</p></blockquote>
</article>

<p style="margin-top:1.2em;margin-bottom:0;"><b>Blogs</b> | Browse by <a href="/tags">Tags</a></p>
<hr>
<table>
{% for post in site.categories.en %}
<tr id="blog-table">
<td>{{ post.date | date: "%Y-%m-%d" }}</td>
<td><a class="post-list-item" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></td>
</tr>
{% endfor %}
</table>
<hr>
<p>All posts <a href="/archive">archived</a></p>
