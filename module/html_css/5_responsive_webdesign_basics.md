---
layout: page
title: Responsive Web Design Basics
permalink: /module/html_css/5/
categories: html_css
excerpt: "Grundlagen des Responsive Webdesign"
navigation_group: module
theme: tomato_6
---

# Responsive Web Design Basics

Responsive Web Design ist ein Set an Webdevelopment Praktiken und Ansätzen, die zum Ziel haben, Websites für eine indefinite Anzahl an Bildschirmgrößen zur Verfügung zu stellen. Die Premisse hinter RWD ist, eine Website zu kreieren, die sich dann auf ihr Ausgabemedium flexibel anpasst, anstatt eine Trennung zwischen Mobil, Tablet und Desktop zu machen (adaptive design).

Responsive Web Design gibt dem Frontend Development auch die Kontrolle über diesen Prozess, wohingegen beim adaptiven Ansatz (also: m.website.com) meistens eine serverseitige Komponente im Spiel ist, die entsprechend anderes Markup zurückschickt.

Es gibt auch Fälle an denen adaptive Webdesign dennoch eine angemessene Lösung ist, wenn auch nur als Übergangslösung. Sehr komplexe Websites brauchen oft eine lange Zeit, ihre Frontend Architektur responsive neu zu entwickeln oder soweit anzupassen, dass diese bereit dafür ist. In so einem Fall kann eine dedizierte mobile Seite die bessere Lösung sein.

## Background

Der Begriff taucht erstmals in dem Talk "A Dao of Flexibility" von Ethan Marcotte bei _An Event Apart_ 2010 auf. Dem folgte auch der Artikel auf alistapart.com mit dem prägenden Titel "Reponsive Web Design".

Der Begriff wird von "Responsive Architecture" abgeleitet, die Architektur umfasst, die mit Hilfe von Sensoren Umweltfaktoren messen können und entsprechend ihre Form, Farbe oder Charakter anpassen können. Die Architektur _antwortet_, sozusagen. Bei Responsive Web Design machen Websites genau dasselbe: Sie passen sich auf ihr Ausgabemedium an.

Das Konzept wurde im selben Jahr, nur kurz nach dem Launch des iPads der 1. Generation geboren. Zu dieser Zeit war adaptive Design sehr üblich, also neben der Desktop Seite eine mobile Seite zu entwickeln, üblicherweise ein vom Server ausgehender Redirect auf eine mobile.site.com, oder m.site.com. Das iPad stellte Entwickler aber vor das neue Problem, dass eine dritte version einer Seite entwickelt werden müsste die für Tablet optimiert waren. Reponsive Web Design stellte damit die ideale Lösung für die Welt der multidevice User dar.

## Flexibles Layout

Der erste wichtige Bestandteil von Responsive Web Design ist das flexible Layout. Nicht allzulange zuvor war das _fluid layout_ noch Gang und Gebe, da für Layout Tables verwendet wurden. Zu dieser Zeit war das fluid layout jedoch aus der Mode gekommen, aus vielen Gründen, unter Anderem die starke Verwendung von CSS background-image's um skeomorphistisches Design zu ermöglichen und diese erwarteten pixel-perfekte Dimensionen.

### Der flexible Grid

Üblicherweise fand man früh im HTML Dokument ein wrapper div, dem eine fixe Breite gegeben und das zentriert wurde:

``` css
.wrapper {
	width: 960px;
	margin: 0 auto;
}
```

Die restlichen Layout-definierenden Elemente hatten ebenfalls exakte Pixel-Angaben, auch weil zu dem Zeitpunkt das Box-Model _content-box_ nicht leicht veränderbar war.

***

#### aside / box-sizing;

Setzt man es nicht anders, so ist der initial-value für diese Eigenschaft immer content-box. Das bedeutet, dass die Berechnung der width eines Elements sich aus der Breite des Contents, ohne Padding, Border oder Margin, ergibt. Setzt man mit CSS die Breite des Elements, so werden Padding und Border nicht abgezogen.

``` css
.button {
	width: 40px;
	padding: 0 5px;
	border: 1px solid #ddd;
	/*
		Die Berechnung der Breite des Elements beim Rendern:
		Content: 	40px
		Padding:	+10px (5px left, 5px right)
		border:	+2px (1px left, 1px right)
		--------------
		width:		52px;
	*/
}
```

`box-sizing: boder-box;` hat zum Effekt, dass von der Width des Contents noch Padding und Border abgezogen werden. Das heißt, dass wenn die Breite (oder Höhe) eines Elements gesetzt wird, vergrößern Padding oder Border diese nicht, sondern werden in die Berechnung miteingezogen.

