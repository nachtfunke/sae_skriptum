---
layout: page
title: CSS Basics
permalink: /module/html_css/3/
categories: html_css
excerpt: "Einführung in Cascading Stylesheets; Erklärung der Basis-Konzepte von CSS; Text-Styling"
navigation_group: module
theme: tomato_4
---

# CSS Basics

## Was ist CSS?

CSS bedeutet _Cascading Style Sheets_. Sie beziehen sich auf das Konzept der Kaskade, die **CSS Cascade**, ein Algorithmus, aus mehreren Eigenschaften entscheidet, welche Eigenschaft angewandt wird.

CSS hat die Aufgabe, HTML zu gestalten, anzumalen (paint), bzw. die Präsentation des HTML zu beeinflussen. Visuelles Design im Web wird also von CSS übernommen. Dabei greift es auf die Elemente im DOM-Tree zu, die sich aus der Struktur des HTML ergeben. Die zuvor mit HTML ausgedrückte Hierarchie und Gruppierung ist also die Grundlage für visuelle Design Systeme mit CSS.

Neben Layout, Text-Styling und User Interface Design, wird CSS ständig erweitert und ermöglicht auch einfache und komplexe Animationen. Bei CSS werden letztendlich nur Eigenschaften für Elemente definiert.

``` css
p {
	font-size: 14px;
}
```

Diese Zeilen haben zur Folge, das in unserem Dokument alle `<p>` Elemente auf die Schriftgröße 14px gesetzt werden. Der Gesamte Ausdruck wird als **Rule** bezeichnet, eine CSS-Regel. Eine Rule wird besteht aus einem _Selector_ und der _declaration_, damit ist alles gemeint, was sich zwischen den geschwungen Klammern `{ }` befindet:

``` css
selector {
	declaration
}
```

Eine Deklaration besteht jeweils wieder aus _property_ und _value_, also Eigenschaft und Wert. Property und Value werden von einem Doppelpunkt getrennt, und mit einem Semikolon `;` beendet. Da in einer Declaration mehrere Property-Value Paare auftauchen können, trennt das Semikolon diese voneinander.

``` css
selector {
	property: value;
	property: value;
}
```

In CSS dreht cih alles um Regeln, um die Eigenschaften von HTML Elementen die wir anpassen. Dazu müssen wir sie aber zuerst _selektieren_, das machen wir indem wir Selektoren schreiben.

## Selektoren schreiben

In dem ersten Beispiel haben wir bereits einen Selektor geschrieben `p { }`. Dabei handelt es sich um einen **Element-Selektor**, er selektiert HTML Elemente anhand ihrer Tag-Namen:

``` css
body { }
p { }
h1, h2, h3 { }
a { }
footer, header { }
article { }
hr { }
```

Der Element-Selektor spezifiziert allerdings keinen Kontext. Steht er so im Stylesheet, so selektieren sie **alle** Elemente des Typs, also alle `<p>`'s, alle `<h1>, <h2>, <h3>`'s, etc.

CSS kennt eine Reihe an Selektoren un der Element-Selektor ist nur einer davon.

### Universal-Selektor

``` css
* {
	color: red;
}
```

Der Universal-Selektor, erkennbar am `*` steht für **alles**. Er ist ähnlich dem Element-Selektor, nur dass dieser einfach alle Elemente allen Typs anspricht.

### Klassen-Selektor

``` css
.beliebiger-klassen-name {
	font-size: 1.5em;
}
```

Dieser Selektor beginnt mit einem Punkt `.`, dem ohne Leerzeichen der Name einer Klasse folgt. Die definierte Deklaration im CSS gilt dann für alle Elemente mit diesem Klassennamen - er selektiert **alle Elemente mit dieser Klasse**. Er ist der am häufigsten verwendeste Selektor beim Schreiben von CSS.

### ID-Selektor

``` css
#beliebiger-id-name {
	display: none;
}
```

Der ID-Slektor selektiert das **Element mit dieser ID**.

