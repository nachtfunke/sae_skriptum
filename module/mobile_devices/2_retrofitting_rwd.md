---
layout: page
title: Retrofitting RWD Process
permalink: /module/mobile_devices/2/
categories: mobile_devices
excerpt: "Arbeitsweise von Desktop zu Mobile: Mit Devtools umgehen & Performance beachten."
navigation_group: module
theme: grape_3
---

# Der Retrofitting RWD Prozess

Responsive Webdesign ist ein Ansatz im Frontend Development, um Websites für alle möglichen Bildschirme anzupassen, ohne dabei für jedes mögliche Gerät selektiv zu entwickeln.

Responsive Webdesign kommt durch die drei Basics, **Fluid Layout**, **Mediaqueries** und **Breakpoints** zustande. Durch relative Werte kreieren wir anpassungsfähige und Kontextabhängige Layouts und nehmen mit Mediaqueries an bestimmten Breakpoints nötige Veränderungen vor.

Beim Retrofitting RWD Prozess geht es darum, Desktop Websites responsive zu machen. Dabei fängt man in der größten Ausgabe an, und arbeitet sich absteigend von Breakpoint zu Breakpoint vor.

![Breakpoints by http://blog.froont.com/9-basic-principles-of-responsive-web-design/]({{site.url}}/img/rwd_breakpoints.gif)

## Breakpoints finden

Testing ist im Responsive Web Design Prozess essentiell. Das fängt beim identifizieren von Breakpoints an. Glücklicherweise hat es in den letzten Jahren  sehr viele Verbesserungen auf diesem Bereich gegeben. Die meisten Bemühungen kommen auf diesem Gebiet von den Google Chrome DevTools.

### Device Mode

Der _Device Mode_ stellt einen guten Ersatz zum Testen mit realen Geräten dar. Dieser Modus emuliert neben Viewport-size oder Pixel-Ratios auch native Scrollbars, Touch events und modifiziert auch den UA-String (User Agent String).

![Device Mode in den Devtools aktivieren]({{site.url}}/img/chrome_rwd_mode.png)

Die Mediaqueries Bar detected auch min- & max-width based Mediaqueries innerhalb des Stylsheets. An derselben Stelle kann man sowohl die Orientation simulieren, als auch den UA-String manipulieren. Der Device Mode stellt gängige Geräte zur Verfügung, allerdigns hat man auch die Option, manuell Geräte hinzuzufügen.

Vor Allem beim Testen von Performance, ist die Option des Network Throttelings sehr hilfreich. Sie erlaubt es, verschiedene Übertragungsszenarien zu simulieren und so zu testen, wie sich die Website unter schlechteren Netzwerkbedingungen verhält.

***

### aside / SCSS-Code Debuggen

Arbeitet man mit SASS, so arbeitet man höchstwahrscheinlich mit Mixins, Variabeln und verschiedenen Partials. Da ist es oft nicht sehr hilfreich, nur den Kompilierten Code im Inspektor zu sehen. Dafür gibt es _Source Maps_.

Abhängig davon, welchen Compiler / welche Methode für Compiling man verwendet, muss man diesen Prozess anders herangehen. Für Gulp gibt es ein Plugin, das man mit `npm install gulp-sourcemaps --save-dev` in sein Projekt installieren kann. Ist das richtige Setting im Chrome gesetzt, so kann man all seinen SCSS-Code im Inspektor sehen, anstatt nur den kompilierten CSS Code.

Sourcemaps können auch für JavaScript files erstellt werden, wenn diese zBsp. kompiliert werden.

#### Weiterführendes

+ Gulp-Soucemaps - [github.com](https://github.com/floridoo/gulp-sourcemaps)
+ Set up CSS & JS Preprocessors - [developers.google.com](https://developers.google.com/web/tools/setup/setup-preprocessors?hl=en)

***

### Live Editing im Browser

Chrome erlaubt es, Files direkt im Browser dank Workspaces zu editieren. Dazu fügt man im _Sources_ Tab per Rechtsklick seinen Folder hinzu, gibt Chrome die nötigen Berechtigungen und schon kann man im Browser selber entwickeln.

### Remote Debugging

Remote Debugging erlaubt es, Websites direkt am Smartphone oder Tablet zu debuggen. Am großen Bildschirm läuft der Inspektor, am Bildschirm des Geräts die Website.

#### Android 4.0+

1. Zuerst muss das Android Gerät via USB verbunden werden. Für USB Debugging gibt es ein eigenes Setting in den `Developer Options > USB Debugging`.
2. Zusätzlich funktioniert Remote Debugging nicht als Guest oder Incognito User, man muss als Chrome User angemeldet sein.
3. In den DevTools wählt man `more tools > inspect devices`, und wählt dann das angezeigte Device aus.

![Settings für Remote Debugging finden]({{site.url}}/img/chrome_remote_debugging.png)

#### iOS

1. Auch für iOS muss zuerst das Gerät via USB verbunden werden und das jeweilige Flag in den Settings gesetzt werden. Zu finden ist es unter `Settings > Safari > advanced > Web Inspector`.
2. Remote Debugging für iOS funktioniert nur mit Safari.
3. Im Safari wählt man unter `Develop > iPhone` dann die offene Seite auf dem iPhone aus und der Inspektor öffnet sich.

### Gulp: BrowserSnyc

Im Idealfall testet man an realen Geräten. Für diesen Fall eignet sich BrowserSync, wenn man nicht die Möglichkeit hat, eine Dev Umgebung auf einem Server einzurichten. Dafür gibt es ein Node Module, das man mit Gulp nutzen kann. Um es zu installieren, reicht `npm install browser-sync --save-dev`. Das Plugin gibt eine IP-Adresse aus, unter der man die lokale Website ansehen kann, solange man im selben Netzwerk ist.

### Weiterführendes

+ Chrome Dev Tools: Device Mode - [youtube.com](https://www.youtube.com/watch?v=FrAZWiMWRa4)
+ Google Developers: Test Responsive and Device-specific Viewports - [developers.google.com](https://developers.google.com/web/tools/chrome-devtools/iterate/device-mode/emulate-mobile-viewports)
+ Set up Persistence with Dev Tools Workspaces - [developers.google.com](https://developers.google.com/web/tools/setup/setup-workflow)
+ Remote Debugging Android Devices - [developers.google.com](https://developers.google.com/web/tools/chrome-devtools/debug/remote-debugging/remote-debugging)
+ BrowserSnyc + Gulp.js - [browsersync.io](https://www.browsersync.io/docs/gulp/)

## Probleme dieses Ansatzes

Als Entwickler fällt uns schnell auf, wenn wir mit Design arbeiten, das nicht gut skaliert. Aber auch im Entwickeln, merken wir relativ schnell, welche Praktiken problematisch werden können. Arbeiten wir nicht durchgängig mit relativen Werten, oder machen wir Layout-definierende Elemente nicht kontet-abhängig, so kann es passieren, dass wir oft für viele verschiedene Breakpoints regeln machen müssen, die unsere Arbeit zuvor überschreiben.

![ständiges Überschreiben durch Breakpoints]({{site.url}}/additive_breakpoints.png)

Das spüren früher oder später auch die User. Arbeiten wir mit `max-width` based Mediaqueries, dann greifen mehr und mehr Mediaqueries, je kleiner der Bildschirm ist. Das heißt im Endeffekt, das der Browser mehr Arbeit hat und das hat Performance Implikationen.

Ein weiteres Problem in der Desktop-first Denkweise ist, dass die meisten Features die aufgrund ihres Designs oder ihres Konzepts nicht skalieren können, einfach ab einem bestimmten Punkt auf `display: none;` gesetzt werden. Eine andere, weiter Performance beeinflussende Option an dieser Stelle ist es, per JavaScript anderes Markup auszuliefern.

Obwohl die Optionen vorhanden sind, zeigen sie in erster Linie konzeptionelle Fehler auf. Das macht den Retrofitting RWD Ansatz nicht zum wirtschaftlichsten.