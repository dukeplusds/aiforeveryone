---
title: Class Projects
category: Previous Class Papers and Projects
order: 2
---
<ul>
    {% assign grouped = site.projects | group_by: 'category' %}
    {% for group in grouped %}
        <li class="nav-item top-level {% if group.name == page.category %}current{% endif %}">
            {% assign items = group.items | sort: 'order' %}
            <a href="{{ site.baseurl }}{{ items.first.url }}"><h3>{{ group.name }}</h3></a>
            <ul>
                {% for item in items %}
                    <li class="nav-item {% if item.url == page.url %}current{% endif %}"><a href="{{ site.baseurl }}{{ item.url }}"><h5>{{ item.title }}</h5></a></li>
                    <li class="nav-item {% if item.url == page.url %}current{% endif %}"><a href="{{ site.baseurl }}{{ item.url }}"><i>{{ item.authors }}</i></a></li>
                {% endfor %}
            </ul>
        </li>
    {% endfor %}
</ul>