---
layout: post
title:  "Môj prvý post!"
date:   2017-03-04 10:32:00 +0100
permalink: /:year/:month/:day/helloworld

---

Volám sa Peter Tibenský a toto je môj prvý príspevok :smile: .

![obrazok]({{site.url}}/files/helloworld.png)

*zdroj: [https://zh.wikipedia.org/wiki/File:HelloWorld.svg][img1-link]*

**Ďalšie články:**
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

**Autori\:**
<ul>
	{% for person in site.data.people %}
		<p>{{person.meno}} {{person.priezvisko}}</p>
	{% endfor %}
</ul>

[img1-link]: https://zh.wikipedia.org/wiki/File:HelloWorld.svg
