---
layout: unit
title: HTML Dokumente erstellen
permalink: /module/html_css/2/
categories: html_css
excerpt: "Lorem Ipsum Dolor"
navigation_group: module
theme: tomato_3
---

# HTML Dokumente Erstellen

## Text auszeichnen

Der Eigentliche Inhalt der Website wird in HTML vom `<body>` Element umschlossen. Innerhalb des bodys kommen HTML Elemente zum Einsatz, um Struktur, Zusammengehörigkeit und Semantik von Inhalten zu kommunizieren. Da heutige Websiten aus mehr als nur Text bestehen, stellt HTML5 ein Element vor, das den eigentlichen Content explizit auszeichnet, das `<main>` Element. Es umschließt den Tatsächlichen Inhalt der Seite.

Hier ist zu verstehen, dass dabei nicht alles als "Inhalt" identifizierbare davon gewrapped wird, sondern der Content, der zentral das Thema der Website kommuniziert.

> The main content section consists of content that is directly related to or expands upon the central topic of a document or central functionality of an application.

Lautet die [Definition des w3c's](https://www.w3.org/TR/2012/WD-html-main-element-20121217/). Nur Ein Main Element per Dokument darf verwendet werden.

### Fett, kursiv & Trennlinien

Reguläre Textverarbeitungsprogramme stellen Authoren die Möglichkeit zur Verfügung, Textpassagen auf **fett** oder _kurisv_ zu stellen. Die HTML Equivalenzen dazu sind `<strong>` und `<em>`, wobei ihre Aufgabe es nicht zwangsläufig ist, Text auf fett oder kursiv zu stellen. Das Default-Browser Styling hat das zur Folge, aber semantisch haben beide Elemente dedizierte Aufgaben:

Das `<strong>` Element zeichnet Textpassagen von Wichtigkeit aus. Das Strong Element kann auch genested werden:


``` html
<p><strong>Wichtig: Vergessen Sie nicht Ihren <strong>Regenschirm</strong> zuhause.</strong></p>
```

Das `<em>` Element (emphasis) wird zur speziellen Betonung verwendet. Abhängig davon, welcher Teil eines Textes hervorgehoben wird, kann sich die Bedeutung des Satzes semantisch verändern. Auch dieses Element kann genested werden.

Die Equivalenz zu Trennlinien ist das `<hr>` Element. Auch dieses Element spielt eine dedizierte, semantische Rolle. Es dient dazu, einen Inhaltlichen, thematischen Umbruch darzustellen, wenn ein Text sich auf ein Thema fokussiert, aber an dieser Stelle ein thematisch abweichender Text eingefügt wird, so wird `<hr>` verwendet, um diese Trennung auszuzeichnen. Im Default-Styling von Browsern wird das Element als Trennlinie dargestellt. Das `<hr>`-Element ist ein **leeres Element und umschließt nichts**.

``` html
<p>Frieren Sie Bananen in daumengroßen Stücken ein und werfen Sie sie in einen Hochleistungs Blender, um eine gesunde Alternative für ansonsten sehr zuckerhaltige Eiscreme zu erhalten.</p>
<hr>
<p>Ich habe schon von Personen gehört, die keine Bananen mögen. Für die funktioniert das Ganze auch mit gefrorenen Beeren.</p>
```

### Tabellarische Daten

Daten die in Tabellen angezeigt werden sollen, gehören in das `<table>` Element. Innerhalb von Tabellen werden Reihen mit `<tr>` und Zellen mit `<td>` gebildet:

``` html
<!-- eine Tabelle mit vier Reihen und drei Zellen -->
<table>
	<tr>
		<td>Frucht</td>
		<td>Farbe</td>
		<td>Zuckergehalt</td>
	</tr>
	<tr>
		<td>Banane</td>
		<td>gelb</td>
		<td>relativ hoch</td>
	</tr>
	<tr>
		<td>Himbeere</td>
		<td>dunkles Pink</td>
		<td>ganz ok</td>
	</tr>
	<tr>
		<td>Apfel</td>
		<td>von grün bis rot</td>
		<td>zu viel!</td>
	</tr>
</table>
```

Damit ist das wichtigste Grundgerüst einer Tabelle bereits aufgebaut. Zusätzlich können `<tr>`'s noch in Header, Body und Footer mit den Elementen `<thead>`, `<tbody>` & `<tfoot>` unterteilt werden.

### Gelöschte und neue Inhalte

Mit den Elementen `<del>` und `<ins>` kann entfernter, und hinzugefügter Text ausgezeichnet werden. Bei lebendigen Dokumente, an denen mehrere Personen arbeiten ist es oft wichtig, entfernten Text dennoch für eine gewisse Zeit sichtbar zu lassen, beziehungsweise neu hinzugefügten Text auch als neu zu erkennen.

Am meisten Sinn ergeben beide Elemente in Verbindung mit dem `datetime` & `cite` Attribut:

``` html
<p>Das Queer Film Festival <strong>Identities</strong> fand 2015 von <del datetime="2016-03-12">09. - 19. Juli</del> <ins cite="https://www.facebook.com/iQFFw/events">11. - 21. Juli</ins> statt</p>
```

`datetime` beschreibt dabei den exakten Zeitpunkt der Änderung, wohingegen das `cite` Attribut eine Quellenangabe für die Änderung in Form einer URL darstellt.

### Weiterführendes

+ `<main>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/main)
+ `<strong>` - [w3.org](https://www.w3.org/wiki/HTML/Elements/strong)
+ `<em>` - [w3.org](https://www.w3.org/wiki/HTML/Elements/em)
+ `<hr>` - [w3.org](https://www.w3.org/wiki/HTML/Elements/hr)
+ `<table>` - [w3.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)
+ `<del>` - [w3.org](https://www.w3.org/wiki/HTML/Elements/del)
+ `<ins>` - [w3.org](https://www.w3.org/wiki/HTML/Elements/ins)

## Bilder & Grafiken einfügen

Für Bilder wird das `<img>` Element verwendet. Es ist ein leeres Element und umschließt keinen Content. Dieses Element benötigt eine Textalternative, zur Verfügung gestellt vom `alt` Attribut:

> Except where otherwise specified, the alt attribute must be specified and its value must not be empty; the value must be an appropriate functional replacement for the image.

Schreibt das [w3c](https://www.w3.org/TR/html5/embedded-content-0.html#alt). Die Aufgabe hier ist es, nicht den Titel des Bildes in das `alt` Attribut zu schreiben, sondern einen Text zu wählen, der das Bild beschreibt, als wäre es nicht sichtbar. Sollte das Bild nicht geladen werden können, so wird dieser Text angezeigt. Wichtiger ist jedoch, dass somit der Inhalt des Bildes auch sehbeeinträchtigten Personen zugänglich bleibt.

Außerdem ist es zu empfehlen, dem Bild immer immer die `width` und `height` Attribute in pixeln mitzugeben. Der Grund dafür ist Performanceoptimierung. Ohne Angabe beider Attribute muss das Bild nach dem laden nochmal gerendert werden.

In Verbindung mit Bildern wird immer wieder das `<figure>` Element genannt. Das Figure element zeichnet jedoch einen seperaten inhaltlichen Kontext (Outline), der sich vom restlichen Kontext abhebt. Inhalt der Innerhalb des `<figure>` Elements ist wird auch als self-contained bezeichnet. Damit eignet es sich beispielsweise um ein Zitat, Codebeispiele oder bestimmte Grafiken, die auch _ohne Kontext für sich stehen können_.

``` html
<figure>
	<img src="img/infografik.jpg" alt="Daten">
	<figcaption><p>Infografik die spezielle Daten darstellt.</p></figcaption>
</figure>
```
Zusätzlich kann das `<figcaption>` Element verwendet werden, um den Inhalt um eine Bildunterschrift zu erweitern.

### Bildformate

Die am häufigsten vorkommenden Bildformate sind JPEG, PNG, GIF & SVG. Ihr Einsatz hängt immer vom Kontext ab. PNG eignet sich für mittelgroße bis große, Transparente Bilder, ist allerdings ein großes Bildformat. GIF eignet sich für einfache Grafiken und unterstütz auch Transparenz. JPEG ist das gängige Format für Bilder aller Art, lässt sich gut komprimieren unterstütz jedoch keine Transparenz. SVG ist das einzige Vektorformat auf dieser Liste. Es eignet sich für Grafiken.

_Hier ist es wichtig zu erwähnen, dass SVG nicht nur als Bildformat verwendet werden kann, sondern auch direkt in HTML eingebunden werden kann (inline SVG)._

Vor Allem bei JPEG Files ist es wichtig, die Kompression von Bildern nicht zu vergessen.

### Das `srcset` Attribut

Mit dem `srcset` Attribut gibt man dem Browser eine Auswahl an weiteren Versionen eines Bildes. Dabei überlässt man die Entscheidung dem Browser, welches Bild geladen wird, und welches nicht:

``` html
<img src="img/placeholder.jpg" alt="platzhalterbild" srcset="img/placeholder_big.jpg 2x, img/placeholder_huge.jpg 3x">
```

Das `x` als Einheit auf die URL des Bildes folgend beschreibt dem Browser, um wie viel diese Version größer als original ist. Dadurch kann der Browser beispielsweise für Retina Displays höherauflösende Bilder laden.

### Weiterführendes

+ `<img>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)
+ `srcset` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-srcset)
+ `<figure>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure)

## Navigation bauen

Um von einem Dokument zu einem anderen zu verlinken, verwendet man `<a>` Elemente. Diese können auch zum verlinken auf Sektionen innerhalb eines Dokuments verwendet werden. In dem Fall zeigt ihr `href` Attribut nicht auf eine URL, sondern auf die ID eines elements.

``` html
<a href="#blog-post">Zum Eintrag</a>
```

Eine Reihe an Links ist eine Liste und für Listen werden die Elemente `<ol>` (ordered list) und  `<ul>` (unordered list) verwendet. Beide Elemente dürfen nur `<li>` (list item) Elemente als direkte Kind-Elemente aufweisen:

``` html
<ul>
	<li>Apfel</li>
	<li>Himbeere</li>
	<li>Kürbis</li>
