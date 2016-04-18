---
layout: page
title: Einheit 3 - Arbeitsschritte optimieren
permalink: /module/frontend_advanced/3/
categories: frontend_advanced
excerpt: "Alles zusammenführen: Automatisierung von Tasks & Optimierungen von Frontend Code."
navigation_group: module
theme: carrot_4
---

# Arbeitsschritte optimieren

Optimierung von kleinen und großen Arbeitsschritten ist ein konstantes Thema im Frontend Development. Beim Herausarbeiten des eigenen Workflows hat man immer die Qual der Wahl. Problematisch wird es tatsächlich, wenn man bei all der Fülle an verschiedenen Tools und neuen Arbeitsschritten den Überblick völlig verliert. Wichtig ist es daher, immer bewusst zu entscheiden, wie und an welcher Stelle optimiert wird und welchen Nutzen man tatsächlich daraus hat.

## Arbeiten mit Icons

Mit Icons zu arbeiten kann ein lästiges Unterfangen sein. Noch bis vor Kurzem waren wir auf png's & gifs angewiesen, die man mühsam sammeln und verwalten musste. Dank der technologischen Weiterenticklung der Browser können wir heute glücklicherweise SVG dafür nutzen. SVG sind Vektorgrafiken für das Web und bringen damit den Vorteil mit, dass sie dynamisch skalierbar sind ohne dabei an Qualität zu verlieren.

### SVG Icons

Entscheidet man sich mit SVG Icons zu arbeiten, so hat das einige Implikationen für den Workflow. SVG's können einerseits normal als `<img />` oder `background-image` referenziert werden, andererseits können sie auch direkt im HTML als inline SVG eingebunden werden.

Am primitivsten geht das einfach über Copy & Paste. Der gesamte SVG Code wird dabei einfach an die gewüschte Stelle eingefügt und kann dann via CSS nach Wünschen angepasst werden.

#### Exportieren von SVG

Arbeitet man mit einer _älteren Version von Illustrator_, so ist anfänglich wichtig, grafiken die man exportieren will, in _ein separates, neues Dokument_ zu kopieren. Es gibt leider in älteren Versionen von Illustrator keine Möglichkeit, ausgewählte Layer oder Gruppen direkt zu exportieren, ohne allen anderen Code im File ebenfalls im File zu haben. Hat man sein Icon in eine, neuen File, muss noch das Artboard angepasst werden. Dazu selektiert man sein Icon und wählt dann `Object > Artboards > Fit to Selected Art`.

Beim Exportieren wählt man `*.svg` als Datei Format aus und klickt dann auf "Export Selection". Es geht dann ein "SVG Options"-Dialog auf, der unter Anderem auch einen Button "Show Code" besitzt. Das ist der Code, der letztendlich dann in das HTML Dokument eingebunden wird, wenn man inline SVG verwendet.

In den aktuellen Versionen von Illustrator, muss man hingegen die Grafik nicht mehr in ein neues Dokument kopieren, stattdessen wählt man die zu exportierende Grafik aus, wählt `File > Export Selection` und das war's.

Es ist natürlich umständlich und nicht sehr nachhaltig, den Code jedesmal von Hand rauszukopieren. Besser ist es, man behält all seine SVG's in einem Ordner, und inkludiert diese von dort aus. Dafür gibt es verschiedene Möglichkeiten, die teilweise vom eigenen Workflow stark abhängen. SVG ist seit ein paar Jahren in aller Munde und das wird sich so schnell nicht ändern. Seither haben sich viele Personen mit ihren jeweils individuellen Lösungen zu dem Problem gemeldet und diese in die Community getragen.

#### Arbeiten mit Currentcolor

Da die einzelnen Elemente aus denen ein SVG besteht Teil des DOMs sind, können diese auch mit CSS selektiert werden. Da ist vor Allem die CSS Variable `currentcolor` sehr nützlich. Currentcolor entspricht immer dem aktuell gesetzten `color`, also Schriftfarben-Wert. Das ist dann sehr interessant, wenn wir zBsp. Text neben einem Icon auf dieselbe Schriftfarbe setzen wollen:

