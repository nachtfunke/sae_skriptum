---
layout: unit
title: Responsive Images
permalink: /module/mobile_devices/6/
categories: mobile_devices
excerpt: "Umgang mit Bildern: WebP, srcset & picture."
navigation_group: module
theme: grape_7
order: 7
---

# Responsive Images

Im Responsive Web Design können wir das Skalierverhalten und die Größe von Bildern einfach mit CSS kontrollieren. Vor Allem, wenn wir mit CSS Background-images arbeiten, können wir auf die flexible Property `background-size` zugreifen. Dank Mediaqueries können wir mit CSS auch hochauflösende Hintergrundgrafiken für Retina Bildschirme liefern, aber reguläre `<img>` Elemente vermissten bis vor Kurzem diese Möglichkeit.

Die meisten Lösungen und Workarounds für dieses Problem bestanden aus JavaScript, bei denen entweder das `src` attribut komplett weggelassen und per JS hineingeschrieben wurde, oder es wurde ab einem bestimmten Threshhold ersetzt.

Heutige Browser haben aber in ihrem Renderprozess einen eigenen Preloading Prozess. Bevor JavaScript & CSS greifen, baut der Browser das DOM aus dem HTMl auf. Wenn er in diesem Prozess ein `<img>` entdeckt, so wird das sofort geladen. Alle JavaScript oder CSS Lösungen hätten also zur Folge, dass hochauflösende Bilder zusätzlich geladen würden, was der Performance der Seite schadet, also musste das Problem mit HTML gelöst werden.

## Das srcset Attribut

Mit dem `srcset` Attribut gibt man dem Browser eine Auswahl an weiteren Versionen eines Bildes. Dabei überlässt man die Entscheidung dem Browser, welches Bild geladen wird, und welches nicht:

``` html
<img src="karotte.jpg"
	 alt="Karotte"
	 srcset="karotte_big.jpg 2x, karotte_huge.jpg 3x">
```

Das `srcset` Attribut akzeptiert eine Liste an URL's, die dem Browser zur Verfügung stehen. Mit _descriptors_ beschreiben wir diese Ressource noch zusätzlich, so dass der Browser die richtige Entscheidung treffen kann.

### Descriptors

Mit dem `x` descriptor geben wir die pixel-density an. Das originale `src` wird immer als `1x` behandelt, also beziehen sich alle anderen `x`'s auf das original.

Neben der pixel-density, können wir auch die Breite des Bildes `w` mitgeben. Auch das Hilft dem Browser, zu entscheiden welches Bild in welchem Kontext verwendet wird.

Die Descriptors können nicht in Verbindung verwendet werden. Wird der `w` Descriptor verwendet, so errechnet der Browser daraus einen x-Werte. Zusätlich ist, wenn der `w` Descriptor verwendet wird, das `sizes` Attribut von Nöten, weil in browsers die `srcset` unterstützen und in denen `w` verwendet wird, das `src` attribut ignoriert wird.

### Sizes Attribut

In `sizes` können wir näher definieren, in welchen Größen der Browser das Bild darstellt. Anders als im `srcset`, in dem wir nur Informationen mit den Descriptoren über das Bild mitschicken, haben wir hier mehr Kontrolle über das Verhalten des Browsers:

``` html
<img src="karotte.jpg"
	 alt="Karotte"
	 srcset="karotte_big.jpg 2x, karotte_huge.jpg 1250w"
	 sizes="(min-width: 600px) 960px, min-width(1024px) 1250px, 100vw">
```

`sizes` verwendet mediaqueries und eine Breitenangabe mit `<length>` units. Für die Breitenangabe kann an dieser Stelle auch `calc()` verwendet werden.

## Das <picture> Element

Mit dem `<picture>` Element kann man mehrere Ressourcen gleichzeit zur Verfügung stellen:

``` html
<picture>
	<source media="(min-width: 480px)" srcset="mobile/karotte.jpg 1x, mobile/karotte_big.jpg 2x">
	<source media="(orientation: landscape)" srcset="rechteckig/karotte.jpg 1x, rechteckig/karotte_big.jpg 2x">
	<source srcset="karotte.jpg 1x, karotte_big.jpg 2x">
	<img src="karotte.jpg" alt="karotte">
</picture>
```

Mit `source` werden verschiedenste Quellen angegeben, die mit `<media>` abhängig vom Viewport verwendet werden. Dem Browser stehen dann nur die `<source>` zur Verfügung, deren mediaqueries auch greifen. Damit kann man also `art direction` betreiben, weil man auf einem Smartphone Bildschirm eventuell ein anders geschnittenes Bild verwenden möchte, als auf einem Desktop-Bildschirm.

## Das WebP Grafikformat

> WebP is a modern image format that provides superior lossless and lossy compression for images on the web. Using WebP, webmasters and web developers can create smaller, richer images that make the web faster.

Das WebP ist ein von Google vorgestelltes Bildformat, bei dem Bilder um bis zu 26% leichter sind, als JPEG's und zusätzlich auch Transparenz unterstützt. Damit ist WebP das ideale Bildformat für Bilder innerhalb des Contents.

WebP-Support ist nicht gut und bis jetzt haben auch nicht alle großen Browser ihre Pläne für die Implementierung des Dateiformats vorgestellt.

## Weiterführendes

### Artikel

+ A new image format for the Web - [developers.google.com](https://developers.google.com/speed/webp/#how_webp_works_stylefont-weight_bold)
+ Responsive Images in Practice - [alistapart.com](http://alistapart.com/article/responsive-images-in-practice)
+ Using Responsive Images (Now) - [alistapart.com](http://alistapart.com/article/using-responsive-images-now)
+ Srcset and sizes - [ericportis.com](https://ericportis.com/posts/2014/srcset-sizes/)

### Courses

+ Responsive Images - [udacity.com](https://www.udacity.com/course/responsive-images--ud882)

### Scripts

+ Picturefill Polyfill - [scottjehl.github.io](http://scottjehl.github.io/picturefill/)

### Podcast Episoden

+ **The Big Web Show 112**: Responsive Images get real with Mat Marquis - [zeldman.com](http://www.zeldman.com/2014/02/25/responsive-images-with-mat-marquis/)
+ **The Web Ahead 99**: Implementing Responsive Images with Jason Grigsby - [thewebahead.net](http://thewebahead.net/99)

### Videos

+ The picture element for art direction - [youtube.com](https://www.youtube.com/watch?v=QINlm3vjnaY)
+ Using srscet for responsive images - [youtube.com](https://www.youtube.com/watch?v=Pzc5Dly_jEM)
+ Responsive Images, WebP, and The Picture Element with Bruce Lawson - [youtube.com](https://www.youtube.com/watch?v=45Ao058RMJA)
