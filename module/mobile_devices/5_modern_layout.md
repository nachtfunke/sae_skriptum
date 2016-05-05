---
layout: page
title: Moderne Layout Techniken
permalink: /module/mobile_devices/5/
categories: mobile_devices
excerpt: "Die richtige Technik wählen: Tables, Floats, Flexbox & CSS Grid."
navigation_group: module
theme: grape_6
---

# Moderne Layout Techniken

In Zeiten von Responsive Web Design sind die technischen Anforderungen an Layout Techniken gestiegen. Es muss flexibel, einfach zu warten und skalierbar sein. Glücklicherweise entwickelt sich auch das Web ständig weiter und es gibt immer etwas neues am Horizont, das unsere aktuellen Probleme löst.

## Floats

Floats werden dazu verwendet, um zu beeinflussen, _wie Elemente auf den Web Flow reagieren_. Sofern Elemente nicht auf `display: none;` gesetzt oder der position-Eigenschaft verändert werden, sind sie Teil des Flows. Wird ein Element auf `float: <left|right>;` gesetzt, so wird es aus dem Flow genommen und rückt an die linke oder rechte Seite seines Container-Elements, behält aber seine Position in der Line bei, die sich aus der Source Order ergibt. Inline-Elemente und Bilder _fließen_ dann um das Element herum (they _wrap_ around the element).

Die Float Eigenschaft beeinflusst also eher, wie der Flow mit dem Element umgeht. Um dieses Verhalten wieder zu reseten, gibt es die Eigenschaft `clear: <left|right|both>;`. Elemente die _cleared_ wurden, setzen das Verhalten des Flows an der Stelle wieder zurück.

### Overflows & Clearfix

Da Elemente die _floated_ sind teilweise aus dem Flow genommen werden und nicht mehr Teil des Höhe-definierenden Contents innerhalb von Container-Elementn sind, entstehen oft Overflows. Dieses default Verhalten von Containern nennt man _collapsing_. Wie das Container-Element mit dem Overflow umgeht kann mit der Overflow-Eigenschaft gesteuert werden.

> The overflow property specifies whether to clip content, render scrollbars or just display content when it overflows its block level container.

In den meisten Fällen reicht `overflow: auto;`, um das Container-Element dazu zu bringen, eine Box um das Element zu zeichnen. Ultimativ besagt der Value `auto` allerdings, dass der Browser selbst entscheiden soll. Daher ist es normal geworden, einen "clearfix" auf Container-Elemente mit floating Elementen anzuwenden:

``` css
.clearfix:after {
    content: "";
    display: table;
    clear: both;
}
```