</ul>
```

Innerhalb von `<li>`'s darf dann wieder flow-content stehen, also auch Links:

``` html
<ul>
	<li><a href="index.html">Home</a></li>
	<li><a href="blog.html">News</a></li>
	<li><a href="about.html">Über Uns</a></li>
	<li><a href="contact.html">Kontakt</a></li>
	<li><a href="imprint.html">Impressum</a></li>
</ul>
```
Natürlich können auch Listen genested werden:

``` html
<ul>
	<li>Kaffee</li>
	<li>Tee
		<ul>
			<li>Schwarztee</li>
			<li>Grüntee</li>
			<li>Kräutertee</li>
		</ul>
	</li>
	<li>Alkohol</li>
</ul>
```

Eine oder mehrere Listen an Links, die gesammelt Links zur Navigation darstellen können mit dem `<nav>` Element eindeutig als Navigation gruppiert werden. Nicht jede Liste an Links ist aber gleich eine Navigation, wie beispielsweise eine Liste an Social Media Links.

``` html
<nav>
	<a href="index.html">Home</a>
	<ul>
		<li><a href="blog.html">News</a></li>
		<li><a href="about.html">Über Uns</a></li>
		<li><a href="contact.html">Kontakt</a></li>
		<li><a href="imprint.html">Impressum</a></li>
	</ul>
