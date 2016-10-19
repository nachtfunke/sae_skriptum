---
layout: unit
title: HTML Basics
permalink: /module/html_css/1/
categories: html_css
excerpt: "Geschichte, Herkunft und Grundlagen von HTML - Einführung in die Grundbegriffe, Syntax und Struktur von HTML Dokumenten."
navigation_group: module
theme: tomato_2
---

# HTML Basics

Öffnet man eine Website, so sieht man heute allerhand Bilder, Videos, Texte, Animationen - all dem gibt HTML halt. Wenn wir Websites ansehen, so laden wir uns diese von einem Server. Und was wir uns geladen haben, können wir auch direkt ansehen, einfach auf "Seitenquelltext anzeigen" gehen, und schon offenbart sich uns das Gerüst (fast) aller Inhalte des Webs. Wie kam es dazu?

## Das Web der Dokumente

Im deutschen Sprachgebrauch machen die meisten Personen keinen Unterschied zwischen dem _World Wide Web_ oder dem _Internet_, obwohl beide nicht dasselbe meinen. Spricht man vom _Web_, so ist damit das WWW, ein Raum an identifizierbaren Informationen gemeint. Dieser Raum nutzt das Internet, ein Netzwerk an Netzwerken, das Computer nutzen, um Daten via TCP/IP auszutauschen.

### Das Internet

> The Internet is the global system of interconnected computer networks that use the Internet protocol suite (TCP/IP) to link billions of devices worldwide.

Sagt Wikipedia. Der Ursprung des Internets liegt in den 1960ern der USA, im ARPANET. Das _Advanced Research Projects Agency Network_ war ein Computernetzwerk, das die amerkanische Ost- mit der Westküste verband und das erste Netzwerk, das das TCP/IP Protokoll adaptierte. Es wurde vom _United States Department of Defense_ finanziert.

Das _TCP/IP_ Protokoll (Transmission Control Protocol / Internet Protocol) definiert die Kommunikation zwischen Rechnern, die anhand einer zugewiesenen IP identifizierbar sind. Das Protokoll wurde ursprünglich für das ARPANET entwickelt.

Das ARPANET hatte zur Aufgabe, regionale akademische und militärische Netzwerke zu verbinden. Der TCP/IP Standard wurde in den 1980ern schließlich von weiteren Netzwerken innerhalb und außerhalb der USA adaptiert und diese wurden schließlich miteinander verbunden. Als in den 1990ern kommerzielle Netzwerke und Firmen an das Internet angeschlossen wurden, begann das Zeitalter des modernen Internets. Die entscheidende Rolle dabei spielte die Entwicklung des World Wide Webs.

### Entstehung des WWW

> The World Wide Web (WWW) is an information space where documents and other web resources are identified by URLs, interlinked by hypertext links, and can be accessed via the Internet.

Oder auch kurz, _the Web_. Es wurde 1989 von Tim Berners-Lee, einem Computerwissenschaftler erfunden. 1990 schrieb er auch den ersten Web Browser. Zur Entstehungszeit war dieser ein Mitarbeiter bei CERN. Als Vision sah Berners-Lee ein _information management system based on links embedded in readable text_. Da dieses Verhalten dem Begriff "Hypertext" entsprach und Tim Berners-Lee keinen Grund sah, Multimedia Inhalte davon auszuschließen, wurde der Begriff "Hypermedia" verwendet, der auch heute noch alles miteinschließt, was im Web zu finden ist. So begann die Entwicklung von HTML und HTTP, dem _Hypertext Transfer Protocol_, bis schließlich im Dezember 1990 der erste Webbrowser, Webserver und die erste Website geschrieben wurden.

### Webstandards

1994 gründete Tim Berners-Lee das _W3C_ (World Wide Web Consortium), mit der Aufgabe die Standards im Web weiterzuentwickeln. Entwickelt werden diese Standards von Arbeitsgruppen. So gibt es Arbeitsgruppen für HTML, CSS, Barrierefreiheit, etc. Von den vielen Veröffentlichungen, die als Standards gelten, bezieht man sich meistens auf _Recommendations_ für markup languages (wie HTML) oder CSS.

