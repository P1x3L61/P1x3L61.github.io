---
layout: wpub_assignment
permalink: /wpub/zadanie1/
title: "WPUB: Zadanie 1"
author: tibensky

assignment-id: wpub_1
inprogress: false
---
Dokumentácia k prvému zadaniu
---
<!-- more -->
**Stránka využíva tieto layouty:**
- default
    - Základný layout, využíva *include* tag na importovanie hlavičky, pätičky a tela stránky
    - [Príklad]({{site.url}}/hobby/)
- classic <i class="little-text"> nadradený layout: detault</i>
    - Layout, ktorý obsah príspevku obohatí o nadpis, dátum vytvorenia príspevku, prezývky (id) autora. Okrem toho pridá pod príspevok odpis autora, ktorý obsahuje okrem mena aj krátku informáciu o autorovi.
    - Príkladom je aj táto podstránka.
- home <i class="little-text"> nadradený layout: detault</i>
    - Tento layout pridá na koniec príspevku zoznam posledne pridaných príspevkov. Zoznam je limitovaný na posledné 3 príspevky.
    - [Príklad]({{site.url}})
- hobby <i class="little-text"> nadradený layout: classic</i>
    - Layout určený na podstránky o hobby. Rozdeľuje obsah na dva stĺpce, pričom v ľavom stĺpci zobrazí náhľadový obrázok (angl. thumbnail) a v pravom stĺpci sa nachádza samotný text.
    - [Príklad]({{site.url}}/hobbies/movies/westworld/)
- project <i class="little-text"> nadradený layout: classic</i>
- wpub_assignment <i class="little-text"> nadradený layout: project</i>
    - Layout vytvorený pre účely dokumentácie zadaní WPUB. Pred samotný text príspevky vloží informácie o zadaní, ktoré načíta z dátového súboru. Tieto informácie (ako sú napríklad: krátky popis zadania, možný počet bodov, požiadavky) zobrazí v prehľadnej podobe a zároveň farebne aj textovo zobrazí, ktoré požiadavky boli splnené.
    - Príkladom je aj táto podstránka


**Medzi podstránky patria napríklad:**
- [home]({{site.url}})
- [o autorovi]({{site.url}}/o-mne/)
- [hobby]({{site.url}}/hobby/)
- [podstránka konkrétneho seriálu]({{site.url}}/hobbies/movies/westworld/)
- [profesia]({{site.url}}/profesia)
- [podstránka konkrétneho projektu]({{site.url}}/wpub/zadanie1/)

_ _ _

**Layouty využívajú niekoľko premenných:**
- author
    - Príspevky využívajúce layout *classic* a layouty od neho odvodené obsahujú atribút *author*, ktorý definuje, kto príspevok napísal. Na základe tejto premennej sa vygeneruje na konci príspevku správny podpis autora

- assignmnent_id
    - Podstránky s layoutom *wpub_assignmnet* využívajú premennú *assignmnent_id*, ktorá je potrebná na prístup k informáciam o zadaní z dátového súboru *projects_info.yml*. Tam sú uložené informácie ako krátky popis zadania, možný počet bodov za zadanie alebo požiadavky spoločne s informáciou, či boli v riešení zadania splnené alebo nie.

- thumbnail-url
    - Príspevky s layoutom *hobby* obsahujú tuto premennú, ktorá odkazuje na náhľadový obrázok v priečiku [files]({{site.url}}/files/). Náhľadový obrázok je použitý v layoute *hobby*, ako aj na podstránke *hobby*

- inprogress
    - Projektové príspevky obsahujú túto premennú na vyjadrenie, či je projekt stále aktívny, alebo už bolo dokončený a ďalej sa na ňom nepracuje. Tento atribút využíva layout *project*, ktorý podľa bool hodnoty pridelenej tejto premennej zobrazí informáciu, či je projekt dokončený alebo sa na projekte pracuje.
    


**Okrem premenných v šablónach používam aj premenné typické pre niektoré podstránky:**

- title
    - Titulka príspevku sa využíva v layoutoch *classic* a *home*. V *classic* sa titulka nastaví na začiatok príspevku, v *home* sa použije pri výpise najnovších príspevkov. Titulku obsahujú príspevky, ako aj iné podstránky (pages) webstránky. Titulka príspevku sa zobrazuje aj v titulnej hlavičke stránky v prehliadači.