### Attribut-Selektoren

Manchmal möchten wir Elemente nicht aufgrund ihrer Klassen oder ID-Attribute selektieren, sondern eventuell aufgrund anderer Attribute:

``` css
[disabled] {
	pointer-events: none;
}
```

Dieser Selektor wählt alle Elemente, die über ein Attribut `disabled` verfügen. Dabei macht er keine Unterscheidung, was in dem Attribut steht, sondern nur ob das Element überhaupt über das Attribut verfügt. Das ist bei Boolschen Attributen kein Problem, aber manchmal wollen wir etwas genauer Selektieren:

``` css
[title="weiter"] {
	background-color: lemonchiffon;
}
```

Damit selektieren wir alle Elemente mit `title="weiter"`. Der Attribut Selektor ist sehr versatil und kann beispielsweise auch Elemente mit Attributen Selektieren, die einen Wert irgendwo in ihrem Value haben:

``` css
[href*="google"] {
	text-decoration: underline;
}
```

Hier wird jedes Element selektiert, dessen `href` in irgendeiner Form das wort `google` beinhaltet.

### Selektoren kombinieren

Diese Selektoren beziehen sich bis jetzt alle auf den Typ des Elements, aber nicht auf ihre Relation zu anderen Elementen. Natürlich gibt es auch dafür eine Reihe an Selektoren. Zuvor ist es aber wichtig zu wissen, dass Selektoren auch kombiniert werden können, wenn diese dieselbe Deklaration haben sollen.

``` css
a, p, .readable {
	letter-spacing: 0.1ch;
}
```

Hier werden alle `<a>`, alle `<p>` und alle Elemente mit der Klasse `.readable` selektieren. Um sich nicht immer zu wiederholen, kann man einfach alle Selektoren die man braucht in eine durch ein Komma `,` abgetrennte Liste an Selektoren schreiben. Diese Art von Slektor nennt man auch **Gruppenselektor**.

Selektoren verschiedener Arten können aber auch direkt kombiniert werden:

``` css
a[href^="https"] {
	text-transform: uppercase;
}
```

dieser Selektor kombiniert den Element- mit dem Attribut-Selektor. Sie gelten dann gemeinsam, also ein Element `<a>` mit einem `href` das mit `https` beginnt. Ein weiteres Beispiel:

``` css
div.commentBox {
	height: 30vh;
}
```

Dieser Selektor selektiert `<div>`'s mit der Klasse `commentBox`. Das heißt, dass Elemente anderen Typs nicht von dieser Rule beeinflusst würden, weil sie nicht selektiert worden sind. Wichtig dabei ist, dass bei dieser Art von Kombination kein Leerzeichen kommt. Stünde zwischen beiden Selektor-Arten ein Leerzeichen, so würde daraus der Descendant-Selektor.

### Descendant-Selektoren

``` css
.commentBox a {
	font-style: italic;
}
```

Diese Regel greift bei allen `<a>` **innerhalb** eines Elements mit der Klasse `.commentBox`. Man nennt ihn auch **Nachfahren-Selektor**. Hier ist es wichtig zu verstehen, dass der Selektor nur Elemente selektiert, die **in einer beliebigen Tiefe ein Nachfahre des Elements** sind. Das heißt, auch in einer ähnlichen Struktur wie dieser, würde die Regel immer noch greifen:

``` html
<div class="commentBox">
	<article class="commentEntry">
		<header>Kommentarname</header>
		<p>Lorem Ipsum, <a href="#">Link.</a></p>
		<a href="#">weiterlesen...</a>
	</article>
</div>
```

Man kann natürlich auch näher spezifizieren, wenn wir zum Beispiel nur alle `<a>` innerhalb von `<p>` selektieren wollen:

``` css
.commentBox .commentEntry p a {
	font-style: italic;
}
```

### Child Selektoren

Mit einem Child-Selektor können wir Elemente, die **direkte Nachfolger**, also Descendants sind, selektieren:

