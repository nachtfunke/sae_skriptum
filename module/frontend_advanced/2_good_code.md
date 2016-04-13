---
layout: page
title: Einheit 2 - Guten Code schreiben
permalink: /module/frontend_advanced/2/
categories: frontend_advanced
excerpt: "praktische Denkansätze und Arbeitsweisen: Methodologien folgen und mit Pre- & Postprozessoren Code schreiben."
navigation_group: module
theme: carrot_3
---

# Guten Code schreiben

Was guten Code auszeichnet ist im Detail subjektiv, allerdings gibt es einige Eigenschaften von denen grundsätzlich jede Codebase profitiert. Guter Code ist

+ skalierbar
+ lesbar
+ verständlich
+ modular
+ semantisch

Selbst wenn man alleine an einem Projekt arbeitet, ist es wichtig, auf diese Dinge zu achten. Als Entwickler befindet sich der eigene Workflow im ständigen Wandel und wird sich über die Jahre zwangsläufig mehrmals verändern. Das ist ultimativ eine gute Sache, aber man weiß nie, an welcher Stelle man ein altes Projekt wieder öffnen muss um daran zu arbeiten. Daher ist es wichtig, verständlichen und lesbaren Code zu schreiben.

Wir haben in der Webentwicklung große Freiheiten in unseren Arbeitsweisen. Es gibt wenige Schritte, die absolut vorgegeben sind und nicht anders gemacht werden können. Legt man also eine Philosophie die auf bestimmte Werte aufbaut dahinter, so werden diese Freiheiten zugunsten dieser Werte eingeschränkt.

## Frontend Development Methodologien

In den letzten Jahren haben sich vor Allem für Lesbarkeit, Verstänlichkeit und Modularisierung Methodologien hervorgetan. Es sind eher gemeinsame Ansätze, die sich auch über Naming Conventions äußern. Einigen sich ein Team auf eine Methodologie so fallen viele Fragen in der Zukunft weg, weil diese von der Methodologie beantwortet werden.

### OOCSS

Einer der frühesten Ansätze in diesem Bereich ist Object Oriented CSS (OOCSS) von Nicole Sullivan. Dessen größter Fokus ist Code Reusing. Beim OOCSS wird alles in Objekte, die sich in Klassen äußern, abstrahiert. Es trennt __Struktur (layout) von Skin__, und __Container von Content__. Das heißt, dass sich eine Klasse nur um die Struktur des Elements kümmert, während eine andere sich um den Skin kümmert. Das hat den Vorteil, dass wir sowohl Skin als auch Layout auf andere Elemente wieder anwenden können.

regulärer Code:

``` css

/* Alle Styles werden in einen kontextuellen Selektor geschrieben */
div.content > aside {
    background-color: tomato;
    padding: 1em;
    float: right;
    width: 25%;
    margin-bottom: 2em;
}

```

Dieser Selektor führ zwar zu dem was wir wollen, aber er stellt einige Bedingungen: das Element muss immer `<aside>` sein, es muss immer ein direktes Kind eines divs mit der Klasse `.content` sein. Was aber, wenn sich das Markup ändert? Dann müssen wir auch unser CSS anpassen. Und das kann man vermeiden.

``` css
/* Styles werden in wiederverwendbare Klassen abstrahiert*/
.sidebar {
    background-color: tomato;
    padding: 1em;
    margin-bottom: 2em;
}
.small_column {
    width: 25%;
}
.last {
    float: right;
}
```

In unserem HTML Code schreiben wir dann: `<aside class="sidebar small_column last">`. Nehmen wir eine dieser Klassen dann raus, so wird der Style nicht mehr angewandt. So können wir einerseits Styles komplett wiederverwenden, andererseits können wir HTML Seiten wie nach einem Baukastensystem zusammenbauen. Das ist dann auch sehr vorteilhaft, wenn man selbst hauptsächlich an Markup & Style arbeitet, ein anderer Entwickler aber zBsp. in PHP arbeitet und auf dieses Markup zugreift um sich eine Seite zu bauen, ohne im CSS Code herumzukramen.

Wie weit man dieses Abstrahieren nimmt, ist einem selbst überlassen. Vorsichtig sollte schon geboten sein, weil ab einem bestimmten Zeitpunkt zig Klassen im Element stehen und die Lesbarkeit dahin ist.

### SMACSS

SMACSS (Scaleable and Modular Architecture for CSS) ist ein System das von Jonathan Snook kreiert wurde. Gleich wie OOCSS hat das System zum Ziel, CSS Code so modular wie möglich zu machen. Dabei wird CSS in 5 Kategorien unterteilt:

