---
layout: default
title: Developerský profil
permalink: /profesia/
description: "Informácie o mojom vzdelaní, projekty, ktoré riešim alebo na ktorých som pracoval. Taktiež dokumentácia k zadaniam z predmetu Webové publikovanie"
---
WPUB projekty
---
<table class="list">
    <tr>
        {% for post in site.posts reversed %}
        {% if post.layout == "wpub_assignment"%}
            <td>
                <div class="list-cell">
                    <a href ="{{post.url}}" style="width: 100%; height: 100%; display: block;"> 
                    {{post.title}} 
                    </a>
                </div>
            </td>
        {% endif %}
        {% endfor %}
    </tr>
</table>

Iné projekty
---
<table class="list">
    <tr>
        {% for post in site.posts reversed %}
        {% if post.layout != "wpub_assignment" and post.layout == "project" %}
            <td>
                <div class="list-cell">
                    <a href ="{{post.url}}" style="width: 100%; height: 100%; display: block;"> 
                    {{post.title}} 
                    </a>
                </div>
            </td>
        {% endif %}
        {% endfor %}
    </tr>
</table>

- - - 
- - -

Moje vzdelanie:
---
**2014 - Súčasnosť:** Fakulta informatiky a informačných technológií (Slovenská technická univerzita), Bratislava

**2010 - 2014:** Gymnázium, Metodova 2, Bratislava

- - - 

Znalosti:
---
**Jazykové znalosti**

    Slovenský jazyk - materinský jazyk
    Anglický jazyk - aktívne 
    Nemecký jazyk - základy

**Administratívne a ekonomické znalosti**

    Strojopis - pokročilý

**Počítačové znalosti - používateľ**

    Microsoft Windows - pokročilý
    macOS - pokročilý 
    UNIX/Linux - pokročilý
    Microsoft Excel - pokročilý 
    Microsoft PowerPoint - pokročilý 
    Microsoft Word - pokročilý 
    OpenOffice.org Calc - pokročilý 
    OpenOffice.org Writer - pokročilý   
    Adobe Photoshop - základy 
    Adobe Dreamweaver - základy 
    Adobe Illustrator - základy
    Adobe After Effects - základy 
    Google AdSense - základy 
    Google Analytics - základy

**Počítačové znalosti - programátor**

    C - pokročilý 
    C++ - pokročilý 
    Java - pokročilý 
    PHP - základy 
    SQL - pokročilý 
    UML - pokročilý  
    Pascal - pokročilý 
    CSS - základy 
    HTML - základy 
    XML - základy 
    WordPress - pokročilý 
    MySQL - základy 
    PostgreSQL - pokročilý