``` css
ul li > ul {
	text-ident: 1em;
}
```

Dieser Selektor selektiert alle `<ul>`, die direke Nachfolger, Kinder von `<li>`'s innerhalb einer `<ul>` sind.

### Adjascent Sibling Selektoren

``` css
p + p {
	margin-top: 0.75em;
}
```

Mit diesem Selektor können wir benachbarte Geschwisterelemente selektieren. Dieser Selektor greift auf jedes `<p>` das ein direktes Geschwistern-Element von einem `<p>` ist.

***

Kombiniert man einige der Selektoren die wir bis jetzt kennen gelernt haben, kann man bereits sehr interessante Regeln schreiben:

``` css
main > * + * {
	margin-top: 1rem;
}
```
Hier kombinieren wir einige Selektoren, gehen wir ihn Schritt für Schritt durch: In einem `<main>` mit direkten Nachfolgern `>` irgendeines Typs `*`, deren benachbarte Geschwisterelemente `+` irgendeines Typs `*`. Also _alle direkten Geschwister Elemente, die direkt auf das Element Main folgen_.

***

### nth-child, last-child, first-child

Manchmal muss man aber ein bestimmtes Kind-Element selektieren:

``` css
li:first-child {
	color: tomato;
}
```

der `:first-child` Selektor selektiert Elemente die ein **erstes Kind** sind. Also in diesem Fall jedes erste `<li>` Kind-Element. Es gibt auch den `:last-child` Selektor, der ein Element selektiert, wenn es das **letzte Kind** ist. Die Syntax für diese Art von Selektor beeinhaltet einen Doppelpunkt `:`. Damit drückt es einen **State** eines Elements aus.

Der `:nth-child()` Selektor kann noch genauer werden:

``` css
li:nth-child(4) {
	color: tomato;
}
```

Hier wird nur jedes `<li>` selektiert, das ein 4. Kindelement ist. Der nth-child Selektor ist sehr mächtig und kann sehr viel mehr ausdrücken, beispielsweise mit den keywords `even` und `odd`.

Neben den spezifischen Child-Selectors gibt es noch weitere Selektoren, die sich um verschiedene States eines Elements drehen:

### Einfache DOM-Events

CSS kann auf einfache DOM-Events reagieren:

``` css
a:hover {
	font-weight: bold;
}
```

Diese Regel greift, wenn der User mit der Maus über das Element fährt, dabei wir das MouseOver Event, in css das `:hover` Event ausgelöst. Es gibt noch einige andere Events:

``` css
a:visited { }
a:active { }
input:focus { }
```

Während `:active` gilt, wenn etwas angeklickt wird, greift `:focus` wenn das Fokus-Event ausgelöst wird, also beispielsweise wenn man in ein `<input>` Element klickt um etwas zu schreiben. `:visited` selektiert Links, die man bereits angeklickt hat.

### Weiterführendes

