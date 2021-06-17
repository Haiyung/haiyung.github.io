---
layout: books
title: Books - Haiyung's Personal Website
permalink: /books
---

# Index of /books

{% assign pdfs = site.static_files | where: "pdf", true %}

<table>
    <thead>
        <tr class="header" id="theader">
            <th id="nameColumnHeader" tabindex="0" role="button">Name</th>
            <th id="dateColumnHeader" tabindex="0" role="button">
                Date Modified
            </th>
        </tr>
    </thead>
    <tbody id="tbody">
        {% for pdf in pdfs %}
            <tr>
                <td>
                    <a class="icon file" draggable="true" href="{{ pdf.path }}" target="_blank">{{pdf.name}}</a>
                </td>
                <td class="detailsColumn">{{pdf.modified_time}}</td>
            </tr>
        {% endfor %}
    </tbody>
</table>

<hr>
<address>
    WEBrick/1.4.2 (Ruby/2.6/Ruby-2.6.3)<br>
    at haiyung.github.io
</address>