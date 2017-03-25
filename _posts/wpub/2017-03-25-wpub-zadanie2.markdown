---
layout: wpub_assignment
permalink: /wpub/zadanie2/
title: "WPUB: Zadanie 2"
author: tibensky

assignment-id: wpub_2
inprogress: false
---

Dokumentácia k druhému zadaniu
---
<!-- more -->
**Členenie textu na kapitola, podkapitola, podpodkapitola, príloha, generovaný obsah**

- Kapitola
    - Príklad: 
    {% highlight xml %}
        {% raw %}
<chapter>
    <title>Úvod</title>
    <para>
        Za posledné roky ...
    </para>
    ...
</chapter>
        {% endraw %}
    {% endhighlight %}

- Podkapitola & podpodkapitola
    - Príklad:
    {% highlight xml %}
        {% raw %}
<chapter id="analyza">
    <title>Analýza</title>
    <para>
      V tejto kapitole ...
    </para>
    <sect1>
      <title id="reprezentaciaOvP">Reprezentácia obrazu v počítači</title>
      <para>
        Na zobrazenie obrázkov...
      </para>

      <sect2>
        <title>Vektorová a rastrová grafika</title>
        <para>
          Existujú dva spôsoby...
        </para>
        ...
      </sect2>
    </sect1>

...
</chapter>
        {% endraw %}
    {% endhighlight %}

- Príloha
    - V prílohe je uvedený plán práce na letný semester
    - Príklad:
    {% highlight xml %}
        {% raw %}
<appendix>
  <title>Plán práce na letný semester</title>
  <para>V tejto prílohe uvediem ...</para>
  ...
</appendix>
        {% endraw %}
    {% endhighlight %}

- Generovaný obsah
    - Súčasťou dokumentu je aj automaticky generovaný obsah z tagov chapter, sect1 - 3, ktoré boli v práci využité.
    - Konfigurácia generovania obsahu a iných zoznamov v thesis.xsl:
        {% highlight xml %}
            {% raw %}
<xsl:param name="generate.toc">
book figure,table,title,toc
</xsl:param>
            {% endraw %}
        {% endhighlight %}   
- - -

**Zvýraznenie slov a členenia textu odrážkami alebo číslovaním**

- Zvýraznenie slov
    - Na zvýraznenie slov som využil tag *emphasis* a jeho atribút *role="strong"*, 
    - Príklad:
        {% highlight xml %}
            {% raw %}
    <listitem>
        <para>
        <emphasis role="strong">Osekávajúce prahovanie</emphasis> <emphasis>(angl. truncate threshold)</emphasis> – Osekávajúce prahovanie ...
        </para>
    </listitem>
            {% endraw %}
        {% endhighlight %}  

- Členenie textu odrážkami alebo číslovaním
    - V dokumente som využil ako členenie textu odrážkami (V prílohe dokumentu), tak aj číslovanie (Kapitola 2, Prahovanie)
    - Príklad:
    {% highlight xml %}
        {% raw %}
<orderedlist numeration="arabic">
    <listitem>
        <para>
        <emphasis role="strong">Binárne prahovanie</emphasis> - Výsledný obraz po segmentácii bude binárny. Toto prahovanie sa dá vyjadriť nasledovne:
        <equation>
            <title>Binárne prahovanie</title>
            <graphic align="center" fileref="obrazky/binary_threshold.png" />
            <alt>dst(x, y) = 1 | src(x, y) &gt; prah; 0 | inak</alt>
        </equation>
        </para>
    </listitem>

    <listitem>
        <para>
        <emphasis role="strong">Osekávajúce prahovanie</emphasis> <emphasis>(angl. truncate threshold)</emphasis> – Osekávajúce prahovanie odstráni z výsledného obrazu všetky tie body, ktoré nadobúdajú hodnotu väčšiu ako prah. Odstránením sa myslí nahradenie pôvodnej hodnoty prahovou hodnotou.

        <equation>
            <title>Osekávajúce prahovanie</title>
            <graphic align="center" fileref="obrazky/truncate_threshold.png" />
            <alt>dst(x, y) = prah | src(x, y) &gt; prah; src(x, y) | inak</alt>
        </equation>
        </para>

    </listitem>

    <listitem>
        <para>
        <emphasis role="strong">Prahovanie na nulu</emphasis> <emphasis>(angl. threshold to zero)</emphasis> – Posledný spôsob prahovania nastaví všetkým bodom, ktorých hodnota je menšia ako prah, nulovú hodnotu. Tým získame obraz, v ktorom zostanú iba body nad prahovou hodnotou.
        <equation>
            <title>Prahovanie na nulu</title>
            <graphic align="center" fileref="obrazky/to_zero_threshold.png" />
            <alt>dst(x, y) = src(x, y) | src(x, y) &gt; prah; 0 | inak</alt>
        </equation>
        </para>
        <para>
        K tejto operácii existuje aj inverzná, ktorá ponechá iba hodnoty pod prahovou hodnotou, a ostatné odstráni.
        </para>
    </listitem>