+ base - generelle Elementselektoren, normalize / reset
+ layout
+ module - wiederverwendbare, modulare Komponenten, unabhängig von Kontext
+ state - verschiedene states eines modules, wie zBsp. hidden, expanded...
+ theme - verbleibende visuelle Aspekte, wie Farbschemen oder Typografie

Die Kategorierung im CSS Code selbst findet über die Naming Convention statt. Layout wird mit `.l-`, oder `.layout-` geprefixed und state mit `.is-`.

``` html
<article class="blog-post layout-3-cols is-listed">
    <h1 class="post-title headline">Lorem Ipsum</h1>
    <p class="post-excerpt desc"></p>
</article>
```

Und unser CSS beispielsweise:

``` css
.blog-post {
    padding: 1em 0;
    background-color: #fff;
}
.layout-3-cols {
    width: calc(100% / 3);
    float: left;
}
.is-listed {
    border-bottom: 1px dotted tomato;
    margin-bottom: 2em;
}
.headline {
    margin-bottom: 1em;
}
.desc {
    font-size: 0.857em;
}
.post-title {
    font-size: 1.5em;
}
.post-excerpt {
    margin-bottom: 1em;
}
```

Auch hier muss man für sich selbst entscheiden, was abstrahiert wird und was nicht. Hier sollte man auch erwähnen, dass ein wenig Kontext nicht schadet, solange man sich nicht im Kontextjungle verirrt. Abstrahiert man alles auf Selektoren mit der selben Spezifität, so wird bei überschneidenden Regeln immer die Regel angewandt, die zuletzt geschrieben wurde. Man könnte in diesem Beispiel getrost `.blog-post .title { ... }` schreiben.

### BEM

BEM steht für Block Element Modifier. Code wird grundsätzlich in Blocks, Elements und Modifier getrennt, ähnlich wie bei SMACSS auch erkennbar an der Naming Convention. BEM zeichnet sich durch besonders gute Lesbarkeit aus: `.block__element--modifier { ... }`. Auf den ersten Blick, erkennt man sofort, worum es dabei geht.

BEM löst in erster Linie ein Problem, dass bei sehr modularer CSS Architektur entsteht: Wir wissen oft nicht mehr, an welchem CSS wir arbeiten können und an welchem nicht, weil alles auf einzelne Objekte abstrahiert wurde die theoretisch überall vorkommen können. BEM löst dieses Problem, weil die Naming Convention auch Vorgaben für das Schreiben von Markup macht:

CSS

``` css
.blog-post {
    padding: 1em;
    background-color: #fff;
}
.blog-post--listed {
    border-bottom: 1px dotted tomato;
    margin-bottom: 2em;
}
.blog-post__title {
    font-size: 1.5em;
}
.blog-post__excerpt {
    margin-bottom: 1em;
}
```

HTML

``` html
<article class="blog-post">
    <h1 class="blog-post__title">Lorem Ipsum</h1>
    <p class="blog-post__excerpt"></p>
</article>
```

BEM produziert genau so abstrahierte und modularisierte Klassen, wie OOCSS. Wir können auch `<p class="blog-post__excerpt title"></p>` schreiben, wenn wir das brauchen. Dabei ist es jedoch wichtig, dass wir die Lesbarkeit nicht vergessen, sonst entsteht `<p class="desc blogpost__excerpt sidebar__text"></p>`. So ein Fall zeigt uns grundsätzlich an, dass wir Styles so modular beschreiben müssen, dass wir sie wiederverwenden können ohne dass sie die Lesbarkeit beeinflussen. So kann aus `sidebar__text` auch `text--small` machen und an den jeweiligen Stellen anwenden. Dabei geht es aber in erster Linie um die Lesbarkeit, die man nicht ignorieren sollte. Löscht man zBsp. das Sidebar-Modul (heißt, es kommt nicht mehr im Markup vor und verschwindet auch aus dem CSS), so greift die Regel auf einmal nicht mehr. Hat man den Teil jedoch abstrahiert, ist das kein Problem.

Blocks können auch Elements von Blocks sein:

``` html
<div class="wrapper--posts post-list">
    <article class="post-list__entry blog-post">
        <h1 class="blog-post__title">Lorem Ipsum</h1>
        <p class="blog-post__excerpt"></p>
    </article>
</div>
```