Source: [CSS-Tricks](https://css-tricks.com/snippets/css/clear-fix/)

### Weiterführendes

+ All About Floats - [css-tricks.com](https://css-tricks.com/all-about-floats/)
+ Force Element to Self-Clear its Children - [css-tricks.com](https://css-tricks.com/snippets/css/clear-fix/)
+ Overflow - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow)

## Flexbox

Mit flexbox können wir das Layout von von Elementen entlang einer Linie sehr flexibel und einfach kontrollieren. Dazu genügt es schon, das Container-Element auf `display: flex;` zu setzen. Damit wird das Container-Element zu einem _flex-container_ und alle **direkten** Child Elemente werden _flex-items_. Eigenschaften um das Verhalten in diesem Kontext zu steuern betreffen grundsätzlich entweder die Rolle des Elements als Container oder Items, **aber** ein Flex-Item kann wieder mit `display: flex;` zu einem Flex-Container gemacht werden, ohne dass es seine Eigenschaften als Flex-Item verliert.

### Eigenschaften für den Flex-Container

Das grundsätzliche flex-Verhalten wird im Container festgelegt:

``` css
.container {
    display: flex;
    flex-direction: row; /* default */
    flex-wrap: nowrap; /* default */
    justify-content: flex-start; /* default */
    align-items: stretch; /* default */
    align-content: stretch; /* default */;
}
```

All diese Properties steuern, wie sich direkte Child Elemente, also flex-items von `.container` verhalten. Der Code-Block zeigt die initial-Werte für diese Eigenschaften.

#### flex-flow: direction + wrap

`flex-direction: <row|row-reverse|column|column-reverse>;` und `flex-wrap: <wrap|wrap-reverse|nowrap>;` können mit der Shorthand Property `flex-flow: flex-direction flex-wrap;` zusammengefasst werden.

`flex-direction` steuert, wie _Lines_ innerhalb des Elements generiert werden (main-axis). Row definiert eine Hauptachse von _Links nach Rechts_, Column von _Oben nach Unten_. Reverse dreht die Linien jeweils um.

`flex-wrap` steuert, wie Flex-Items in der Line behandelt werden. Per default werden alle Flex-Items mit `nowrap` in eine einzelne Linie gedrückt und erzeugen keine neue Linie. `wrap` legt fest, dass eine neue Line erzeugt wird, wenn die Container-Breite von der Summe der Flex-item breite überstiegen würde.

#### justify-content

Diese Eigenschaft steuert, wie Flex-Items entlang der Line (Main Axis) ausgerichtet werden. Zur Option stehen: `justify-content: <flex-start|flex-end|center|space-between|space-around>;`.

#### align-items

Mit `align-items` lässt sich festlegen, wie Flex-Items entlang der Cross-Axis der _aktuellen Line_ ausgerichtet werden: `align-items: <flex-start|flex-end|center|stretch|baseline>;`

#### align-content

Diese Eigenschaft hat keine Wirkung, wenn Flex-Items sich nur in einer Line befinden. Wenn mehrere Lines entstehen, regelt die Eigenschaft, wie sich diese Lines entlang der Croxx-Axis ausrichten. `align-content: <flex-start|flex-end|center|stretch|space-around|space-between>;`

### Eigenschaften für das Flex-Item

Neben der expliziten Eigenschaft für das align-Verhalten (`align-self`), können noch Reihenfolge, Größe und Wachstumsverhalten von flex-items kontrolliert werden:

+ `flex-basis`: Definiert die default-Größe des Elements. `<length|content> | auto` - default: `auto`.
+ `order`: Beeinflusst die Reihenfolge im flex-flow.
+ `flex-grow`: Beschreibt das Wachstumsverhalten des flex-items mit einer proportionalen Nummer. `<number>` - default: `1`.
+ `flex-shrink`: Beschreibt das Schrumpfverhalten des flex-items mit einer proportionalen Nummer: `<number>` - default: `0`.
+ shorthand `flex`: `flex: flex-grow flex-shrink flex-basis;` (default: `flex: 0 1 auto;`)

### Weiterführendes

+ A complete Guide to Flexbox - [css-tricks.com](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
+ Flexbox Best Kept Secret - [medium.com](https://medium.com/@samserif/flexbox-s-best-kept-secret-bd3d892826b6)
+ Solved by Flexbox - [philipwalton.github.io](https://philipwalton.github.io/solved-by-flexbox/)
+ Flexbox Patterns - [flexboxpatterns.com](http://www.flexboxpatterns.com/home)
+ Flexbox Defense - [flexboxdefense.com](http://www.flexboxdefense.com/)
+ Flexbox Froggy - [flexboxfroggy.com](http://flexboxfroggy.com/)

## CSS Grid Layout

> CSS Grid Layout (aka "Grid"), is a two-dimensional grid-based layout system that aims to do nothing less than completely change the way we design grid-based user interfaces.

Chris Coyer, [css-tricks.com](https://css-tricks.com/snippets/css/complete-guide-grid/)

Mit CSS Grid Layout erlangen Webdeveloper und Designer eine CSS Implementierung eines Layout Tools das im editorial Print Design elementar ist und bisher mit anderen Layout Techniken wie Floats oder Tables imitiert wurde. Diese Technologie befindet sich noch in Entwicklung und sowohl ihre Fertigstellung als auch Implementierung wird noch ein wenig Zeit in Anspruch nehmen. Da neue CSS Features heute nicht mehr hinter vendor-prefixes entwickelt werden sondern hinter flags, können wir bereits mit der Technologie experimentieren. In Google Chrome geben wir in der Adresszeile `chrome://flags` ein und suchen nach den **Experimental Web Platform Features**, und stellen sicher, dass sie enabled sind.

Wie bei jeder neuen Technologie ist es wichtig, damit zu experimentieren. Das ist für Grid wichtiger als für jede andere neue Technologie die wir in den letzten Jahren hatten. Die Syntax ist noch etwas fremd und wirkt anfänglich etwas abschreckend. Ihr Potential erschließt sich tatsächlich im Umsetzen von sehr komplexen Grid-Systemen, in Verbindung mit Flexbox.

### Das Grid-Container-Element

Wie bei flexbox, reicht eine Eigenschaft, um einen Container für Grid zu definieren: `display: grid;`. Als nächstes müssen wir vertikale und horizontale Linien definieren:

``` css
.container {
    display: grid;
    grid-template-columns: 25% 25% 25% 25%;
    grid-template-rows: [row-1] 2em [row-2] 2em;
}
```

#### grid-template-columns & grid-template-rows

Diese Eigenschaften definieren Columns (Spalten) und Rows (Reihen) des Grids. Alle Length-Values können hier verwendet werden, zusätzlich gibt es noch den Wert `auto` und Fraction-units `fr`.

Dabei werden _Lines_ generiert (column & row), denen ein automatischer, numerischer Name gegeben wird. Man kann sie allerdings auch explizit benennen, wenn man das möchte:

``` css
.container {
    display: grid;
    grid-template-rows: [header] 50vh [content] auto [footer] 125px;
}
```

Das ist dann relevant, wenn man grid-items an speziellen Stellen im Grid positionieren möchte.

##### keyword repeat()

Mit dem `repeat()` keyword, kann man eine gewisse Anzahl an Definitionen wiederholen. Anstatt zu schreiben `grid-template-columns: 25% 25% 25% 25%;`, ginge auch `grid-template-columns: repeat(4, 25%)`.

##### Auto-Rows & Columns

In einem Grid für das Web gehen wir meistens davon aus, dass wir eine fixe Spaltenanzahl haben, allerdings nicht wissen, wie viele Reihen wir benötigen, weil unser Content eventuell dynamisch ist. Dabei helfen die Eigenschaften `grid-auto-rows: <length>;` und auch für columns `grid-auto-columns: <length>;`.

#### grid-column-gap & grid-row-gap (oder auch gutter)

Beim definieren von columns und rows ziehen wir Linien. Mit den Eigenschaften `grid-column-gap` und `grid-row-gap` können wir die Stärke dieser Linie und somit Gutter, also Abstände zwischen den Grid-Elementen definieren. Als Shorthand für beide Werte gibt es `grid-gap`.

#### grid-template-areas

Mit der Eigenschaft `grid-template-areas` können wir Rows & Columns zu benannten flächen definieren:

``` css
.container {
    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 400px auto 4em;
    grid-template-areas: "header header header header"
                         "artikel artikel artikel sidebar"
                         ". footer footer .";
}
```

Der `.` definiert hier leere Zellen. Grid-Items können dann diese Areas zugewiesen werden:

``` css
.header {
    grid-area: header;
}
```

### Die Grid-Item Element

Um die Element explizit entlang des Grids zu positionieren, werden die Eigenschaften `grid-column-start`, `grid-column-end`, `grid-row-start`, `grid-row-end` gesetzt (Shorthand: `grid-column: start/end;`, `grid-row: start/end;`). Als Value für diese Eigenschaften werden die Namen der Lines verwendet. Wenn keine Namen explizit gesetzt werden, sind diese numerisch und aufsteigend:

``` css
.container {
    display: grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-row: 20vh repeat(4, 5em) 300px; /* erzeugt 6 row-lines */
}
.element {
    grid-column: 2/3; /* Beginnt an column-line 2, endet an column-line 3 */
    grid-row: 2/span 4; /* Beginnt an row-line 2, endet an row-line 4 (spannt sich über 4 row-lines auf) */
}
```

#### keyword span

Mit dem keyword `span` kann man das Grid-Item _aufspannen_, entweder über die Anzahl, oder bis zur genannten Line aufspannen.

### Content innerhalb von Grid-Items kontrollieren

Eine Reihe an Eigenschaften gibt Kontrolle darüber wie der Inhalt von Grid-Items behandelt werden soll:

#### im Container:

+ `justify-items`: Richtet Content entlang der column-line aus `<start|end|center|stretch>`
+ `align-items`:  Richtet Content entlang der row-line aus `<start|end|center|stretch>`

#### im Element:

+ `align-self`:  Richtet Content entlang der row-line aus `<start|end|center|stretch>`
+ `justify-self`: Richtet Content entlang der column-line aus `<start|end|center|stretch>`

### Weiterführendes

+ **Rachel Andrew**: Introducing CSS Grid Layout - [youtube.com](https://www.youtube.com/watch?v=7oWUj8A1r_w)
+ Complete Guide to Grid - [css-tricks.com](https://css-tricks.com/snippets/css/complete-guide-grid/)
+ Grid by Example - [gridbyexample.com](http://gridbyexample.com/)

## Die richtige Technik wählen

Bei der Fülle von Layout-Techniken, ist es wichtig zu entscheiden, welche Technik für welche Situation gut geeignet ist. CSS Grid wird aus dieser Diskussion vorerst rausgenommen, da dessen Adaption noch dauert. Dazu muss man allerdings sagen, dass CSS Grid ab einem bestimmten Zeitpunkt den Hauptteil aller layout-Arbeiten übernehmen wird. In Kombination mit Flexbox, gibt es kaum 2D-Probleme, die Grid & Flexbox gemeinsam nicht lösen können.

### Tables?

HTML Tables haben eine explizite Semantik und sollten nicht für Layout verwendet werden. Allerdings werden immernoch Tables für Email-Layouts verwendet. Es ist nicht zu empfehlen, Email-Templates von Hand zu coden. Stattdessen werden in der Industry Email-Builder oder eine kompilierte Email-Sprache verwendet (Foundation).

#### Weiterführendes

+ Foundation for Emails - [foundation.zurb.com](http://foundation.zurb.com/emails.html)
+ mailchimp - [mailchimp.com](http://mailchimp.com/)

### Flexbox oder Floats?

Zum aktuellen Stand hören wir oft _"Just use flexbox."_. Ultimativ sollte man sich dennoch ein wenig um Browser-Support Gedanken machen. Respektiert man die Grundsätze von Progressive Enhancement so könnte man Beispielsweise das Basis-Layout mit Floats lösen, aber vertical-alignment mit flexbox lösen. Eine sichere Grundregel ist es vermutlich, Großes, Seiten-Layout-Definierendes mit Floats zu lösen, wohingegen kleinere Elemente darin bedenkenlos mit Flexbox gelöst werden könnten.

## Weiterführendes

### Artikel

+ Our New System for Layout - [24ways.org](https://24ways.org/2015/grid-flexbox-box-alignment-our-new-system-for-layout/)

### Videos

+ **Rachel Andrew**: The New CSS Layout - [youtube.com](https://www.youtube.com/watch?v=mVk7xMrcEMk)

### Podcasts

+ **The Web Ahead 114**: Layout Out the Future with Rachel Andrew - [thewebahead.net](http://thewebahead.net/114)
+ **The Web Ahead 115**: Predicting the Future with Rachel Andrew, Eric Meyer & Jeffrey Zeldman - [thewebahead.net](http://thewebahead.net/115)

### Newsletter

+ CSS Layout News - [csslayout.news](http://csslayout.news/)