Browserhersteller haben sich nicht immer an die Empfehlungen der Standards gehalten, als sie in den Browser Wars um User kämpften und ein browser-eigenes feature nach dem anderen das Licht der Welt erblickte. Um diese wichtigen Standards den Browserherstellern und Developern näherzubringen, wurde das _Web Standards Project_ (WaSP) ins Leben gerufen. Viele der Gründer und Projektleiter dieses Projekts (Jeffrey Zeldman, Molly Holzschlag) sind auch noch heute Industry Leader und Stimmen mit Gewicht, innerhalb der Industrie. Dank der Arbeit des WaSP können wir uns heute zum größten Teil auf Web Standards verlassen.

## HTML

Was ist nun HTML genau? HTML bedeutet _Hypertext Markup Language_ und es wird verwendet, um Websites zu erstellen (kurzgesagt). HTML hat dabei die Hauptaufgabe, den Inhalt eines Webdokuments, einer HTML-Seite _semantisch_ zu beschreiben, damit ist HTML eine **Auszeichnungssprache**.

***

### Was ist eine Auszeichnungssprache?

Eine Auszeichnungssprache wird dazu verwendet, um Text für Maschinenlesbarkeit zu strukturieren und zu formatieren. Ohne eine Auszeichnungssprache hat der Computer keine Möglichkeit, etwas über die Natur des Textinhalts zu erfahren, wie dieser Gegliedert oder aufgebaut ist.

### Was ist Semantik?

Semantik heißt Bedeutungslehre und im Kontext von HTML ist damit die sinnhafte Verwendung von HTML-Elementen und Attributen gemeint.

***

Auch HTML ist ein sich weiterentwickelnder Standard im Web. Heute befinden wir uns in der Version 5, wohingegen bereits an 5.1 gearbeitet wird. HTML ist und bleibt ein elementarer Bestandteil des Webs.

Für Webentwickler ist HTML die Grundlage für alles Weitere. Webseiten sind in ihrem Kern immernoch Dokumente, die Inhalt beschreiben, auch wenn diese oft nicht so aussehen.

## Syntax & Aufbau von HTML Dokumenten

Sehen wir uns den Quellcode von Seiten an, so erkennen wir folgende Syntax:

``` html
<element>Inhalt</element>
```

Inhalt wird also in HMTL-Elemente, _Tags_ eingeschlossen. Ein Tag besteht aus einem öffnenden Größer-Zeichen `<`, dem Namen des Tags, und dem schließenden Kleiner-Zeichen `>`. Ein Element besteht also aus einem **Start-Tag** und einem **End-Tag**, welches jeweils durch den Slash hinter der aufgehenden Klammer `</>` definiert wird:

``` html
<p>Ich bin ein Blindtext.</p>
```

HTML-Elemente oder Tags umschließen also Inhalt, können aber auch weitere HTML-Elemente umschließen:

``` html
<div>
	<h1>Ich bin eine Überschrift!</h1>
	<p>Ich bin ein <strong>Blindtext</strong></p>
</div>
```

Damit kann HTML Inhalte nicht nur **Gruppieren**, sondern auch **Hierarchien und Zusammenhänge** ausdrücken. Diese Vorgehensweise nennt man auch _nesting_. Befindet sich ein Element in einem anderen Element, so spricht man von einem Eltern- bzw Kind-Element. Das Eltern-Element, in diesem Fall das `<div>`-Element, kann

Jedoch kann nicht jedes Element weitere Elemente nesten. Beispielsweise das `<img>` Element, das dazu verwendet wird um Bilder einzubinden:

``` html
<img src="/bild.jpg" alt="ein Platzhalterbild">
```

HTML-Elemente, die keinen Inhalt umschließen nennt man _leere Elemente_ (Empty Elements).

HTML-Elemente wie `<img>` werden noch näher mit _Attributen_ definiert:

``` html
<p>In diesem Text befindet sich ein <a href="http://www.google.at">Link</a> auf eine andere Website</p>
```

Hier befindet sich innerhalb des `<p>` Elements, dem _paragraph_, das für Absätze, also Fließtext verwendet wird, ein `<a>`, dem _anchor_, das einen Hyperlink um einen Text erzeugt. Das Linkziel des `<a>`-Tags wird mit dem `href`-Attribut definiert. Attribute werden in das öffnende HTML-Tag geschrieben, **nicht in das schließende**.

Die Syntax von Attributen sieht dabei immer gleich aus:

``` html
<element attribut="Wert"></element>
```