``` css
.button {
	box-sizing: border-box;
	width: 40px;
	padding: 0 5px;
	border: 1px solid #ddd;
	/*
		Die Berechnung der Breite des Elements beim Rendern:
		Content: 	28px (content - padding - border)
		Padding:	+10px (5px left, 5px right)
		border:	+2px (1px left, 1px right)
		--------------
		width:		40px;
	*/
}
```

***

#### A: flexible Wrapper-Elemente

Das Wrapper-Element flexibel in seiner Breite zu setzen ist nicht kompliziert:

``` css
.wrapper {
	max-width: 960px;
	margin: 0 auto;
}
```

Die Breite des Elements ergibt sich aus der Natur von Block-Level-Elementen immer auf 100%, bis es eine maximale Breite von 960px erreicht hat.

#### B: flexible Layout-Elemente

Elemente die innerhalb eines Wrappers nebeneinander stehen wollen, müssen sich den zur Verfügung stehenden Platz teilen. Früher hat man hier mit genauen Pixel Werten gearbeitet.

``` css
.wrapper {
	max-width: 960px;
	margin: 0 auto;
}
.spalte_1 {
	width: 640px;
	float: left;
}
.spalte_2 {
	width: 320px;
	float: right;
}
```

Heute kann man sich auf relative Werte verlassen. Für Layout definierende Elemente eignen sich __Prozente__ am Besten. Verwendet man Prozent-Werte um die Breite von Elementen zu setzen, so beziehen sich diese immer auf 100% des darüber liegenden Elements, in den meisten Fällen bezieht sich das auf das Wrapper Element.

``` css
.wrapper {
	max-width: 960px;
	margin: 0 auto;
}
.spalte_1 {
	width: 66.6666667%; (640 / 960 * 100)
	float: left;
}
.spalte_2 {
	width: 33.3333333%; (320 / 960 * 100)
	float: right;
}
```

Verwendet man prozentuelle width-Angaben bei Elementen kann man tatsächlich sehr genau sein und einige Kommastellen mit angeben.

Nutzt man ein modernes Grid-System, das diese Rechnungen übernimmt, braucht man sich darüber keine allzugroßen Gedanken machen. Grid-Systeme bestehen aus einer Spaltenanzahl (üblicherweise 12), die bereits in Prozenten angegeben sind und auch Gutter (whitespace zwischen Spalten), meistens in Form von Margin, berücksichtigen.

In einer weiteren Einheit widmen wir einen großen Teil den Grid-Systemen und Layout-Engines.

***

#### aside / Weitere relative Werte

Relative Wertangaben machen das Arbeiten mit verschiedenen Bildschirmgrößen zu einem problemlosen Unterfangen. Der Umgang mit den Werten kann etwas mäßig anlaufen, vor Allem wenn man es gewohnt ist, in Pixeln zu denken. Nach einiger Zeit jedoch, lernt man die Vorteile von Werten wie `em` oder `ch` zu lieben und möchte nicht mehr darauf verzichten.

##### em, rem

`em` bezieht sich relativ auf die `font-size` des Elements. Font-size ist ein Wert der nach unten kaskadiert, das heißt, wenn man den Wert in einem Element setzt, so gilt dieser Wert für dessen Kind-Elemente. Verändert man also im html oder body diesen Wert nicht, so ist der default-Wert 1em = 16px.

`rem` bezieht sich immer auf die im root-element `<html>` gesetzte Font-size, nicht auf die vererbte font-size. Verändert man also die font-size von `<html>`, so verändern sich alle mit `rem` gesetzten Angaben ebenfalls.

##### vh, vw, vmin, vmax

`vh`, `vw`, `vmin` und `vmax` sind die Viewport-Units. Sie beziehen sich immer auf den Viewport des Dokuments. `vh` bezieht sich auf die Höhe des Viewports, `vw` auf dessen Breite. Dabei verhalten sie sich wie Prozente relativ zum Viewport und können von 0 bis 100 gesetzt werden.

`vmin` bezieht sich entweder auf Breite oder Höhe, je nach dem was gerade kleiner ist, und `vmax` je nach dem was gerade größer ist.

##### ch, ex

`ch` und `ex` sind font-family relative Werte. `ch` bezieht sich auf **die Breite des `0` Characters** und `ex` auf die x-height, **die Höhe des kleinen `x` Characters** und kann nicht kleiner als 0.5em werden. Diese Werte können sich mit der font-family ändern.

***

### Flexible Images

Bilder sind immer ein großes Thema im Responsive Web Design, weshalb wir dem Thema auch eine gesamte Einheit gewidmet haben. An dieser Stelle wird daher nur auf das Nötige eingegangen, um Bilder flexibel zu machen.

Grundsätzlich können wir als Webentwickler auf zwei technische Lösungen zugreifen um Bilder einzubinden, einerseits mit dem `<img>` Element, andererseits via css mit `background-image`. CSS gibt uns mehr flexible Möglichkeiten mit Bildern umzugehen, **aber**, dadurch werden Bildinhalte ihrer Semantik beraubt und in Dekoration verwandelt.