+ 30 CSS Selektors to memorize - [code.tutsplus.com](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
+ Selectors - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors)
+ Alphabetisch geordnete Selektor-Referenz - [css-tricks.com](https://css-tricks.com/almanac/selectors/)
+ Universal Selector - [css-tricks.com](https://css-tricks.com/almanac/selectors/u/universal/)
+ Attribute Selector - [css-tricks.com](https://css-tricks.com/almanac/selectors/a/attribute/)
+ Descendant Selector - [css-tricks.com](https://css-tricks.com/almanac/selectors/d/descendant/)
+ nth-child Selector - [css-tricks.com](https://css-tricks.com/almanac/selectors/n/nth-child/)

## Vererbung

Vererbung ist ein weiteres Kernkonzept von CSS. Es besagt, dass manche Eigenschaften nach unten vererbt werden, wenn diese in einem Element darüber gesetzt worden sind. Nicht alle Eigenschaften werden automatisch geerbt, aber einige, vor Allem Eigenschaften zum Text-Styling. Setzen wir die Schrift-Familie im HTML-Element, so wird diese nach unten weitervererbt, es sei denn wir beenden dieses Verhalten explizit

Für die Vererbung gibtes außerdem noch einen globalen Wert, der bei jeder fast Eigenschaft eingesetzt werden kann:

``` css
p {
	background-color: inherit;
}
```

Mit dem `inherit` Keyword können wir explizit die Vererbung von bestimmten Eigenschaften festlegen.

### Mit der Kaskade arbeiten

Eine gute Faustregel ist es, Eigenschaften die natürlicherweise vererbt würden, nicht mit dem Universalselektor `*` zu setzen, stattdessen die Deklarationen in einen HTML-Element Selektor, oder `:root` Selektor zu schreiben.

### Weiterführendes:

+ CSS Specificity and Inheritance - [smashingmagazine.com](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)
+ 

## Spezifität

Spezifität ist das mitunter wichtigste Thema bei CSS. Da wir nur Regeln mit Selektoren schreiben, kann es oft vorkommen, dass mehrere Regeln auf dasselbe Element zutreffen. Die **Spezifität** entscheidet dann, welche dieser Regeln zutrifft.

Jeder Selektor hat eine bestimmte Spezifität, abhängig von der Art des Selektors ist diese Nummer höher oder niedriger. Bei Kombinationen von Selektoren sind die Zahlen der Spezifität kummulativ und ergeben so eine Selektor-Spezifität.

Spezifität von Selektoren kann auch [ganz genau berechnet werden](http://specificity.keegan.st/).

Der Selektor mit der niedrigsten Spezifität ist der Universalselektor `*`. Der Selektor mit der höchsten Spezifität ist der ID-Selektor `#`. Auch Inline-Style hat eine Spezifität, diese ist auch höher als der ID-Selektor.

Als letzter Ausweg gilt dann noch das Keyword `!important`. Es überschreibt jede andere Regel.

Wichtig ist noch, dass bei gleicher Spezifität immer die Regel gewinnt, die als letztes vom Browser gelesen wurde. Auch CSS wird von links oben bis rechts unten gelesen, nachdem beim Browser ja nur eine lange Textzeile ankommt.

### Spezifität kontrollieren

CSS drückt ein Design System aus. Daher ist es wichtig, diese Styles so **abgekapselt** wie möglich zu schreiben. Behandelt man die einzelnen Bestandteile im Design als Komponenten, so können diese auch beinahe unabhängig von einander verändert werden. Daher ist es wichtig, die Spezifität von Regeln so niedrig wie möglich zu halten, damit spätere Neuerungen diese leicht überschreiben können. Wenn wir schon früh im Stylesheet mit id's oder sehr komplex kombinierten Selektoren arbeiten, müssen wir höhere Spezifität erzeugen um diese zu überschreiben und das kann zu Problemem führen.

Daher ist die goldene Regel, gewisse Dinge einfach zu vermeiden, wie zum Beispiel den ID-Selektor, oder `!important`. Design-Komponenten sollten bevorzugt mit Klassen gruppiert werden, im idealfall können die einzelnen Regeln an ähnlichen Namen bereits erkannt werden.

### Weiterführendes

+ Specificity - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
+ Specifics on CSS Specificty - [css-tricks.com](https://css-tricks.com/specifics-on-css-specificity/)

## Stylesheets kommentieren

Bei der Fülle an Selektoren ist es wichtig, Stylesheets gut zu organisieren. Es gibt eine Fülle von Methoden und Herangehensweisen an diese Thematik, wichtig dabei ist, ein System zu respektieren, wenn man sich für eines entschieden hat, auch wenn es das eigene ist.

Zum Organisieren von Stylesheets eignen sich Kommentare:

``` css
/*
	In CSS können natürlich auch Kommentare geschrieben werden.
	Diese können auch mehrzeilig sein.
*/
```

Bei Background-image übergeben wir in `url()` die URL der Bildatei. Per Default wird dieses Bild entlang der x und y Achse wiederholt, bis der gesamte Hintergrund des Elements ausgefüllt wurde.

## Text

CSS bietet einige Möglichkeiten Text zu stylen. Allen Anfang macht jedoch die Schriftart selbst. Im Web konnten wir bis vor nicht all zu langer Zeit nur auf eine kleine Auswahl an Schriftarten zugreifen. Das hat den einfachen technischen Grund, dass der Browser nur Schriftarten darstellen kann, die ihm zur Verfügung stehen, also die im Betriebssystem installier sind. Diese Unterscheiden sich natürlich stark von System zu System, daher gibt es nur wenige Schriftarten, die tatsächlich als **Web Safe Fonts** bezeichnet werden können:

+ Arial (sans-serif)
+ Courier New (monospace)
+ Georgia (serif)
+ Times New Roman (serif)
+ Trebuchet MS (sans-serif)
+ Verdana (sans-serif)

Das ist natürlich eine sehr schmale Auswahl. Dank weiterentickelter Webtechnologie, können wir heute auch Fonts benutzen, die nicht web safe sind. Mit Web Fonts werden die nötigen Datein der Schriftart einfach mit geschickt. Wie das genau funktioniert, wird in einer späteren Einheit erklärt.

### font-family

Um die Schriftart zu setzen, gibt es die eigenschaft `font-family`. Wir können hier den Namen der Schriftart direkt hineinschreiben, um diese zu setzen, aber wir können auch eine Reihe an _Fallbacks_ angeben, die dann angewendet werden, sollte die zuvor angegeben Schriftart nicht verfügbar sein:

``` css
font-family: Calibri, "Helvetica Neue", "PT Sans", Verdana, sans-serif.
```

Der Browser geht die Liste von vorne bis hinten durch und wendet an, was er kann. Sobald eine der Schriftarten zur Verfügung steht, wird nicht mehr weiter gesucht. Diese Liste an Schriftarten nennt man den **Font Stack**. Am ende steht dann meistens nur mehr noch, welche Art der Schriftart es sein soll. Als Mögliche Keywords dafür stehen `serif`, `sans-serif`, `monospace`, `cursive` & `fantasy` zur Verfügung.

### font-size

Diese Eigenschaft spricht für sich, sie legt die Größe der Schrift fest.

``` css
font-size: 18px;
```

Aber mit der Font-Size kann man mehr anstellen, als auf den ersten Blick zu sehen ist. Die Schriftgröße kann nämlich nicht nur in px angegeben werden. Eine Reihe von Values stehen zur Verfügung, allen Voran ist vor Allem `em` der vorrangige Wert um Schriftgrößen zu definieren.

`em` bezieht sich relativ auf die Schriftgröße im Eltern Element. Per Default ist die Schriftgröße immer 16px. Setzen wir also 1em so bedeutet das 16px.

``` css
font-size: 0.8em;
```

Ist die Default-Font size 16px, so ergibt 0.8em 12.8px. Damit lassen sich sehr gut Verhältnise darstellen. Ändert man im Eltern-Element die Font-size, so würden sich alle Font-sizes der Nachfahren die mit em angegeben wurden auch mitändern, weil sie sich immer auf den Wert des Eltern-Elements beziehen:

``` css
.comments {
	font-size: 12px;
}

.comments p {
	font-size: 1em; /* also 12px */
}

.comments h1 {
	font-size: 1.5em; /* also 18px, weil 12 * 1,5 = 18 */
}
```

Ändern wir jetzt in `.comments` die font-size auf 16px, so ergeben sich bei `p` eine font-size von 16px und bei `h1` eine font-size von 24px, ohne dass wir etwas in diesen CSS Regeln ändern mussten.

`em` ist eine **lenth-unit** in css. Das heißt, überall wo Länge angeben werden kann, kann auch em verwendet werden. Auch bei `width`, beispielsweise. Und immer bezieht sich dieses em auf die **font-size des Eltern-Elements**.

### color

Die `color` Eigenschaft ändert die Schriftfarbe:

``` css
p {
	color: #bada55;
}
```

Farben können in CSS auf verschiedene Arten angegeben werden, entweder mit ihrem Namespace, HEX-Wert, rgb und rgba, aber auch in hsl, bzw hsla. [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

### font-weight

Mit der Font-weight lässt sich das Schriftgewicht verändern, also wie bold der Text ist. Welche font-weights zur Verfügung stehen, hängt von der Font-family ab.

``` css
p > strong {
	font-weight: bold;
}
```

Font-Weights können entweder mit ihrem namespace oder mit ihrem numerischen Wert festgelegt werden. Ihr numerischer Wert geht von 100 bis 900.

``` css
font-weight: 100;
font-weight: 200;
font-weight: 300;
font-weight: 400; /* normal */
font-weight: 500;
font-weight: 600;
font-weight: 700; /* bold */
font-weight: 800;
font-weight: 900;
```

Mit dem namespace `lighter` und `bolder` kann außerdem noch festgelegt werden, dass die font-weight um eine Stufe leichter oder schwerer als das Eltern-Element sein soll.

### font-style

Mit font-style lässt sich text auf kursiv setzen:

``` css
p > em {
	font-style: italic;
}
```

### text-transform

Mit `text-transform` kann Großschreibung forciert werden.

``` css
h2 {
	text-transform: uppercase;
}
```

`uppercase` setzt alles auf Großbuchstaben, `lowercase` auf Kleinbuchstaben, `capitalize` auf Kapitälchen,

### text-decoration

Mit `text-decoration` wird hauptsächlich ein Unterstrich für Texte dargestellt.

``` css
p > span.underline {
	text-decoration: underline;
}
```

### text-align

Mit `text-align` wird die Textausrichtung festgelegt:

``` css
.commentBox {
	text-align: center;
}
```

Als mögliche Werte stehen zur Verfügung: `left`, `right`, `center`, `justify` & `justify-all`. Bei `justify-all` wird außerdem noch die letzte Textlinie in Blocksatz gesetzt, die ansonsten ausgelassen würde.

### text-indent

`text-indent` legt fest, wie viel Platz frei gelassen werden soll, bis die Textlinie beginnt.

``` css
.commentBox > p {
	text-indent: 1em;
}
```

Das hat zur Folge, dass die erste Textlinie des `<p>` erst nach 1em anfängt. Diese Eigenschaft betrifft nur die erste Linie von Fließtexten, es sei denn man hängt das keyword `each-line` an, allerdings ist dieses keyword noch experimentell und nicht weit supported.

### line-height

Mit `line-height` lässt sich die line-box-height von inline-elementen festlegen.  Bei block-level-elementen wird damit die minimalhöhe von line-boxes innerhalb des elements festgelegt. Text spannt sich über diese line-boxes, wir nehmen damit also Einfluss auf die Zeilenhöhe des Textes.

```
p {
	line-height: 1.5;
}
```

Als Wert akzeptiert auch line-height die lenght-values, aber auch eine Nummer oder Prozente. Diese beziehen sich dann auf die aktuelle font-size. Zu empfehlen ist es, immer die unitless-number methode zu wählen, da sie sich dann immer relativ zur aktuellen font-size ergibt.

### letter-spacing

Mit `letter-spacing` definieren wir den Abstand zwischen den einzelnen Characters.

```
p {
	letter-spacing: 0.1ch;
}
```

## Backgrounds

Backgrounds sind solide Farben, Gradients (Farbverläufe) oder Bilder.

### background-color

### background-image

### background-position

### background-repeat

### background-size

### Weiterführendes

+ Fundamentals in Text Styling - [developer.mozilla.org](https://developer.mozilla.org/en-US/Learn/CSS/Styling_text/Fundamentals)
+ font-weight - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight)
+ text-transform - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/text-transform)
+ text-align - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align)
+ text-indent - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/text-indent)
+ line-height - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height)
+ letter-spacing - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing)