Manche Attribute sind **boolsche Attribute**, das heißt, ihr Wert ist nur entweder _true_ oder _false_:

``` html
<div disabled></div>
<div disabled="false"></div>
```

Dabei reicht es, das Attribut in das Element zu schreiben, ohne einen Wert zuzuweisen.

### Elementare Bestandteile eines HTML Dokuments

Jedes HTML-Dokument besteht aus einigen wenigen elementaren Grundbausteinen:

``` html
<html>
	<head>
		<title>Titel der Seite</title>
	</head>
	<body>
		<p>Hier steht der sichtbare "Körper" der Website.</p>
	</body>
</html>
```

Dies ist das Grundgerüst, das jede Website benötigt, um als theoretisch _komplett_ angesehen zu werden. Dieser gegliederte, hierarchische Aufbau wird als **DOM** (Document Object Model) bezeichnet.

Ganz außen umschließt `<html>` die gesamte Website. Eine Ebene darunter befinden sich der `<head>`, in dem sich generelle- und Metainformationen über die Seite, sowie für das Dokument notwendige Ressourcen befinden und der `<body>`, der den Content umschließt.

Diese Grundstruktur darf nur einmal per Dokument vorkommen, das heißt, innerhalb eines `<html>` Elements darf es nur einen `<body>` & `<head>` geben, zusätzlich müssen diese immer direkt auf das `<html>` Element folgen.

Innerhalb eines HTML Dokuments, kann der Author Kommentare einfügen, die vom Browser nicht gerendert werden und nicht Teil des DOM sind:

``` html
<p>Hier steht mein Blindtext.</p>
<!-- Dieser Kommentar wird vom Browser nicht dargestellt. -->
```

#### doctype

Ein weiterer wichtiger Teil jedes HTML Dokuments ist der _doctype_, der dem Browser bedeutet, HTML und CSS zu rendern. Er wird in der ersten Linie des Dokuments, noch vor dem `<html>` angegeben:

``` html
<!DOCTYPE html>
<html>
	<head><!-- Informationen & Ressourcen --></head>
	<body><!-- Inhalt (Content) --></body>
</html>
```
So sieht ein Dokument mit Doctype-Angabe für HTML5 aus. Die Schreibweise ist _case insensitive_, das heißt, dass Groß- oder Kleinbuchstaben keine Rolle spielen.

##### ältere Doctypes

In HTML 4.01 gab es mehrere Doctypes, die dem Browser jeweils zusätzliche Informationen mitgaben. Es gab drei Versionen des HTML 4.01 Doctypes: Transitional, Strict und Frameset:

Transitional:

``` html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

Strict:

``` html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

Frameset:

``` html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

Strict & Transitional bedeuteten dem Browser, wie dieser mit manchen alten Elementen umging. HTML hatte ursprünglich viele Elemente, die rein repräsentativ waren, das heißt, sie haben hauptsächlich Einfluss auf die Darstellung des Elements genommen. Strict erlaubt diese Elemente nicht mehr, das heißt der Browser würde sie als Fehler, _invalid_ einstufen und sie eventuell gar nicht darstellen. Transitional erlaubte diese Elemente allerdings noch.

Frameset erlaubte Webentwicklung mit Frameset-Content.

##### XHTML

Zusätzlich um bekannten HTML, gibt es außerdem noch XHTML. Es gab einen eigenen Doctype für XHTML allerdings wurde dieser von den Browsern nie flächendeckend implementiert, stattdessen gab man den **MIME-Type** im `<html>` Element an:

``` html
<html xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">
```

Dies hatte in erster Linie Implikationen für die Syntax. So wurden zum Beispiel leere Elemente in XHTML mit einem `/` geschrieben:

``` html
<img src="/image.jpg" alt="platzhalterbild" />
```

Vor HTML5 musste man sich entscheiden, ob man entweder mit der HTML oder XHTML Syntax arbeiten wollte. HTML5 unterstützt beide Syntaxen. XHTMl hätte ursprünglich HTML komplett ersetzen sollen, man entschied sich jedoch, HTML stattdessen weiterzuentwickeln. Heute wird XHTML kaum mehr verwendet.

#### head

Der `<head>` eines HTML Dokuments liefert generelle- und Metainformationen über das Dokument an. Zusätzlich listet er eine Reihe an Ressourcen, die für das korrekte Darstellen der Website benötigt werden:

``` html
<!doctype html>
<html>
	<head>
		<meta charset="utf-8">
		<meta http-equiv="x-ua-compatible" content="ie=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>Der Titel meines Webdokuments</title>
		<link rel="stylesheet" href="style.css">
		<script src="script.js"></script>
	</head>
	<body></body>
