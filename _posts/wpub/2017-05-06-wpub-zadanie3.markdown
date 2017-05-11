---
layout: wpub_assignment
permalink: /wpub/zadanie3/
title: "WPUB: Zadanie 3"
author: tibensky

assignment-id: wpub_3
inprogress: false
---

Dokumentácia k tretiemu zadaniu
---
<!-- more -->

**Opis typu dokumentu**

Na opis typu dokumentu som využil XML Schema, kde som vytvoril komplexné typy pre rôzne druhy slidov. Definoval som elementy ako aj ich atribúty a možné početnosti. Opis typu dokumentu sa nachádza v súbore ***schema.xsd***.

- Príklad komplexného typu pre jednostĺpcový slide
    {% highlight xml %}
        {% raw %}
	<!-- Typ jednostlpcovy slide-->
	<xs:complexType name="onecolumn-slide">
		<xs:sequence>
			<xs:element name="title" type="xs:string" />
			<xs:element name="paragraph" type="xs:string" minOccurs="1" maxOccurs="unbounded"/>
		</xs:sequence>
		<!-- Atribut hovoriaci, ci maju byt odrazky cislovane-->
		<xs:attribute name="ordered" type="xs:boolean" use="optional" default="false"/>
	</xs:complexType>
        {% endraw %}
    {% endhighlight %}

- - - 

**Vytvorenie ukážkovej prezentácie**

Súbor ***prezentacia.xml*** predstavuje ukážkovú prezentáciu, ktorá je správne vytvorená a validná voči schéme. Ide o ukážkovú prezentáciu využívajúcu všetky možnosti, ktoré sú v rámci opisu typu dokumentu možné. Prezentácia môže pozostávať z elementov a atribútov, ktoré bližšie opisujú vlastnosti prezentácie alebo jej obsah. 

Vytvoril som 7 typov slidov, pričom 2 z nich predstavujú automaticky generovaný titulný silde a obsahový slide. Prítomnosť týchto slidov môže používateľ ovplyvniť vložením elementu ***title-slide***, prípadne ***content*** medzi slidy prezentácie.

Medzi ostatných 5 slidov patrí:

- onecolumn-slide - Slide s jedným stĺpcov odstavcov
- twocolumn-slide - Slide s dvoma stĺpcami odstavcov, pričom každý stĺpec má vlastný podnadpis
- image-slide - Slide so stĺpcom odstavcov na ľavej strane a obrázkom na pravej strane
- twoimage-slide - Slide s jedným odstavcom a dvoma obrázkami
- table-slide - Slide s odstavcom a s tabuľkou

Atribúty používané v prezentácii:

- Atribút *show-pagenum* typu boolean hovorí, či sa má na slidoch zobrazovať číslovanie slidov.
- Atribút *ordered* typu boolean určuje, či budú odrážky na jednostĺpcovom alebo dvojstĺpcovom slide číslované.
- Atribúty *src, src1, src2* pri slidoch s obrázkami určujú zdroj obrázku.
- Atribút *header* v tabuľkovom slide definuje riadok / riadky, ktoré sa majú považovať za hlavičkové.

- - -

**Základný návrh XSL transformácií**

XSL transformácie využívajú 3 súbory v závislosti od toho, či chce používateľ prezentáciu transformovať do XHTML alebo PDF. 

Súbor ***xslt.xsl*** predstavuje základný opis transformácie pre transformáciu do XHTML.

Súbor ***xslt-fo.xsl*** predstavuje základný opis transformácie pre konverziu na FO XML súbor, ktorý sa použije na transformáciu do PDF.

Súbor ***params.xsl*** obsahuje parametre a spoločné šablóny pre obe transformácie - do XHTML aj PDF.

Transformácie sú dostatočne parametrizované a parametre sú opísané v nasledujúcich odstavcoch. Návrh transformácií som členil na viacero šablón, ktoré sa pri transformáciách volajú rekurzívne. To sprehľadnilo kód transformácií a umožnilo viacnásobné využitie šablón, ako napríklad v prípade šablóny zachytávajúcej (angl. match) element ***paragraph***.

- - -

**Vytvorenie XSLT pre konverziu z XML do XHTML+CSS**

Na transformáciu XML prezentácie do XHTML som vytvoril súbor ***xslt.xsl***. Na vykonanie transformácie odporúčam využiť dávkový súbor ***html.bat***, ktorý som vytvoril pre tento účel a požaduje XML prezentáciu ako vstupný argument. Tento skript vykoná transformáciu XML prezentácie využitím XSLT a knižnice SAXON, pričom každý slide prezentácie transformuje na samostatný súbor. Tieto súbory skript uloží do priečinka ***slideshow***, do ktorého tiež prekopíruje všetky ***jpg*** súbory z priečinka, v ktorom bol spustený. Okrem toho prekopíruje do do priečinka ***slideshow*** aj CSS súbor so štýlmi, ktoré sú použité pre definovanie štýlov prezentácie.

