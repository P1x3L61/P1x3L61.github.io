---
layout: wpub_assignment
permalink: /wpub/zadanie1/
author: tibensky
---

**Využitie filtrov:**
<!-- more -->
- V súbore filter.html:
    {% highlight html %}
        {% raw %}
<h2 class="footer-heading">{{ site.title | escape }} (C) {{site.time | date: '%Y'}} </h2>
        {% endraw %}
    {% endhighlight %}

- V súbore home.html:
    {% highlight html %}
        {% raw %}
            {{ post.excerpt | strip_html}}
        {% endraw %}
    {% endhighlight %}