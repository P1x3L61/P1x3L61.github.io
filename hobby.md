---
layout: default
title: Moje hobby
permalink: /hobby/
description: "Moje hobby, voľnočasové aktivity a informácie o všetkom, čo ma zaujíma"
---
{{page.title}}
---

Medzi moje záľuby patrí okrem iného sledovanie filmov a seriálov. 


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
