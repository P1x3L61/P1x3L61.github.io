---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
welcome-message: "Vitaj na mojom webe!"
---

{{page.welcome-message}}
---
Táto webová stránka vznikla ako projekt na predmet Webové publikovanie. Nájdete tu informácie o zaujímavých projektoch, ktoré som vyvíjal, ako aj informácie o rôznych veciach, ktoré ma zaujímajú.

<img style="margin-left: auto; margin-right: auto; width:128px; height:128px; display: block;" src="{{site.logo-url}}" alt="{{site.logo-alt}}" />

*Web je rozdelený do niekoľkých kategórií:*

<ul style="font-size: 14px;">
    {% for page in site.pages %}
           {% if page.title %}
                 <li><b>{{page.title}}</b> - <i>{{page.description}}</i></li>
           {% endif %}
     {% endfor %}
</ul>