Hat ein Bild also die Aufgabe etwas inhaltlich zu kommunizieren, so ist das `<img>` Element zu wählen. Ist das Bild als Dekoration gedacht, so kann getrost `background-image` verwendet werden.

#### Inline-Images `<img>`

Ein einfaches Setting macht Bilder flexibel:

``` css
img {
	max-width: 100%;
}
```

Damit werden Bilder nicht kleiner als sie in ihrer natürlichen Größe wären, können aber auch nicht über ihren Container hinauswachsen. Hier kann man auch erwähnen, dass es in vielen Fällen auch kein Problem ist, `display: block;` zu verwenden. Das entfernt auch gleich den zusätzlichen Abstand unterhalb des Bildes.

#### CSS background-images

Setzen wir ein Bild via `background` so können wir auch auf `background-size` zugreifen.

``` css
.seriously_decorative_element {
	background: url('../img/cat.jpg') center center no-repeat;
	background-size: contain;
}
```

Interessant sind bei der `background-size` Angabe `contain` & `cover`.

_Contain_ zieht das Bild dabei so groß wie möglich auf, ohne dabei das Seitenverhältnis (aspect-ratio) zu verändern. Übersteigen Breite oder Höhe des Bildes den Container so wird das Bild _letterboxed_, der entstandene Platz wird mit background-color gefüllt (background-color default: transparent). Wird auch keine Angabe zur background-position gemacht, so wird das Bild automatisch auf beiden Achsen zentriert.

_Cover_ zieht das Bild so groß wie möglich auf, ebenfalls ohne dabei das Seitenverhältnis (aspect-ratio) zu verändern. Übersteigen Breite oder Höhe des Bildes den Container, so wird das Bild _clipped_, der über den Container hinausragende Teil des Bildes abgeschnitten.

## Mediaqueries

Mediaqueries existieren in ihrer Rohform schon seit CSS 2. Man konnte im Head abhängig vom mitgesandten media-type andere Stylesheets laden...

``` html
<link rel="stylesheet" href="css/main.css" media="all" />
<link rel="stylesheet" href="css/print.css" media="print" />
```

... oder im Stylesheet Media-Abhängige Blöcke definieren:

``` css
@media print {
	p {
		font-size: 12pt;
		color: #000;
	}
}
```

Die Mediaqueries, die wir für Responsive Web Design benötigen unterscheiden sich nicht zu stark in ihrer Syntax, sie wurden nur erweitert (Diese Syntax kann auch 1:1 für `<link />` übernommen werden).

``` css
@media screen and (max-width: 960px) {
	/* CSS Code für Screens deren Breite maximal 960px ist */
}
```

Allerdings gehen wir davon aus, dass die width von `screen` immer dem Viewport entspricht, und das ist nicht unbedingt der Fall. Als das iPhone 2007 auf den Markt kam, entsprach die Canvas im mobilen Safari auf der die Website gerendert wurde einer Größe von 980px, obwohl der Bildschirm des iPhones nur 320px breit war. Um Webdevelopern die Kontrolle über dieses Verhalten zu geben, stellte Apple ein neues Attribut für das `<meta />` tag vor.

### Den Viewport setzen

Um den Viewport zu setzen, sodass wir sicherstellen, dass unsere Mediaqueries sich immer auf den tatsächlichen Bildschirm beziehen und nicht auf die aufgezogene Canvas, verwenden wir das viewport-attribut des `<meta />` tags:

``` html
<meta name="viewport" content="width=device-width" />
```

Wir setzen also die Breite des Viewports auf die Breite des Geräts. Mediaqueries die sich also auf die `width` von `screen` beziehen, beziehen sich auf die Breite des Gerätebildschirms.

#### Zusätzliche Parameter

Neben dem Setzen des Viewports, kann man auch noch zusätzliche Kontrollen, zBsp. über die Zoomstufe ausüben:

``` html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
```

### Mediaqueries konstruieren

Mediaqueries haben zwei grundsätzliche Bestandteile, den Media-Type und das Query selbst:

``` css
@media <media-type> and (<query>)
```

Der `<media-type>` kann dabei sein `all`, `screen`, `print` oder `speech`. Hier gibt es aktuell noch support für mehr media-types, die allerdings ab CSS 4 nicht deprecated sind, also ist es zu empfehlen, sich auf diese 4 Media-Types zu begrenzen.

Das `<query>` besteht aus dem **feature** und dem **value**. Die Liste an features ist lange, daher nennen wir an dieser Stelle nur die aktuell relevantesten (Einheit 4 geht näher auf dieses Thema ein):

+ width, min-width, max-width, height - `<length>`
+ orientation - `<portrait|landscape>`
+ aspect-radio - `<integer/integer>`