</html>
```

Hier passieren einige Dinge, daher gehen wir Zeile für Zeile durch:

``` html
<meta charset="utf-8">
```

Diese Zeile gibt die **Zeichensatz Codierung** (character encoding) des Dokuments an. Abhängig von den Verwendeten Zeichen, muss der Browser diese interpretieren, da er immer nur von den Zeichen ausgeht, die in der englischen Sprache verwendet werden. Es gibt eine Reihe an Zeichensätzen für verschiedene Sprachen und Usecases, die UTF-8 Angabe ermöglicht die Darstellung aller Zeichen.

``` html
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

Diese Zeile gibt an, in welchem Modus des Internet Explorers die Seite gerendert werden soll, falls diese im IE angesehen wird, in diesem Fall im Modus "Edge".

``` html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Wenn Websites auf Smartphones angesehen werden, so erzeugen manche Smartphones virtuelle Canvases, die größer sind als ihre tatsächliche Bildschirmauflösung, sodass breitere Websites denoch via pinch-zoom lesbar sind. Diese Angabe bedeutet dem Browser, dass diese virtuelle Canvas der Breite des Geräts entsprechen soll. Diese Angabe ist für fexibles Webdesign für alle möglichen Ausgabegeräte (Responsive Web Design) notwendig.

``` html
<link rel="stylesheet" href="style.css">
```

Dieses Element linkt ein Stylesheet `style.css`, ein Dokument das das visuelle Design des HTML Dokuments steuert.

``` html
<script src="script.js"></script>
```

Hier wird eine JavaScript-Datei `script.js` verlinkt. Sowohl das Stylesheet als auch das JavaScript-File werden vom Browser anhand der `src` und `href` Attribute nachgeladen. Das heißt, dass der Browser den `<body>` erst rendert, wenn alle Resourcen im `<head>` geladen wurden. Damit ist also mit Vorsicht umzugehen.

#### body

Im `<body>` steht dann der HTML Code, der den Inhalt der Website beschreibt. Neben dem regulären Inhalt können aber auch hier `<script>` Elemente auftauchen, um JavaScript zur Erweiterung von Funktionen in das Dokument zu laden.

### HTML-Elemente für den Anfang

HTML stellt eine große Reihe an Elementen zur Verfügung, um den Inhalt einer Website zu strukturieren. Ihre Aufgabe ist es, Content semantisch, also bedeutungsvoll in Struktur zu bringen und Hierarchien auszudrücken.

#### Links

Verlinkungen können mit dem `<a>`-tag und dessen `href` Attribut erstellt werden. Ein `<a>` wiederum HTML umschließen, allerdings darf innerhalb dessen kein weiteres `</a>` vorkommen.

``` html
<a href="http://www.google.com" target="_blank" title="Hier gehts zu google.com">Google</a>
```

Das Attribut `target="_blank"` führt dazu, dass das Linkziel in einem neuen Browsertab geöffnet wird. Das `title` Attribut zeigt dessen Value, wenn der User mit der Mouse über dem Link bleibt, ohne ihn zu klicken. Das `href` Attribut akzeptiert eine URL-Angabe. Insofern die Angabe `http://` weggelassen wird, ist der Link **relativ** und geht immer von der aktuellen URL aus.

#### Texthierarchien

Fließtext wird in HTML durch die Verwendung von Überschriften und Absätzen strukturiert. In HTML stehen 6 hierarchische Stufen zur Verfügung, von `<h1>`  bis `<h6>`. Dabei ist besonders auf die Semantik zu achten:

``` html
<!-- die Einrückungen sollen nur die Gliederung verdeutlichen -->
<h1>Früchte und Gemüse</h1>
	<h2>Früchte</h2>
		<h3>Steinobst</h3>
			<h4>Äpfel</h4>
			<h5>Granny Smith</h5>
			<h5>Ausbacher Roter</h5>
			<h5>Baldwin</h5>
			<h4>Pfirsiche</h4>
		<h3>Zitrusfrüchte</h3>
			<h4>Zitronen</h4>
			<h4>Limetten</h4>
			<h4>Orangen</h4>
		<h3>Beeren</h3>
			<h4>Panzerbeeren</h4>
				<h5>Kürbisse</h5>
					<h6>Butternut Squash</h6>
	<h2>Gemüse</h2>
```