</orderedlist>
        {% endraw %}
    {% endhighlight %}

- - - 

**Odkazy na iné časti vlastného dokumentu, prípadne odkazy na URL**

V dokumente využívam ako odkazovanie iné časti vlastného dokumentu, tak aj odkazy na URL. Príklady:
- Kapitola "Vývojové prostriedky"
{% highlight xml %}
{% raw %}
<chapter id="analyza">
    <title>Analýza</title>
    ...
</chapter>
...
...
... Táto knižnica poskytuje rozhranie a implementáciu väčšiny metód spomenutých
v kapitole <xref linkend="analyza"/> od morfologických operácií,
cez segmentáciu až po metódy na modelovanie pozadia a detekciu objektov. ...
{% endraw %}
{% endhighlight %}

- Kapitola "Analýza", podkapitola "Detekcia pozadia"
{% highlight xml %}
{% raw %}
<footnote>
    <para>Video, na ktorom bola vykonaná akumulačná metóda: <emphasis>
    <ulink url="https://www.youtube.com/watch?v=U7HRKjlXK-Y">https://www.youtube.com/watch?v=U7HRKjlXK-Y</ulink>
    </emphasis>
    </para>
</footnote>
{% endraw %}
{% endhighlight %}

- - -

**Poznámka pod čiarou**

V dokumente je niekoľkokrát použitá poznámka pod čiarou, napríklad:
{% highlight xml %}
{% raw %}
<para>
      Doteraz boli techniky spracovania obrazu opísané v teoretickej rovine, 
      bez spomenutia počítačovej reprezentácie týchto operácií. Pri realizácii systému,
      ktorý je predmetom tejto práce a jeho návrh je opísaný v nasledujúcej kapitole, 
      bude použitá knižnica počítačového videnia OpenCV<footnote><para>Domovská 
      stránka knižnice OpenCV: <ulink url="http://opencv.org">http://opencv.org</ulink></para></footnote> (Open source 
      Computer Vision) verzie 3.1. Táto knižnica poskytuje rozhranie a implementáciu 
      väčšiny metód spomenutých v kapitole <xref linkend="analyza"/> od morfologických 
      operácií, cez segmentáciu až po metódy na modelovanie pozadia a detekciu 
      objektov. Na implementáciu grafického používateľského rozhrania sa predpokladá 
      použitie knižnice Qt<footnote><para>Domovská stránka frameworku Qt: <ulink url="https://www.qt.io">https://www.qt.io</ulink></para></footnote> .
</para>
{% endraw %}
{% endhighlight %}

- - - 

**Zoznam použitej literatúry vrátane citácie v texte**

Na konci dokumentu je uvedená bibliografia. Na prvky tejto bilbiografie sa odkazujem niekoľkokrát na rôznych miestach v dokumente.

Príklad odkazovania:
{% highlight xml %}
{% raw %}
...zakrytia časti útvaru iným objektom <xref linkend="12"/>....
{% endraw %}
{% endhighlight %}

Príklad bilbiografie:
{% highlight xml %}
{% raw %}
  <bibliography>
    <title>Použitá literatúra</title>

    <bibliomixed id="1">
      The United Nations. 2014. <title>World’s population increasingly urban with more than half living in urban areas.</title>
      <bibliomisc>Dostupný online: <ulink url="http://www.un.org/en/development/desa/news/population/world-urbanization-prospects-2014.html">http://www.un.org/en/development/desa/news/population/world-urbanization-prospects-2014.html</ulink></bibliomisc>
    </bibliomixed>

