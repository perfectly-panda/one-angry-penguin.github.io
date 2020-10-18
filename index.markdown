---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
<ul>
    {% for post in site.posts %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <ul><li>{{ post.date | date: '%B %d, %Y' }}</li></ul>
        
    </li>
    {% endfor %}
</ul>