Die Struktur, die durch die Verwendung dieser Elemente entsteht, nennt man auch **Outline**. Es gibt noch weitere Elemente, die die Outline beeinflussen, diese werden zu einem späteren Zeitpunkt nähergebracht.

Uns stehen außerdem noch die Elemente `<strong>` und `<em>` zur Verfügung, um Gewichtung und Betonung im Text auszudrücken. `<strong>` stellt dabei eine starke Betonung dar, gleich einer Anhebung der Stimmlautstärke, wohingegen `<em>` (emphasize) einer hervorhebende Betonung gleicht.

#### div & span

In Websiten werden immer wieder die Elemente `<div>` und `<span>` verwendet, um Elemente zu gruppieren. Sie haben beide keine semantische Bedeutung und können daher gefahrlos verwendet werden. Hierbei wird `<span>` üblicherweise innerhalb des Textes verwendet, wohingegen `<div>` verwendet wird, um andere Elemente zu gruppieren:

``` html
<div>
	<!-- Intro-Sektion des Textes -->
	<div>
		<h1>Überschrift</h1>
		<p>Intro-Text</p>
	</div>
	<!-- Hauptsektion des Textes -->
	<div>
		<h2>Unterüberschrift</h2>
		<p>Lorem Ipsum ...</p>
	</div>
</div>
```

#### Globale Attribute

Einige Attribute sind global und können auf beinahe jedes Element angewandt werden. Hier die wichtigsten für den Anfang:

##### class

``` html
<div class="text">
	<div class="text__intro">
		<h1 class="headline artikel__title">Überschrift</h1>
		<p>Intro-Text</p>
	</div>
	<div class="text__content">
		<h2>Unterüberschrift</h2>
		<p>Lorem Ipsum ...</p>
	</div>
</div>
```

Elementen Klassen zuzuweisen, erlaubt es, diese mit CSS oder JavaScript anzuwählen. In ein Element können mehrere Klassen gleichzeitig geschrieben werden, und Klassen können in mehreren Elementen vorkommen. Das macht Klassen zu einem wiederverwendbaren Gefäß für Funktion (JavaScript) und visuellem Design (CSS).

Wie diese Klassen heißen, ist dem Author überlassen, allerdings sollten die Klassennamen semantisch ausdrücken, was das Element tatsächlich tut.

##### id

Mit dem `id` Attribut, kann eine im Dokument einzigartige Bezeichnung für ein Element vergeben werden. Ein Element kann nur über eine eizige ID verfügen, die nicht ein zweites mal vorkommen darf innerhalb des Dokuments.

Der Sinn von ID's ist es, ein Element einzigartig identifizierbar zu machen.

##### style

Das `style` Attribut erlaubt es, CSS innerhalb eines Elements zu schreiben. Man spricht dann von Inline CSS. Darauf soll allerdings verzichtet werden, wenn es möglich ist.

## Weiterführendes

+ What is the difference between the Web and the Internet? - [w3.org](https://www.w3.org/Help/#webinternet)
+ Internet - [wikipedia.org](https://en.wikipedia.org/wiki/Internet)
+ So, who really did invent die Internet? - [nethistory.info](http://www.nethistory.info/History%20of%20the%20Internet/origins.html)
+ World Wide Web - [wikipedia.org](https://en.wikipedia.org/wiki/World_Wide_Web)
+ Preserving the Architecture of the Web with Stefan Tilkov - [thewebahead.net](http://thewebahead.net/116)
+ The Web Standards Project - [webstandards.org](http://www.webstandards.org/)
+ Properly Using CSS and JavaScript in XHTML Documents - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Archive/Web/Properly_Using_CSS_and_JavaScript_in_XHTML_Documents_)
+ Everything that goes in your `<head>` - [github.com](https://github.com/joshbuchea/HEAD)
+ Declaring character encodings in HTML - [w3.org](https://www.w3.org/International/questions/qa-html-encoding-declarations.en)
+ Character Encoding for Beginners - [w3.org](https://www.w3.org/International/questions/qa-what-is-encoding)
+ HTML Elements Reference - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
+ HTML Global Attributes - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)