...   

    <bibliomixed id="11">
      Sonka, M., Hlavac, V., Boyle,  R.: <title>Image Processing, Analysis, and Machine Vision</title>, Stamford: Cengage Learning, 2014, p. 920. ISBN 978-1-2859-8144-4
    </bibliomixed>

    <bibliomixed id="12">
      Fernandes, L. A., Oliveira, M. M.: <title>Real-time line detection through an improved Hough transform voting scheme</title>, Pattern Recognition, zv. 41, 1. vyd 2008, pp. 299 - 314. ISSN 0031-3203
    </bibliomixed>

    <bibliomixed id="13">
      Wang, H., Suter, D.: <title>A re-evaluation of mixture of Gaussian background modeling [video signal processing applications]</title>, rev. Proceedings. (ICASSP '05). IEEE International Conference on Acoustics, Speech, and Signal Processing, 2005., Melbourne, Victoria: IEEE, 2005, pp. 1117-1120. ISSN 1520-6149
    </bibliomixed>

...

  </bibliography>
{% endraw %}
{% endhighlight %}

- - -

**Obrázky, tabuľky, odkazy na ne, zoznam obrázkov a tabuliek**

Príklad obrázku:
{% highlight xml %}
{% raw %}
<figure id="diagram1">
          <title>Diagram aktivít zobrazujúci činnosti pri vyhodnocovaní obsadenosti parkovacích miest.</title>
          <mediaobject>
            <imageobject>
              <imagedata scalefit="1" width="100%" contentdepth="60%" fileref="obrazky/diagram1.png"/>
            </imageobject>
          </mediaobject>
</figure>
{% endraw %}
{% endhighlight %} 

Príklad tabuľky:
{% highlight xml %}
{% raw %}
<table frame="none" id="planPrace">
    <title>Plán práce na letný semester</title>
    <tgroup cols="2" colsep="1" rowsep="0">
      <colspec colnum="1" colwidth="0.5*"/>
        <thead>
          <row rowsep="1">
            <entry><emphasis>Obdobie</emphasis></entry>
            <entry><emphasis>Plán</emphasis></entry>
          </row>
        </thead>
        <tbody>
          <row>
            <entry>
              <emphasis>december - január</emphasis>
            </entry>
            <entry>
              <itemizedlist>
                <listitem>Dokončenie algoritmu na získanie modelu pozadia</listitem>
                <listitem>Implementácia rozhrania pre komunikáciu so serverom</listitem>
                <listitem>Implementácia rozhrania pre komunikáciu so serverom</listitem>
              </itemizedlist>
            </entry>
          </row>

          <row>
            <entry><emphasis>1. - 3. týždeň</emphasis></entry>
            <entry>
              <itemizedlist>
                <listitem>Dokončenie algoritmu na sledovanie pohybu vozidiel</listitem>
                <listitem>Implementácia algoritmu získania modelu parkoviska</listitem>
              </itemizedlist>
            </entry>
          </row>

          <row>
            <entry><emphasis>4. - 5. týždeň</emphasis></entry>
            <entry>
              <itemizedlist>
                <listitem>Dokončenie algoritmu na získanie modelu parkoviska</listitem>
                <listitem>Implementácia grafického používateľského rozhrania</listitem>
              </itemizedlist>
            </entry>
          </row>

          <row>
            <entry><emphasis>6. - 8. týždeň</emphasis></entry>
            <entry>
              <itemizedlist>
                <listitem>Prepojenie modulov na sledovanie pohybu objektov s modelom parkoviska</listitem>
                <listitem>Implementácia vyhodnocovania obsadenosti</listitem>
                <listitem>Dokončenie komunikácie so serverom</listitem>
              </itemizedlist>
            </entry>
          </row>

          <row>
            <entry><emphasis>9. týždeň</emphasis></entry>
            <entry>
              <itemizedlist>
                <listitem>Testovanie systému na dostatočne veľkom datasete</listitem>
                <listitem>Oprava chýb</listitem>
              </itemizedlist>
            </entry>
          </row>

          <row>
            <entry><emphasis>10. - 12. týždeň</emphasis></entry>
            <entry>
              <itemizedlist>
                <listitem>Oprava chýb zistených pri testovaní</listitem>
                <listitem>Písanie technickej dokumentácie</listitem>
              </itemizedlist>
            </entry>
          </row>

        </tbody>
    </tgroup>

  </table>
{% endraw %}
{% endhighlight %} 

Príklad rovnice:
{% highlight xml %}
{% raw %}
<equation>
    <title>Binárne prahovanie</title>
    <graphic align="center" fileref="obrazky/binary_threshold.png" />
    <alt>dst(x, y) = 1 | src(x, y) &gt; prah; 0 | inak</alt>
</equation>
{% endraw %}
{% endhighlight %} 
Príklad odkazov:
{% highlight xml %}
{% raw %}
<xref linkend="rastrovaReprezentacia"/>
{% endraw %}
{% endhighlight %} 
Zoznam obrázkov je automaticky generovaný na začiatku dokumentu vďaka konfigurácii v thesis.xml:
{% highlight xml %}
{% raw %}
<xsl:param name="generate.toc">
book figure,table,title,toc
</xsl:param>
{% endraw %}
{% endhighlight %} 

- - - 

**Register pojmov**
V dokumente som využil register pojmov. Na určenie pojmov som použil tag *indexterm* a následne v ňom pomocou tagov *primary*, *secondary*, *tertiary* definoval kľúčové slová.
Príklad:
{% highlight xml %}
{% raw %}
<indexterm>
    <primary>Segmentácia</primary>
    <secondary>Detekcia hrán</secondary>
    <tertiary>Cannyho detekcia hrán</tertiary>
</indexterm>
{% endraw %}
{% endhighlight %} 

Na konci dokumentu som napísal tag *index*, ktorý na danom mieste vygeneroval register.

- - -

Okrem týchto požiadaviek som upravil aj šablónu a to nasledovne:

thesis-tp-fo.xsl:

- Za názvom ústavu som nastavil 5cm medzeru, aby sa titulný názov práce zobrazoval nižšie, ako pôvodne.
- Zakázal som rozdelovaniu slov v názve univerzity

{% highlight xml %}
{% raw %}
<xsl:template name="book.titlepage.before.recto"><fo:block xmlns:fo="http://www.w3.org/1999/XSL/Format" text-align="center" font-size="20pt" border-bottom-width="0.5pt" border-bottom-style="solid" hyphenate="false" font-family="sans-serif" text-transform="uppercase">
      <xsl:value-of select="/book/bookinfo//affiliation/orgname"/>
    </fo:block><fo:block xmlns:fo="http://www.w3.org/1999/XSL/Format" hyphenate="false" space-before="6pt" text-align="center" font-size="14pt" font-family="sans-serif">
      <xsl:value-of select="/book/bookinfo//affiliation/orgdiv[@role='fakulta']"/>
    </fo:block><fo:block xmlns:fo="http://www.w3.org/1999/XSL/Format" space-before="3pt" space-after="5cm" text-align="center" font-size="12pt" font-family="sans-serif">
      <xsl:value-of select="/book/bookinfo//affiliation/orgdiv[@role='ustav']"/>
    </fo:block>
</xsl:template>
{% endraw %}
{% endhighlight %} 


thesis.xml:

- Nastavil som odsadenie odstavcov, aké využívam v bakalárskej práci. Teda nový odsek je oddelený prázdnym riadkom.
{% highlight xml %}
{% raw %}
<xsl:attribute-set name="normal.para.spacing"> 
  <xsl:attribute name="text-indent">
    <xsl:choose>
      <xsl:when test="preceding-sibling::para">1.5em</xsl:when>
      <xsl:otherwise>0em</xsl:otherwise>
    </xsl:choose>
  </xsl:attribute>
  <xsl:attribute name="space-before.optimum">0em</xsl:attribute>
  <xsl:attribute name="space-before.minimum">0em</xsl:attribute>
  <xsl:attribute name="space-before.maximum">1em</xsl:attribute>
</xsl:attribute-set>
{% endraw %}
{% endhighlight %} 