Hier bringt `.post-list` als neuer Block das Thema Kontext ins Spiel. Wir können auch hergehen, und im CSS `.post-list > .blog-post` schreiben, dabei limitieren wir uns aber, weil wir davon ausgehen, dass nur `.blog-post` in `.post-list` vorkommen können. Die Regel würde also nicht mehr greifen, wenn ein modifier ins Spiel kommt, oder andere Elemente ebenfalls dazukommen. Also macht man den blog-post-block zu einem post-list-element, in dem man die zusätzliche Klasse `post-list__element` dazugibt.

Bei mehreren Klassen hat sich ein Muster bewehrt: `<div class="reused-class  new-class"></div>` Haben beide Klassen dieselbe Spezifität, so kann `.new-class` überschreiben, weil sie später hinzugefügt wurde. Ich empfehle auch, zwischen wiederverwendeten Klassen und neuen Klassen zwei Leerzeichen zu machen, so ist beim durchlesen sofort klar, wie die Regeln gruppiert sind, und was wiederverwendet und was neu ist.

### Atomic Design

> Atomic design is a methodology used to construct web design systems.

Kreiert wurde die Atomic Design Methodology von Brad Frost. Atomic Design gibt, anders als BEM keine Naming Conventions oder Code Empfehlungen grundsätzlich vor, sondern stellt eine Philosophie für das Kreieren von Website Design Systemen vor. Dabei werden die einzelnen Bestandteile einer Website aufgesplittet und neu grupppiert:

+ Atoms
+ Molecules
+ Organisms
+ Templates
+ Pages

In einem Design System zu denken inkludiert auch die Frontend Entwicklung. Am effektivsten arbeiten alle Beteiligten bereits in der Konzeptionsphase zusammen. Atomic Design richtet sich an alle Beteiligten im Web Design Prozess, auch Designer. Im Grunde, kann man das System auch als _style guide driven design_ bezeichnen.

### Weiterführendes

