---
layout: page
title: Progressive Enhancement
permalink: /module/mobile_devices/4/
categories: mobile_devices
excerpt: "RWD Workflow: Progressive Enhancement & Advanced Mediaqueries."
navigation_group: module
theme: grape_5
---

# Progressive Enhancement

Mit Progressive Enhancement (PE), definiert das w3c:

> Starting with a baseline of usable functionality, then increasing the richness of the user experience step by step by testing for support for enhancements before applying them.

Damit stellt es einen Kontrapunkt zu _Graceful Degredation_ dar, bei dem die beste UX per Default zur Verfügung gestellt wird, und alternative, abgespeckte Versionen für ältere Technologie ausgeliefert werden. Geprägt wurde der Begriff "Progressive Enhancement" 2003 von Steve Champeon und Nick Finck und erlangte in den letzten Jahren zusätzliche Aufmerksamkeit, dank RWD.

Die Prinzipien von RWD sind einfach zu verstehen: Mit einem einfachen Kern beginnen, und schrittweise nicht-essentielle Verbesserungen, Upgrades quasi, Anwenden. Das stellt sicher, dass in Fällen, in denen die Grundlage für diese Verbesserungen nicht vorhanden ist (alter Browser, Screenreader, etc.), der Kern immernoch konsumierbar ist.

## PE anwenden

In realer Anwendung, äußert sich pE wie die meisten dieser Prinzipien nicht nur im Development, sondern vor Allem im Zusammenspiel aller Beteiligten des Entstehungsprozesses. Das heißt beispielsweise konkret, Basis-Funktionen einer Websites von modernen Verbesserungen abhängig zu machen. Dabei geht es nicht nur darum, alte Browser zu unterstützen, sondern auch Fälle zu bedenken, in denen Fundamentale Features nicht zur Verfügung stehen.

Ein praktischer Ansatz für die Anwendung dieser Prinzipien ist _Feature Detection_ mit Modernizr. Modernizr schreibt abhängig vom konfigurierten Build Klassen in das `<html>` Element, die wir sowohl in JavaScript als auch CSS nutzen können:

``` css
html.flexbox .wrapper--flex {
    display: flex;
}
html.no-flexbox .block__element {
    float: left;
    width: calc(100% / 3);
}
```

### Konzeptioneller Aspekt

Konzeptionell bedeutet es, elementare Funktionen nicht von Technologie abhängig zu machen, die zu Verbesserung verwendet wird, wie zBsp. Animationen. In den letzten Jahren ist es modern worden, Applikationen mit JavaScript komplett clientside zu rendern. Bei vielen dieser Frameworks wird das DOM durch ein _virtuelles DOM_ ersetzt, dessen Content ohne JavaScript völlig inaccessible ist. Mittlerweile gibt es dazu Workarounds.

Browser als RTE's werden nicht verschwinden, aber es gibt für jede Technologie ein passendes Einsatzgebiet, und das schlichte liefern von Content ist keine adequate Rechtfertigung für eine pure JavaScript WebApplikation. Progressive Enhancement erinnert daran, dass wir nie davon ausgehen können, dass uns immer jede Technologie zur Verfügung steht und dass wir keine Kontrolle über das Konsumverhalten von Benutzern ausüben können, ohne damit Usergruppen auszuschließen.

## Advanced Mediaqueries

Neben den regulären Mediaqueries `max-width`, `min-width` und `orientation` stehen uns als Developer noch weitere Möglichkeiten zur Verfügung:

``` css
@media screen and (device-aspect-radio: 16:9) { }
@media screen and (resolution: 300dpi) { }
@media screen and (-webkit-min-device-pixel-ratio: 2) { }
```

Die Liste geht noch etwas weiter - wir konzentrieren uns hier auf Mediaqueries die vermutlich überall Anwendungen finden werden könnten.

### device-aspect-ratio

Prüft das Pixel-Seitenverhältnis des Bildschirms des Ausgabegeräts (Eventuell relevant für das Arbeiten mit viewport units). Min & Max möglich.

### resolution & -webkit-min-device-pixel-ratio

Prüft die Auflösung des Geräts (Eventuell relevant um Retina Bildschirme zu selektieren). Min & Max Möglich.

``` css
@media screen and (min-resolution: 120dpi), screen and (-webkit-min-device-pixel-ratio: 1.3) { }
```

### Operatoren

Mediaqueries können mehrere Bedingungen gleichzeit setzen:

``` css
@media screen and (min-width: 480px) and (max-width: 960px) { /* Wird nur zwischen 480px und 960px angewandt */ }
```

Zusätzlich kann man mit Mediaqueries auch ein **oder** abbilden, dazu verwendet man ein Komma:

``` css
@media screen and (device-aspect-ratio: 16:9), screen and (orientation: landscape) { }
```

Bei einem Komma wird jedes Query separat behandelt.

## Weiterführendes

### Artikel

+ Understanding Progressive Enhancement - [alistapart.com](http://alistapart.com/article/understandingprogressiveenhancement)
+ Graceful Degredation vs Progressive Enhancement - [w3.org](https://www.w3.org/wiki/Graceful_degradation_versus_progressive_enhancement)
+ Progressive Enhancement: The Past, Present & Future - [blog.teamtreehouse.com](http://blog.teamtreehouse.com/progressive-enhancement-past-present-future)
+ Using Mediaqueries - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
+ Retina Display Mediaquery - [css-tricks.com](https://css-tricks.com/snippets/css/retina-display-media-query/)

### Podcast Episoden

+ **The Web Ahead**: Progressive Enhancement with Arron Gustafson - [thewebahead.net](http://thewebahead.net/105)
+ **The Web Ahead**: Responsing Responsibly with Scott Jehl - [thewebahead.net](http://thewebahead.net/89)
+ **Developer Tea Podcast**: Responsible Responsive Webdesign with Scott Jehl - [youtube.com](https://www.youtube.com/watch?v=UTy6VT7mA5U)

### Websites

+ **HTML5 Please** gibt Informationen über die Verfügbarkeit von HTML5 Features und empfiehlt, wenn nötig, passende Polyfills - [html5please.com](http://html5please.com/)
