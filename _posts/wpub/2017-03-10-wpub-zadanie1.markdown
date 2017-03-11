---
layout: wpub_assignment
permalink: /wpub/zadanie1/
title: "WPUB: Zadanie 1"
author: tibensky

assignment-id: wpub_1
possible-score: 6
short-description: "Tvorba webového sídla"
---

**Využitie filtrov:**
<!-- more -->
- V súbore filter.html:
    {% highlight html %}
        {% raw %}
<h2 class="footer-heading">{{ site.title | escape }} (C) {{site.time | date: '%Y'}} </h2>
        {% endraw %}
    {% endhighlight %}

- v súbore home.html:
{% highlight html %}
        {% raw %}
            <li>
                <a href="{{ post.url }}">{{ post.title }}</a>
                {{ post.excerpt | strip_html}} <p style="font-size:10px;">dĺžka článku: {{post.content | number_of_words}} slov</p>
            </li>
        {% endraw %}
{% endhighlight %}



*Pri tvorbe tejto webstránky bola použitá nasledovná [farebná schéma](http://www.colorcombos.com/color-schemes/7626/ColorCombo7626.html)*
![color-scheme](http://s3.amazonaws.com/colorcombos-images/users/1/color-schemes/color-scheme-7626-main.png?v=20150512172013)