Pred transformáciou je možné upravovať parametre v súbore ***params.xsl*** ako sú:

- author
  - Názvoslovie pre text "Autor"
- date
  - Názvoslovie pre text "Dátum"
- content
  - Názvoslovie pre text "Obsah"
- separator
  - Oddeľovač použitý pri zobrazení akutálneho čísla slidu a celkového počtu slidov
- width
  - Šírka prezentácie
- height
  - Dĺžka prezentácie
- file_prefix
  - Začiatok názvu XHTML súborov slidov
- previous_slide
  - Názvoslovie pre text "Predošlý slide"
- next_slide
  - Názvoslovie pre text "Ďalší slide"


Na slidoch sa automaticky generuje počítadlo slidov vo formáte *x / y*, kde x je aktuálne číslo slidu a y je celkový počet slidov v prezentácii. Separátor / je možné zmeniť v parametroch.

Každý slide sa generuje do vlastného xhtml súboru, ktorý je validným XHTML súborom obsahujúcim DTD aj XML namespace. Názov súboru je generovaný automaticky a to pomocou prefixu, ktorý je možné zvoliť v parametroch a následne automaticky vygenerovaného ID elementu. Titulný slide ako jediný nesie názov ***index.html***. Ukážka kódu na generovanie súboru pre každý slide:

{% highlight xml %}
{% raw %}
<xsl:for-each select="slides/*">

      <!-- Meno suboru, titulka = index -->
      <xsl:variable name="filename">
        <xsl:choose>
          <xsl:when test="name() = 'title-slide'">index</xsl:when>
          <xsl:otherwise><xsl:value-of select="$file_prefix"/><xsl:value-of select="generate-id(.)"/></xsl:otherwise>
        </xsl:choose>
      </xsl:variable>

      <xsl:result-document method="html" href="{$filename}.html">
      ...
      ...
      </xsl:result-document>
      ...
      ...
</xsl:for-each>
{% endraw %}
{% endhighlight %}

Štýly prezentácie som čo najviac oddelil od HTML kódu a preto sa nachádzajú v súbore ***styles.css***, na ktorý sa výsledné html súbory odkazujú. Dávkový súbor tento súbor so štýlmi v rámci vykonania prekopíruje do výsledného priečinku s prezentáciou.

- - - 

**Vytvorenie XSLT pre konverziu z XML do PDF**

Na transformáciu do PDF je potrebné najprv vytvoriť XML FO dokument. K tomu slúži súbor ***xslt-fo.xsl***, ktorý obsahuje šablóny na transformáciu. Na vykonanie transformácie z XML prezentácie do PDF slúži dávkový súbor ***pdf_xep.bat***, ktorý požaduje XML prezentáciu ako vstupný argument. Tento skript bol použitý aj v druhom zadaní. Skript vykoná transformáciu do XML-FO a následne do PDF.

Pred transformáciou je možné upravovať parametre v súbore ***params.xsl*** ako sú:

- author
  - Názvoslovie pre text "Autor"
- date
  - Názvoslovie pre text "Dátum"
- content
  - Názvoslovie pre text "Obsah"
- separator
  - Oddeľovač použitý pri zobrazení akutálneho čísla slidu a celkového počtu slidov
- h1 až h6
  - Veľkosti písma použité v prezentácii

Pre každý typ slidu som vytvoril vlastnú šablónu, v ktorej je vygenerovaný formátovaný obsah slidu. Ukážka šablóny pre slide typu *image-slide*:
{% highlight xml %}
{% raw %}
  <xsl:template match="image-slide">
    <fo:block-container text-align="center">
    	<xsl:apply-templates select="title" />
    	<fo:table text-align="left" padding-top="1cm">
    		<fo:table-body>
    			<fo:table-row>
    				<fo:table-cell padding-right="0.5cm" width="10cm">
    					<fo:list-block wrap-option="wrap" font-size="{$h5}" margin-left="1cm">
    						<xsl:apply-templates select="paragraph" />
    					</fo:list-block>
    				</fo:table-cell>
    				<fo:table-cell width="19cm">
    					<fo:block>
    						<fo:external-graphic src="url({@src})"   content-width="scale-to-fit"/>
    					</fo:block>
    				</fo:table-cell>
    			</fo:table-row>
    		</fo:table-body>
    	</fo:table>
    </fo:block-container>
  </xsl:template>
  {% endraw %}
{% endhighlight %}