+ About Atomic Design - [patternlab.io](http://patternlab.io/about.html)
+ Atomic Design Book - [atomicdesign.bradfrost](http://atomicdesign.bradfrost.com/table-of-contents/)
+ Pattern Lab - [patternlab.io](http://patternlab.io/)
+ BEM - [getbem.com](http://getbem.com/)
+ BEM 101 - [csstricks.com](https://css-tricks.com/bem-101/)
+ SMACSS - [smacss.com](https://smacss.com/)
+ An Introduction to SMACSS - [vanseodesign.com](http://vanseodesign.com/css/smacss-introduction/)
+ Shoptalkshow with Jonathan Snook - [shoptalkshow.com](http://shoptalkshow.com/episodes/001/)
+ An Introduction to OOCSS - [smashingmagazine.com](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
+ OOCSS Wiki - [github.com](https://github.com/stubbornella/oocss/wiki)

## Pre- & Postprocessing

Pre- und Postprozessoren verändern zu einem bestimmten Zeitpunkt den Code, den man schreibt. Bei Postprozessoren schreibt man in einer alternativen Syntax und der Prozessor kompiliert diesen Code. Beim Postprocessing schreibt man regulären Code und in einem nächsten Schritt, nimmt der Postprozessor Veränderungen vor.

Zu den bekanntesten Preprozessoren gehören SASS, LESS, Stylus, HAML. Zu bekannten Postprozessoren gehören PostCSS & Autoprefixer.

Mit CSS Preprozessoren zu arbeiten hat sich zum industriellen Standard entwickelt. Es spart viel Zeit ein und ermöglicht einige Workflow Schritte, die mit nativem CSS (noch) nicht möglich sind. Zu diesen Features gehören unter Anderem:

+ Variables
+ Selector Nesting
+ Mixins
+ Functions
+ Math

Features unterscheiden sich grundsätzlich anhand der Technologie die darunter liegt. Zudem kommen auch noch viele Plugins & Extensions als Zuatz zum Preprozessor selbst.

Wir konzentrieren uns weiterhin auf SASS, nachdem sich dieser Prozessor über die Jahre als Standard durchgesetzt hat. Das heißt jedoch nicht, dass andere Prozessoren nicht genauso legitim wären. Letztendlich hängt alles vom eigenen Workflow ab.

## SASS

SASS steht für _Syntactically Awesome Stylesheets_ und wurde ursprünglich von Hampton Catlin und Natalie Weizenbaum entwickelt. Die Stylesheet Sprache wurde schließlich von Chris Eppstein mit SassScript erweitert. SASS selbst ist eine Stylesheet Sprache die als CSS interpretiert wird. Darunter liegt SassScript, was die eigentliche Scriptsprache darstellt. Die originale Syntax unterscheidet sich etwas von der neueren, weiterentwickelten Syntax. Die neuere Syntax wird in `*.scss` Files geschrieben.

SASS kann auf verschiedene Compiler zurückgreifen, abhängig vom eigenen Workflow. Neben dem regulären, ruby basierten Compiler, gibt es den ebenfalls ruby basierten Compass Compler und den C/C++ basierten LibSass Compiler. Im Gegensatz zum regulären ruby Compiler, bietet Compass einige zusätzliche Funktionen und eine große Menge an Mixinx und Functions, die vor Allem früher für Vendor Prefixing von CSS3 Features verwendet wurden. Der große Nachteil dahinter ist allerdings die Geschwindigkeit es Compilers. Eine sehr gute Alternative ist heute LibSass. LibSass ist dem ruby basierten Compiler sehr ähnlich und verzichtet auf zusätzliche Features. Der einzige Unterschied ist, dass LibSass auf C/C++ basiert und damit um Welten schneller ist.

### Partials

Partials machen das Organisieren von Code sehr viel einfacher. Anstatt alles in ein File zu schreiben, können wir unseren Code in so vielen Files wie wir wollen organisieren, letztendlich wird aber nur ein File compiled.

Ein Partial zeichnet sich dadurch aus, dass es vom Compiler ignoriert wird und kein eigenes CSS File per Sass Partial generiert wird. In den meisten Fällen befindet sich nur ein `style.scss` File mit sehr vielen @import's im Ordner, das dann compiled wird. Ein Sass-File wird ein Partial, sobald vor dem file Namen ein Underscore steht: `_layout.scss`. In der main style.scss importieren wir dieses Partial dann mit `@import 'layout';`. Dabei können Partials natürlich auch auf mehrere Ordner verteilt liegen. Beim Importen muss die Dateiendung und der Underscore nicht angegeben werden.

### Variables

Variabeln speichern Daten. Dabei verhalten Sie sich genauso, wie man es erwarten würde:

``` sass
$color-primary: #bada55;

p > a {
    color: $color-primary;
}
```

SASS-Variabeln werden beim processing dann durch den gespeicherten Wert ersetzt. Variabeln eignen sich am Idealsten zum Setzen von Settings, wie Schriftarten, Farb-Schemas, etc.

Mehrere Daten selber Art (wie zBsp mehrere Farben in einem Farbschema) können auch in sass-maps gespeichert werden. Um auf Werte innerhalb der Map zuzugreifen, wird eine Funktion, `map-get($map, key);` verwendet.

``` sass
$colors: (
    // key: value,
    primary: #bada55,
    secondary: #fada55,
    dark: #aaa
);

p > a {
    color: map-get($colors, primary);
}
```

Maps eignen sich auch gut, um eine Reihe an Breakpoints, Schriftarten etc. zu speichern. Keys & Values können jede Form von Sass-Type sein und müssen nicht ausschließlich Strings sein.

### Nesting

Nesting gehört zu den mächtigsten Features. Dabei können wir einen neuen Selektor innerhalb eines bestehenden Schreiben:

``` sass
p {
    font-size: 1em;
    strong {
        font-weight: 600;
    }
}

// produziert:

p {
    font-size: 1em;
}
p strong {
    font-weight: 600;
}
```

Sass hängt beim processing die Selektoren nach ihrem Nesting zusammen. Schreibt an also einen Selektor in einen Selektor, so wird der darüberliegende Selektor vorangehangen.

Beim Nesting kommt außerdem das Ampersand, "&amp;" zum Tragen. Es referenziert immer den Eltern Selektor.

``` sass
p {
    font-size: 1em;
    line-height: 1.5;
    & + & {
        margin-top: 0.75em;
    }
    &.cursive {
        font-style: italic;
    }
    &:hover {
        color: #bada55;
    }
    &__element {
        font-size: 0.9em;
        &--modifier {
            font-size: 0.75em;
        }
    }
}

// produziert:

p {
    font-size: 1em;
    line-height: 1.5;
}
p + p {
    margin-top: 0.75em;
}
p.cursive {
    font-style: italic;
}
p:hover {
    color: #bada55;
}
p__element {
    font-size: 0.9em;
}
p__element--modifier {
    font-size: 0.75em;
}
```

Komplizierte Selektoren lassen sich somit komfortabel und leicht veränderbar schreiben und eignen sich fantastich zum Arbeiten mit beispielsweise der BEM Methodologie.

Dabei sollte man das Level an Nesting immer im Auge behalten. Man vergisst oft, dass Jedes neue Nesting Level einen Selektor mit höherer Spezifität erzeugt, es sei denn das `&` wird verwendet, um den Eltern Selektor komplett zu verändern (`&__element { ... }`).

### Mixins

Mixins erlauben es, mehrzeilige Deklarationen zu speichern und auszugeben und akzeptiert sogar Argumente:

``` sass
@mixin set-open-type-feature($feature) {
    -moz-font-feature-settings: $feature;
    -webkit-font-feature-settings: $feature;
    font-feature-settings: $feature;
}

p {
    @include set-open-type-feature("smcp");
}
```

Natürlich akzeptiert ein Mixin auch mehrere Argumente, default values und kann auch auf Variabeln oder sass-maps zugreifen, die außerhalb des Mixins definiert wurden.

### Functions

Wohingegen mixins mehrzeiligen Code ausgeben, geben functions nur einen Wert eines sass-types zurück, können allerdings auf mehr Sass-Logik zurückgreifen. Genauso wie Mixins, akzeptieren auch Functions mehrere Argumente, default values etc.

``` sass
$colors: (
    primary: #bada55,
    secondary: HotPink,
);

// Alternative Funktion, um Farben aus dem Wert einer Sass-Map auszulesen.
@function color($name) {
    @return map-get($colors, $name);
}

header {
    background-color: color(primary); // Im Gegensatz zu background-color: map-get($colors, primary);
}
```

### Control Directives

Control Directives bringen spannende Möglichkeiten, wie Schleifen ins Spiel: @if, if(), @for, @while & @each. Diese lassen sich gut in Mixins & Functions integrieren:

``` sass
@each $color-name, $color-value in $colors {
    .bgcolor--#{$color-name} {
		background-color: #{$color-value};
	}
    .txtcolor--#{$color-name} {
		color: #{$color-value};
	}
    .bordercolor--#{$color-name} {
		border-color: #{$color-value};
	}
}
```

### Weiterführendes

+ Sass - [sass-lang.com](http://sass-lang.com/)
+ Using Sass Maps - [sitepoint.com](http://www.sitepoint.com/using-sass-maps/)
+ The Sass Ampersand - [css-tricks.com](https://css-tricks.com/the-sass-ampersand/)
+ Sass Basics - [sitepoint.com](http://www.sitepoint.com/tag/sass-basics/)
+ pure sass functions - [thesassway.com](http://thesassway.com/advanced/pure-sass-functions)
+ Sass Control Directives - [thesassway.com](http://thesassway.com/intermediate/if-for-each-while)

## SASS File Management mit ITCSS

ITCSS ist eine Methode, mehrere CSS Files zu organisieren und wurde von Harry Roberts erstmals vorgestellt. Arbeitet man in SASS so hat man vermutlich lauter Partials, die ebenfalls nach dieser Methode organisiert werden können. Die Idee dahinter ist, CSS nach ihrer Selektor-Spezifität zu ordnen, sodass Selektoren mit höherer Spezifität später geladen werden. ITCSS schlägt folgende Struktur vor:

+ settings: In diesem File wird alles gespeichert, was als Setting oder Konfiguration angesehen werden kann. Der Perfekte Ort für Sass-Maps & Variabeln.
+ tools: Hier landen alle Mixins & functions.
+ generic: das ist der Ort für resets & lowest-specificity rules (* Selector)
+ base: Element-Selectors
+ objects: Ein Ordner, in dem Objekte, nach dem Verständnis von BEM oder OOCSS, also abstrahierte, abgekapselte CSS Klassen als einzelne Partial gespeichert werden.
+ components: Ein Ordner, der Kontexte von objects als Partials sammelt. ZBsp. eine Slideshow, Header, Footer.
+ trumps: Alles, was eine sehr hohe Spezifität aufweist. Also zBsp. id-Selektoren.

Und so sieht dann beispielsweise das Main Sass file aus:

``` sass
@import 'settings';
@import 'tools';
@import 'generic';
@import 'base';

@import 'objects/menu';
@import 'components/header';

@import 'trumps';
```

Folgt man BEM, SMACSS oder OOCS so sollten sich in den meisten Partials bis Components nur Selektoren mit sehr niedriger Spezifität anhäufen, daher ist die Reihenfolge der @imports relevant, weil bei Regeln die sich gegenüberstehen und die gleiche Spezifität haben, die gewinnt, die näher am Ende des Stylesheets steht.

### Weiterführendes

+ Harry Roberts: Managing CSS Projekts with ITCSS - [youtube.com](https://www.youtube.com/watch?v=1OKZOV-iLj4) / [speakerdeck.com](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)
