---
layout: default
title: Home
---

<a href="https://www.crs4.it/" target="_blank"><img src="{{site.url}}/images/CRS4-logo.png" width="200"></a>
## [{{site.title}}]({{site.url}})

---

{::nomarkdown}

{% assign pages_list = site.pages | sort:"url" %}
    {% for node in pages_list %}
      {% if node.title != null %}
        {% if node.layout == "page"  and node.hide == null %}
          <a class="sidebar-nav-item{% if page.url == node.url %} active{% endif %}" href="{{site.url}}{{ node.url }}">{{ node.title }}
          <p class="note">{{node.summary}}</p></a>
        {% endif %}
      {% endif %}
    {% endfor %}
{:/}

--- 

### Authors and Contributors

 * [Rossano Atzeni](https://www.crs4.it/en/people/rossano-atzeni/)


Some of the materials used in this training are from the 
[Galaxy community](https://github.com/galaxyproject/training-material) and are the result of a collaborative work. 
Thanks to [all the contributors](https://github.com/galaxyproject/training-material/graphs/contributors) 
and the Galaxy Training Network!