- description
    - Podstránky (pages) ako [hobby]({{site.url}}/hobby/), [profesia]({{site.url}}/profesia) alebo [o autorovi]({{site.url}}/o-mne/) obsahujú premennú *description* ktorá obsahuje krátku slovnú definíciu webstránky. Tá sa používa napríklad na [úvodnej stránke]({{site.url}}) v rozcestníku webstránky v šablóne *home*.
- welcome-message
    - Táto premenná sa využíva na [domovskej stránke]({{site.url}}) a zobrazuje správu na privítanie. Premenná je uložená v konfiguračnom súbore.
- type
    - V kolekcii hobbies niektoré príspevky (o filmoch alebo seriáloch) obsahujú premennú *title*, ktoré určuje, že sa jedná o film alebo seriál.

_ _ _

**Stránka využíva tieto kolekcie:**
- hobbies
    - Kolekcia hobbies združuje príspevky, ktoré nemajú žiadnu chronologickú postupnosť a preto som sa rozhodol využiť kolekciu miesto článku (post). Ide o kolekciu markdown súborov, ktoré využívajú layout *hobby*

**Šablóny využívajú tieto dátové súbory:**
- people.yml
    - Dátový súbor obsahuje informácie o autoroch. Tieto informácie využíva napríklad layout *classic* na vytvorenie podpisu autora, kde na základe premennej *author* získa z dátového súboru informácie ako meno, priezvisko a popis autora.
- projects_info.yml
    - Dátový súbor obsahuje informácie projektoch. Využíva ho napríklad layout *wpub_assignmnets*, ktorý na základe *assignmnent_id* získa informácie o zadaní a zobrazí ich v prehľadnej forme.

_ _ _

**Využitie filtrov:**
- V súbore footer.html, ktorý je importovaný v šablóne default:
{% highlight html %}
{% raw %}
<h2 style="float: left;" class="footer-heading">{{ site.title | escape }} (c) {{site.time | date: '%Y'}} </h2>
{% endraw %}
{% endhighlight %}

- v šablóne home:
{% highlight html %}
{% raw %}
<li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    {{ post.excerpt | strip_html}} <p class="little-text">dĺžka článku: {{post.content | number_of_words}} slov</p>
</li>
{% endraw %}
{% endhighlight %}

- v šablóne classic:
{% highlight html %}
{% raw %}
<p style="font-size: 12px;">{{page.date | date_to_long_string}}, {{page.author}}</p>
{% endraw %}
{% endhighlight %}

- v šablóne wpub_assignment:
{% highlight luqid %}
{% raw %}
{% assign posts = site.posts | where: "layout", "wpub_assignment" %}
{% endraw %}
{% endhighlight %}


**Využitie tagov:**

- include v layoute default:
{% highlight html %}
{% raw %}
    <html lang='{{ page.lang | default: site.lang | default: "sk" }}'>
    {% include head.html %}
    <body>
        {% include header.html %}
        {% include main.html %}
        {% include footer.html %}
    </body>
    </html>
{% endraw %}
{% endhighlight %}

- highlight a raw:
{% highlight html %}
{% raw %}
    {.% highlight html %}
    {.% raw %}
        <p style="font-size: 12px;">{{page.date | date_to_long_string}}, {{page.author}}</p>
    {.% endraw %}
    {.% endhighlight %}
{% endraw %}
{% endhighlight %}

_ _ _


**Využitie pluginov:**

Na stránke je nainštalovaný plugin [Emoji for jekyll](https://github.com/yihangho/emoji-for-jekyll), ktorý transformuje emoji kód na konkrétnu ikonu. 
Preto sa *: smile :* zmení na ikonu :smile:

_ _ _

**Pri tvorbe tejto webstránky bola použitá nasledovná [farebná schéma](http://www.colorcombos.com/color-schemes/7626/ColorCombo7626.html)**
![color-scheme](http://s3.amazonaws.com/colorcombos-images/users/1/color-schemes/color-scheme-7626-main.png?v=20150512172013)