### Mediaqueries managen ohne Preprozessor

Grundsätzlich bleiben uns als Webdeveloper mehrere technische Möglichkeiten. Wir können unseren angepassten Code als separate Stylsheets per Mediaquery im `<head>` verlinken, oder wir benutzen `@import` mit einem Query, wodurch der Import nur auf Treffen des Mediaquerys ausgeführt wurde, oder wir schreiben sie direkt in unser Stylesheet. Es ist zu empfehlen, keine zusätzlichen Ladezeiten dem User abzuverlangen, wenn es anders möglich ist. Daher ist es best-practice, die Mediaqueries direkt in das Stylesheet zu schreiben.

Benutzt man keinen Preprozessor wie SASS, so ist es zu empfehlen, die Mediaqueries absteigend nach Bildschirmgröße an das Ende des Stylesheets zu schreiben:

``` css
@media screen and (max-width: 960px) {
	/* ...wenn screen nicht größer ist als 960px */
}
@media screen and (max-width: 720px) {
	/* ...wenn screen nicht größer ist als 720px */
}
@media screen and (max-width: 480px) {
	/* ...wenn screen nicht größer ist als 480px */
}
@media screen and (max-width: 480px) and (orientation: landscape) {
	/* ...wenn screen nicht größer ist als 480px und die orientation landscape ist */
}
```

## Breakpoints

Der Begriff _Breakpoint_ definiert einen Stelle, an dem das Layout bright. Also zBsp. bricht das Menü um, oder die Schrift innerhalb einer Box kann nicht mehr gelesen werden. Breakpoints können entweder vordefiniert werden, zum Beispiel können gängige Bildschirmgrößen dazu verwendet werden. Oder, man passt bei der Entwicklung die Größe des Bildschirms an, und findet die Breakpoints manuell.

Letztere Möglichkeit sollte bevorzugt werden. Wer sich von gängigen Bildschirmgrößen abhängig macht, riskiert kaputte Layouts für Personen, deren Bildschirm nicht dem Mainstream entspricht. Und Responsive Web Design möchte genau dieses Problem lösen: Nicht für einzelne Geräte entwickeln, sondern für alle Bildschirme.

## Workflow Implikationen

RWD verändert die Art und Weise wie wir arbeiten und wie wir über verschiedene Prozesse denken. Eventuell verzichten wir auf Features, die nicht gut skalierbar sind oder wir bedenken Möglichkeiten auf Grund von Vorteilen, die wir nicht beachtet hätten, müssten wir nicht für eine unbekannte Anzahl an Bildschirmauflösungen designen.

### Der Prozess im visual Design

Designer die zum heutigen Zeitpunkt in die Industrie einsteigen, wissen bereits um Responsive Web Design Bescheid und suchen im besten Fall das Gespräch mit dem Developer oder liefern zumindest Anweisungen und multiple Mockups für die diversen Breakpoints / Ausgabegrößen der Website. Ist das nicht der Fall, ist es höchstens zu empfehlen, nicht die Arbeit des Designers abzunehmen, sondern statt dessen das Gespräch zu suchen.

#### Kommunikation

Viele Designer die multidisziplinär arbeiten, stellen oft nur Desktop Mockups und mit Glück Smartphone-Mockups zur Verfügung; Das reicht für RWD nicht. Zwischen Desktop und Smartphone liegen viele mögliche Breakpoints die alle bedacht werden müssen.

Im Idealfall sucht man das Gespräch mit Designern so früh wie möglich. Lieber stellt man eine Frage zu viel, als eine zu wenig.

## Weiterführendes

### Artikel

+ Responsive Web Design, 2010 - [alistapart.com](http://alistapart.com/article/responsive-web-design)
+ CSS: box-sizing - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)
+ Viewport Units, vh, vw, vmin, vmax - [web-design-weekly.com](https://web-design-weekly.com/2014/11/18/viewport-units-vw-vh-vmin-vmax/)
+ CSS: background-size - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size)
+ Using media queries - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
+ Using the Viewport Meta Tag - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)

### Podcast Episoden

+ A Responsive Web Design Podcast, Ethan Marcotte + Karen McGrane - [responsivewebdesign.com](http://responsivewebdesign.com/podcast/)

### Videos

+ A Dao of Flexibility, Ethan Marcotte 2010 - [vimeo.com](https://vimeo.com/34662135)

### Literatur

+ Responsive Web Design, Ethan Marcotte (~16€) - [abookapart.com](https://abookapart.com/products/responsive-web-design)
+ Going Responsive, Karen McGrane (~16€) - [abookapart.com](https://abookapart.com/products/going-responsive)
+ Responsive Design: Pattern & Principles (~16€) - [abookapart.com](https://abookapart.com/products/responsive-design-patterns-principles)