``` sass
.button {
    color: tomato;
    & > svg {
        fill: currentcolor;
    }
}
```

Der tatsächliche Selektor hängt letztendlich aber vom SVG ab und ob / wie diese optimiert sind. Nicht jedes SVG ist gleich aufgebaut und oft muss der Selektor spezifischer sein:

``` sass
svg {
    rect, circle, ellipse, line, polyline, polygon, path {
        fill: currentcolor;
    }
}
```

Auf jeden Fall zu vermeiden: `svg * { ... }`. Der Universalselektor wählt dementsprechend jedes Element innerhalb von svg an und kann vor Allem bei komplexen SVG's Performanceprobleme bei Animationen verursachen.

#### Wo findet man icons?

Grundsätzlich findet man Icons in Fülle an zu vielen verschiedenen Orten, um diese wirklich alle nennen zu können. Viele qualitativ hochwertige Icons finden sich im wöchentlichen [Collective](http://tympanus.net/codrops/collective/) von [Codrops](http://tympanus.net/codrops/), bzw. gibt es dort auch eine [Freebies-Kategorie](http://tympanus.net/codrops/category/freebies/), die man im Auge behalten kann.

Hier und da findet man auch Icons auf [dribbble und Behance](http://dbfreebies.co/icons). Sehr zu empfehlen ist [thenounproject.com](https://thenounproject.com/). Dort kann man einzelne SVG's runterladen und verwenden, solange man den Urheber nach den Regeln von thenounproject.com nennt.

### Icon Fonts

Icon fonts sind eine bequeme und angenehme Alternative zu inline SVG's. Sie funktionieren in der Regel alle sehr gleich, in dem Sie ein Stylesheet und Fonts zur Verfügung stellen. Im HTML fügt man dann ein Element mit der korrespondierenden Klasse hinzu.

``` html
// Beispiel an Hand von Font Awesome
<span class="fa fa-angle-right"></span>
```

Das macht das Arbeiten mit Icons sehr einfach. Vorsicht jedoch vor der Gewohnheit: Wer immer nur zwei Icons benötigt muss dafür nicht eine ganze Icon Font einbinden. Performance-Bewusstsein in der Webentwicklung bedeutet vor Allem auch, dem User nicht anzumuten, noch mehr runterzuladen.

Ein guter Mittelweg ist Fontello, ein Tool mit dem man seine eigene Icon Font zusammenstellen kann. Braucht man also nur 5 Icons aus der Font Awesome, ist das keine schlechte Alternative. Sucht man nach einem spezifischen Icon eignet sich The Noun Project am Besten. Eine nette Alternative dazu ist die Seite [http://svgicons.sparkk.fr/](http://svgicons.sparkk.fr/), die Icons direkt für Copy & Paste anbietet.

### Weiterführendes

+ Using SVG - [css-tricks.com](https://css-tricks.com/using-svg/)
+ SVG Symbol, a good choice for Icons - [css-tricks.com](https://css-tricks.com/svg-symbol-good-choice-icons/)
+ Icon Systems with SVG Sprites - [css-tricks.com](https://css-tricks.com/svg-sprites-use-better-icon-fonts/)
+ How to work with SVG Icons - [fvsch.com](http://fvsch.com/code/svg-icons/how-to/)
+ Icomoon - [icomoon.io](https://icomoon.io)
+ Iconjar - [geticonjar.com](http://geticonjar.com/)
+ Ionicons - [ionicons.com](http://ionicons.com/)
+ The Noun Project - [thenounproject.com](https://thenounproject.com/)
+ Fontello Icon Fonts Generator  -[fontello.com](http://fontello.com/)
+ Inline SVG vs Icon Fonts - [css-tricks.com](https://css-tricks.com/icon-fonts-vs-svg/)

## Arbeitsumgebung für Preprozessoren

Arbeitet man mit Preprozessoren wie SASS oder LESS, so braucht man ein wenig Vertrauen in den Umgang mit der Commandline. Wer das noch nicht hat, kann auf GUI's zurückgreifen. Diese führen in der Regel nur Commandline Tools in einer grafischen Oberfläche zusammen.

### Weiterführendes

+ Prepos - [prepos.io](https://prepros.io/)
+ Codekit - [incident57.com](https://incident57.com/codekit/)

## Taskrunner

Mit Taskrunnern wie Grunt & Gulp lassen sich viele kleine Schritte in einem Commandline Tool zusammenführen. Zwar bezeichnet sich Gulp als _Streaming Build System_, effektiv macht es aber dasselbe wie Grunt: es hilft dabei, mehrere Arbeitschritte zu automatisieren. Da Gulp neuer ist und in seiner Beliebtheit und Adaption Grunt vorraus ist, konzentrieren sich die Beispiele hier auf darauf. Versteht man aber die einzelnen Schritte hinter dem Arbeiten damit, kann man auch ein gruntfile lesen und muss lediglich einen frischen Blick auf die Syntax werfen, um zu verstehen was passiert.

### Weiterführendes zu Gulp & Grunt

+ Gulp - [gulpjs.com](gulpjs.com)
+ Grunt - [gruntjs.com](gruntjs.com)
+ Gulp for Beginners - [css-tricks.com](https://css-tricks.com/gulp-for-beginners/)
+ Getting Started with Gulp - [markgoodyear.com](https://markgoodyear.com/2014/01/getting-started-with-gulp/)
+ How do I update to Gulp 4? - [liquidlight.co.uk](https://www.liquidlight.co.uk/blog/article/how-do-i-update-to-gulp-4/)

### Mit einem neuen Gulp Projekt beginnen

Zuerst wir das CLI (Commandline Interface) global installiert:

``` bash
npm install gulp-cli -g
```

Ist die Installation beendet, legen wir im Projektordner noch fest, dass Gulp als devDependency für NPM gespeichert wird. Damit stellen wir sicher, dass wenn wir oder jemand anders das Projekt an einem anderen Ort aufmachen, ohne große Probleme alle devDependencies installiert werden können. Dabei hilft NPM's package.json, die wir mit diesem Befehl anlegen:

``` bash
npm init
```

Es startet darauf hin einen Q&A Prozess, dessen Antworten sich in der package.json wiederspiegeln. Wer das überspringen möchte, kann das flag `--yes` mit anhängen, was dazu führt, dass nur nach einem Namen gefragt wird.

Ist dieser Prozess beendet, können wir NPM-Module als devDependencies speichern, die erste davon ist gulp:

``` bash
npm install gulp --save-dev
```

Sobald Gulp installiert ist, legen wir noch `gulpfile.js` im Root Verzeichnis an - dann hat Gulp auch schon alles, was es benötigt um funktionieren zu können.

### Entwicklungsumgebung abgrenzen

An der Stelle ist es wichtig, seine Ordnerstruktur im Auge zu behalten. Es kann schwierig sein, Gulp oder Grunt zu einem späten Prozess in ein Projekt zu integrieren, weil diese Tools am idealsten funktionieren (und bis zu einem gewissen Grad auch davon ausgehen), dass es zwei separate Directories gibt: einem in dem gearbeitet wird, eines das nur den am Ende entstandenden Code beeinhaltet. Das kann abhängig von sehr vielen Faktoren aber dennoch bei jedem Projekt etwas aussehen. In diesem Beispiel gehen wir aber davon aus, dass wir im Directory `dev/` entwickeln, und das Directory `dist/` den finalen Endcode beeinhaltet.

Der Grund für diese Trennung ist, dass wir beispielsweise im dev-directory mit unkomprimiertem, zum debugging gut geeigneten Code arbeiten wollen, aber im dist-directory nur komprimierte Files haben. Das schafft eine klare Trennung von produktivem Code und Entwicklungsumgebung.

### Gulp Tasks

Beginnen wir mit dem Grundgerüst des gulpfile.js

``` javascript
var gulp = require('gulp');

gulp.task('task-name', function() {
    // Task-Code
});
```

`task-name` ist hier die Bezeichnung des Tasks. Möchte man diesen speziellen Task aufrufen, so genügt in der Konsole: `gulp task-name`. Gulp kennt auch den task `default` - schreibt man dann in der Konsole nur `gulp`, so wird dieser Task ausgeführt.

#### SASS Compiling

Wir wollen in unserem Default Projekt SASS schreiben. Wir brauchen also einen Task, der unsere SCSS Files in CSS Files kompiliert. Dafür brauchen wir das Plugin "gulp-sass". Gulp Plugins sind NPM Modules und werden über NPM installiert. Wir schreiben daher in die Konsole,

`npm install gulp-sass --save-dev`

um gulp-sass als devDependency zu speichern. Um das Plugin nutzen zu können, müssen wir es in userem gulpfile.js inkludieren.

``` javascript
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('task-name', function() {
    // Task-Code
});
```

Nun steht uns das Plugin zur Verfügung und wir können einen Task schreiben. Zuerst brauchen wir einen Task, der all unsere SCSS-Files findet und diese in CSS Files kompiliert:

``` javascript
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function() {
    return gulp.src('dev/scss/**/*.scss') // greift unsere SCSS Files auf
        .pipe(sass()) // ...übergibt sie gulp-sass
        .pipe(gulp.dest('dev/css')); // ...und speichert den output
});
```

Hier passieren drei Dinge:

+ Files werden ausgelesen: `gulp.src()`
+ Daten werden einem Gulp Plugin gestreamed: `gulp.pipe()`
+ Daten werden in ein neues File gespeichert: `gulp.dest()`

Damit hat man auch schon die Basics verstanden. Die meisten Gulp Plugins die wir im Frontend Benutzen, arbeiten mit diesen Methoden. Im Falle von umserem Sass Task, kann man auch noch Optionen für das Compiling angeben: `.pipe(sass({outputStyle: 'nexted'}))`.

Rufen wir mit `gulp sass` den Task auf, so durchsucht Gulp unsere files und schreibt CSS in den angegebenen Ordner. Wir gehen für dieses Beispiel noch einen Schritt weiter und fügen außerdem einen Watch-Task hinzu, bei dem wir nicht immer neu die Commandline aufrufen müssen:

``` javascript
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function() {
    return gulp.src('dev/scss/**/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('dev/css'));
});

gulp.task('sass:watch', function() {
    gulp.watch('dev/scss/**/*.scss', [sass]); // beobachte den Pfad und führe bei Änderungen den task [sass] aus
});
```

Rufen wir diesen Task auf, so können wir die Commandline getrost in Ruhe lassen und bequem in den SCSS Files arbeiten, während jedes Speichern unsere Files neu kompiliert. In einem letzten Schritt für dieses Beispiel, verbinden wir beide Tasks noch so, dass sie aufeinanderfolgen. Wir wollen, dass zuerst unser SCSS kompiliert wird und anschließend soll jede neue Änderung ebenfalls kompiled werden:

``` javascript
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function() {
    return gulp.src('dev/scss/**/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('dev/css'));
});

gulp.task('sass:watch', function() {
    gulp.watch('dev/scss/**/*.scss', [sass]);
});

gulp.task('default', [sass, sass:watch]);  // Führe zuerst [sass], dann [sass:watch] aus.
```

Geben wir jetzt in der Konsole `gulp` ein, so wird unser bestehendes SCSS kompiliert und anschließend bleibt alls auf Abruf und wartet auf Änderungen, die dann wieder neu kompiliert werden, sobald wir speichern.

### Weitere Tasks hinzufügen

In einem weiterführenden Schritt wollen wir alle Tools, die wir nutzen wollen zusammenführen. Kennt man die Basics von Gulp, ist das nur mehr eine Formalität. Essentielle Gulp Plugins für Frontend Entwickler sind zum Beispiel:

+ Autoprefixer - [npm/gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)
+ Browsersync + Gulp [browsersync.io](https://www.browsersync.io/docs/gulp/)
+ Clean CSS - [npm/culp-clean-css](https://www.npmjs.com/package/gulp-clean-css)
+ Jade - [npm/gulp-jade](https://www.npmjs.com/package/gulp-jade)
+ Page Speed Insights - [github.com](https://github.com/addyosmani/psi-gulp-sample)

## Finale Optimierungen

Im letzten Schritt von Arbeitsschritt Optimierungen, versuchen wir den Output selbst zu verbessern. Für Frontend Entwickler bedeutet das letztendlich immer: Ladezeiten verkürzen und Performance optimieren.

### Perfomance Optimierung

Viele unterschiedliche Faktoren hängen von der Performance einer Website ab. Wieder handelt es sich dabei um ein Thema, dessen Herangehensweise wiederum erneut von vielen verschiedenen Faktoren abhängt - aber Einiges können wir unabhängig von diesen Faktoren machen.

Tatsächlich handelt sich bei dem Thema aber um ein sehr komplexes. Ein Mindestmaß an Optimierung wird im besten Fall zur Gewohnheit, allerdings ist es nicht nötig, für kleine statische Websites oder Cover Pages sogar Performance Optimierungen bei CSS Slektoren zu betreiben. Allerdings fangen viele Projekte sehr klein an und entwickeln sich oft ohne dass es zu erwarten war in etwas sehr Großes und dort kann selbst die kleinste Optimierung in Summe sehr viel ausmachen.

#### Performance Probleme finden

Bevor man ein Problem beben kann, muss man es erstmal finden. Sehr gute Tools dafür, sind [Pingdom](http://tools.pingdom.com/fpt/) und Google's [Page Speed Insights](https://developers.google.com/speed/pagespeed/insights/). Wohingegen Pingom's Tool sehr übersichtlich Einblick in die rohen Daten dahinter gibt, gibt Page Speed Insights direkte Tips zum Beheben von Problemen.

Dabei sollte man erwähnen, dass das Tool sehr intolerant ist. Page Speed Insights ist ein fantastisches Tool, um herauszufinden, wo noch Potential liegt. Der Wert einer Website wird aber nicht völlig auf Grund schlechter Performance in Frage gestellt (wobei das natürlich ebenfalls abhängig von Website, Kontext und Usergruppe ist). Jedenfalls sollte der Wert kein Indikator für schlechtes Development im aktuellen Zeitalter sein. Die Community rund um Performance Optimierung lässt das aber oft so worken.

#### Anwendbare Tipps

Vieles können wir aber dennoch allein in unserem Feld machen, daher hier ein paar handfeste Tips.

##### Es muss nicht immer jQuery sein

jQuery ist für viele, vor Allem Anfänger im JavaScript Bereich eine fantastische Möglichkeit, Interaktivität in die eigene Website zu bringen. jQuery 2.2.3 kommt bereits auf 86KB, was alleine nicht viel ist, aber in Summe das Performance Budget übersteigen kann.

Wo es geht, sollte auf Vanilla JavaScript umgestiegen werden. Hierzu gibt es einige Ressourcen, die da weiterhelfen können, wie zum Beispiel __[youmightnotneedjquery.com](http://youmightnotneedjquery.com/)__. Diese Seite gibt Vanilla-Beispiele für einige sehr häufige Usecases von jQuery (Klassen hinzufügen, Fades, AJAX, ...).

Weiters kann man auch seinen speziellen Usecase isolieren und eventuell nur dafür eine entsprechende Library verwenden:

+ Mit [sprint](https://github.com/bendc/sprint) kann man jQuery-like Code für DOM-Manipulation schreiben, wobei die Library auf nur 5KB gzipped kommt.
+ [qwery](https://github.com/ded/qwery) ist eine Selector Engine, 2,7KB.
+ Die Event Emitter Library [microevent.js](https://github.com/jeromeetienne/microevent.js) kommt mit nur 20 Zeilen JavaScript aus, 1,66KB.
+ Für AJAX eignet sich [Reqwest](https://github.com/ded/Reqwest), mit nur 9,55KB.
+ Für viele reguläre Animationen reicht heutzutage auch CSS, Abhilfe schafft [animate.css](http://daneden.github.io/animate.css/), 51,6KB.
+ [move.js](https://github.com/visionmedia/move.js) für simple CSS3 Backend Animationen, 13,8KB.

##### Render Blocking Ressources

Page Speed Insights spricht schnell mal von _Render Blocking Ressources_. Der Name spricht für sich - Es handelt sich um Ressources, die das Rendern der Website verhindern. Damit ist in erster Linie alles gemeint, was im `<head>` der HTML Seite landet. Das heißt, alles was wir in den `<head>` unseres HTML Dokuments schreiben, muss zuerst geladen werden, bevor die Seite gerendert wird.

Das kann dann sehr problematisch werden, wenn wir Files aus CDN's benötigen, wie zum Beispiel Webfonts. Webfonts sind kein integraler Bestandteil der Funktion einer Website, auch wenn diese Kern des Brandings sind. Im Idealfall können wir Webfonts selbst hosten, viele werden aber auf eine Lösung wie Typekit oder Google Webfonts zurückgreifen. Ein Schneller Fix ist es daher, den gesamten `<link />` Zur Webfont aus dem Head vor das schließende `</body>` zu geben. Das ist keine Lösung, die valide ist, aber sie stellt eine Lösung für dieses Problem dar, nachdem Browser das CSS dennoch darstellen. Speziell im Falle von Webfonts gibt es allerdings auch eine [Font Loading API](https://drafts.csswg.org/css-font-loading/), die sich momentan im Entwurf befindet. Bis wir auf dieses Interface zugreifen können, bietet Google in Zusammenarbeit mit Adobe's Typekit den [Web Font Loader](https://github.com/typekit/webfontloader).

Wenn es um JavaScript Files geht, gibt es zwei Ansätze. Vor HTML5 gab man `<script>`'s vor das schließende Body Tag, weil das sicher gestellt hat, dass das DOM verfügbar war, bevor die Ressource geladen wurde. Das hatte jedoch den Nachteil, dass das Laden der Scripts nicht anfangen konnte, bis der Render Parser an der Stelle angelangt ist. HTML5 bietet dafür eine sehr einfache Lösung an. Gibt man dem `<script async>`, so kann das Script asynchron geladen werden, während die Seite gerendert wird. An manchen Stellen ist jedoch `<script defer>` die richtige Wahl, bei der die Scripts in ihrer Reihenfolge ausgeführt werden, wohingegen mit `async` geladene Scripts ausgeführt werden sobald sie fertig geladen wurden.

##### Critical CSS

Als Critical CSS bezeichnet man jenes CSS, das unbedingt nötig ist, um die Darstellung der Seite, _above the fold_ sicher zustellen. Tools wie [critical](https://github.com/addyosmani/critical) oder [criticalCSS](https://github.com/filamentgroup/criticalCSS) bieten Plugins für Taskrunner wie Gulp an, um diesen Prozess zu automatisieren. Dabei wird PhantomJS verwendet, um die Website in einer kleineren Größe aufzurufen und das dafür gebrauchte CSS wird in eine eigenes CSS File geschrieben.

Abhängig vom Ansatz, wird dieses File als render blocking ressource in den html head geschrieben, wohingegen der rest des CSS via JavaScript nachgeladen wird. Dieser Ansatz funktioniert gut, benötigt allerdings im Build-Task von Taskrunnern ein wenig Konfiguration - ein Schritt der sich definitiv lohnt.

#### Weiterführendes

+ Discover the Chrome Developer Tools - [codeschool.com](http://discover-devtools.codeschool.com/)
+ Web Fundamentals: Performance - [developers.google.com](https://developers.google.com/web/fundamentals/performance/?hl=en)
+ Why Performance Matters - [smashingmagazine.com](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
+ Getting Ready for HTTP/2 - [smashingmagazine.com](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
+ Writing Efficient CSS Slectors - [csswizardry.com](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)
+ A curated List of Web Performance Optimization - [github.com](https://github.com/davidsonfellipe/awesome-wpo)
+ Authoring Critical CSS - [css-tricks.com](https://css-tricks.com/authoring-critical-fold-css/)
+ Understanding Critical CSS - [smashingmagazine.com](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)
