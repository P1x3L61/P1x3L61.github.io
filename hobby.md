---
layout: default
title: Moje hobby
permalink: /hobby/
description: "Moje hobby, voľnočasové aktivity a informácie o všetkom, čo ma zaujíma"
---
{{page.title}}
---

Medzi moje záľuby patrí okrem iného sledovanie filmov a seriálov. Nižšie je zoznam mojich obľúbených seriálov, prípadne filmov.


<div class="wrapper">
  <hr>
    <h2>:movie_camera: Zoznam obľúbených filmov a seriálov :movie_camera::</h2>
    <ol class="ordered-list">
    {% for hobby in site.hobbies %}
    {% if hobby.type == "movie" or hobby.type == "series" %}
        <li style="margin-bottom: 20px;">
            <a href="{{hobby.url | relative }}" >
                <img src="{{site.url}}/files/{{hobby.thumbnail-url}}" class="thumbnail"/> 
                <b class="text-thumbnail">{{hobby.title}} </b>
             </a>
        </li>
    {% endif %}
    {% endfor %}
    </ol>
</div>

- - -

Okrem toho rád voľný čas vyplním prechádzkou po meste, prípadne v prírode. Hlavne tam musí byť mobilný signál :grinning:. V poslednej dobe ovšem všetok môj čas ochotne vypĺňajú školské zadania a tak som rád, keď vo voľnom čase môžem iba ležať a čumieť do blba.