</nav>
```

Website Navigationen sind letzendlich nur eine Liste an Links. Der semantisch korrekte Ort für Navigationselemente ist üblicherweise das `<header>` Element. Header Elemente können mehrmals innerhalb eines Dokuments vorkommen, jeweils als Teil einer Outline. Innerhalb eines Header Elements darf kein weiteres Header Element vorkommen.

``` html
<header>
	<nav>
		<a href="index.html">Home</a>
		<ul>
			<li><a href="blog.html">News</a></li>
			<li><a href="about.html">Über Uns</a></li>
			<li><a href="contact.html">Kontakt</a></li>
			<li><a href="imprint.html">Impressum</a></li>
		</ul>
	</nav>
</header>
<main>
	<!-- Content -->
</main>
```


### Weiterführendes

+ `<header>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) bzw [w3.org](https://www.w3.org/wiki/HTML/Elements/header)
+ `<ul>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)
+ `<li>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li)
+ Flow Content - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories#Flow_content)
+ `<nav>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav)

## komplexe Strukturen abbilden

> sidebar mit aside, liste an ähnlichen Posts mit article, Authoreninformation in footer

Ein weiteres wichtige Element ist das `<article>` Element. Es beschreibt ähnlich wie das `<figure>` Element eine Komposition an self-containing content. Das kann eine Liste an News-Artikeln sein, ein einziger Blog-Post, ein Forum-Eintrag oder eine Auswahl an Artikeln in einem online Shop.

Mit einem `<article>` Element wird eine neue Outline erzeugt. Somit kann der Content im Element wieder mit `<header>` und auch dem `<footer>` Element sektioniert werden.

### Sektionierungen

Neben dem `<header>` Element gibt es auch das `<footer>` Element und das `<section>` Element, das zum Sektionieren von Content verwendet werden kann:

``` html
<!-- Mögliches Markup für einen Blog-Post -->
<article class="post">
	<header class="post__header">
		<h1>Titel meines Postes</h1>
		<p>Und in diesem Text schreibe ich mein Intro, oder auch den Auszug.</p>
	</header>
	<section class="post__content">
		<p>Hier steht der Hauptcontent meines Posts</p>
	</section>
	<aside class="post__related-posts">
		<ul>
			<li>
				<a href="post_1.html">
					<article>Ähnlicher Post 1</article>
				</a>
			</li>
			<li>
				<a href="post_2.html">
					<article>Ähnlicher Post 2</article>
				</a>
			</li>
		</ul>
	</aside>
	<footer class="post__footer">
		<p>Hier steht alles weitere, wie zum Beispiel Quellenangaben, oder Infos zum Author.</p>
	</footer>
