---
layout: default
title: O autorovi
permalink: /o-mne/
description: "Základné informácie o mne"
---
{{page.title}}
---
Volám sa Peter Tibenský a študujem Slovenskú technickú univerzitu v Bratislave. Navštevujem Fakultu informatiky a informačných technológií, kde študujem v :three:. ročníku. 

Táto webstránka vznikla ako projekt na predmet [Webové publikovanie][wpub] v akademickom roku 2016/2017. Táto stránka okrem iného obsahuje aj dokumentáciu k zadaniam z tohoto predmetu, ktoré môžete nájsť v sekcii [projekty]( {{site.url}}/projekty/ ), alebo na nasledujúcich odkazoch:

{% assign posts = site.posts | where: "layout", "wpub_assignment" %}


<ul>
    {% for post in posts %}
        <li>
            <a href="{{post.url | relative}}" >{{post.title}}</a>    
        </li>
    {% endfor %}
</ul>



[wpub]: https://wiki.fiit.stuba.sk/study/bc/info/wp/