</article>
```

Das `<section>` Element repräsentiert eine generische (aber inhaltliche / thematische) Sektionierung innerhalb des Dokuments. Es ist kein Ersatz für das generische Container-Element `<div>`.

Das `<aside>` Element wird üblicherweise für Sidebars, Randkommentare oder Glossare verwendet. Es präsentiert Content, der lose thematisch mit dem restlichen Content zusammenhängt, aber grundsätzlich für sich alleine stehen kann.

### Weiterführendes

+ `<article>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)
+ `<footer>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer)
+ Outlines: Defining Sections in HTML5 - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML_sections_and_outlines#Defining_Sections_in_HTML5)
+ `<section>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section)

## Content & Präsentation Trennen

Die Trennung von Ästhetik und Inhalt ist wichtig im Webdesign. Viele Prinzipien und Iterationen des Webdevelopments bauen auf dem Verständnis dieses Prinzips auf. Es ist der Grund, weshalb wir heute HTML zum Auszeichnen von Content vewenden und CSS um auf die Präsentation dessen Einfluss zu nehmen. Auszeichnungsprachen haben die Aufgabe, Content maschinenlesbar zu machen. Dabei stellt die Ästhetik keine Rolle. Tatsächlich könnte sie im Weg sein, wenn wir Elemente aufgrund ihrer Darstellung verwendenden anstatt für ihre semantische Implikation.

### Weiterführendes

+ Seperation of presenation and content - [wikipedia.org](https://en.wikipedia.org/wiki/Separation_of_presentation_and_content)
+ Seperation: The Web Designers Dilemma - [alistapart.com](http://alistapart.com/article/separationdilemma)
