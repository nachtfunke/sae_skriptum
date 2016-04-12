---
layout: page
title: Einheit 1 - Workflow & Toolchain
permalink: /module/frontend_advanced/1/
categories: frontend_advanced
excerpt: "Arbeiten mit Konfigurationen und Anpassungen: Einsatz von Boilerplates & Frontend Frameworks; Frontend Projekte beginnen."
theme: carrot_2
---

# Workflow & Toolchain

> A toolchain is a set of distinct software development tools that are linked (or chained) together [...]

_[elinux.org](http://elinux.org/Toolchains)_

Tools & Workflow gehören zusammen - unsere Tools bestimmen unseren Workflow. Jemand, der sicher auf der Commandline ist, wird anders Arbeiten, als jemand der sich auf GUI-based tools verlässt. Man kann nicht sagen, dass ein Tool besser als das andere ist, da sie selten komplett ident sind. Sie haben verschiedene Vor- und Nachteile. Letztendlich kommt es auf die einzelnen Personen an, die damit arbeiten. Ab einem gewissen Punkt wird zumindest eine Entscheidung für oder gegen eiN Tool getroffen.

Der relevanteste Faktor bei der Frage ob ein neues Tool in den Workflow integriert werden soll, ist woraus das Team besteht. Arbeitet man alleine, muss man diese Frage mit sich selbst klären. Arbeitet man jedoch im Team, so beeinflussen die Tools die man nutzt die Arbeitsweise der teilnehmenden Personen.

In den meisten Firmen / Agenturen, die Verstärkung für ihr Dev Team suchen, existiert bereits eine etablierte Toolchain und ein sich daraus ergebender Workflow. Was nicht bedeutet, dass es für Einzelpersonen nicht Tools gibt, die sie verwenden können, ohne dass es große Einflüsse auf den Rest des Teams ausüben. In dem Fall jedoch, dass mehrere Personen an der selben Codebase arbeiten, ist klare Kommunikation und das gemeinsame Treffen von Entscheidungen diesbezüglich essentiell.

Neue Libraries, Framworks, Plugins, Tools und Kits schießen täglich aus dem Boden. Es vergeht kein Tag, an dem nicht was Neues am Radar auftaucht. Das macht den etablierten Workflow daher auch immer zu etwas lediglich temporär etabliertem, das sich potentiell schnell ändert, auch in Teams mit etablierten Systemen und Vorgängen. Im besten Falle, behält man immer einen offenen aber skeptischen Geist bei diesem Thema bei. Nicht alles was neu und glänzend ist und scheinbar von allem außer einem selbst benutzt wird, ist tatsächlich für die eigene Situation nötig.

Die Tools über die wir reden haben gemeinsam, unseren Output als Developer zu optimieren. Daher ist die Frage _"Ist das für mich / für uns wirklich hilfreich?"_ immer im Hinterkopf zu behalten.

## Projekte beginnen

Die meisten Frontend Projekte beginnen damit, ein Template zu entwickeln. Selst in Systemen die letzendlich erfordern, dass wir Code aufsplitten, sodass das System sie wieder zusammenführen kann, ist es empfehlenswert, mit einem regulären HTML Dokument zu beginnen und erst im nächsten Schritt, dessen Code in ein Theme zu verwandeln oder in ein CMS einzuspeißen.

### Dependency Management

An dieser Stelle ist es ratsam, einen Plan zu haben, wie das Projekt ungefähr aussieht. Bevor man beginnt, ist es ratsam, eine Liste an Dingen zu haben, die man braucht. Selten besteht heute eine Website nur aus HTML & CSS. Oft läuft JavaScript darin, Webfonts und kleine oder größere Frameworks werden benötigt. Um diese externen Abhängigkeiten zu managen, gibt es heute mehrere Möglichkeiten, hier werfen wir aber einen genaueren Blick auf bower.

#### bower - Package Manager

`npm install -g bower`, Um bower global zu installieren. Sobald bower installiert ist, können mit `bower install [package]` dependencies installiert werden. Ist man sich nicht sicher, wie ein package exakt heißt, kann man mit `bower search [dingsbums]` suchen. Bower legt in Projekt dann einen Ordner `bower_components` an, in diesen bower alles reinspeichert, was installiert wurde.

Es ist empfehlenswert, solche Packages als dependency zu speichern. `bower init` legt dafür ein file `bower.json` an, nach dem gleichen Prinzip wie package.json bei NPM, in dem die devDependencies gespeichert werden. Installiert man dann mit `bower install [package] --save`, so wird eine dependency in bower.json angelegt. Andere Entwickler können dann mit `bower install` alle dependencies installiern.

Eine der großen Nutzen von Bower ist es auch, dass festgehalten werden kann, welche version einer dependency benötigt wird. Im Version Control kann außerdem der Ordner bower_components ignoriert werden, was das repository klein hält.

Man kann mit bower natürlich auch eigene Projekte als packages zur Verfügung stellen. Genauere Infos dafür stehen auf [bower.io](http://bower.io/).

##### Weiterführendes

+ [http://bower.io/](http://bower.io/)
+ creating bower packages - [bower.io](http://bower.io/docs/creating-packages/)
+ BOWER! Streamline Web Workflow with Bower Package Manager - [youtube.com](https://www.youtube.com/watch?v=Vs2wduoN9Ws)

### Feature Detection

Möchte man als Entwickler auf Features zugreifen, deren Browser Support noch nicht sehr weitreichend ist, so greift man auf modernizr zurück. Modernizr ermöglicht es Entwicklern, Informationen darüber zu erhalten, welches Feature vorhanden oder nicht vorhanden ist. Welche man dabei exakt braucht, lässt sich auf der website von modernizr ein [eigener build](https://modernizr.com/download?setclasses) zusammenstellen.

Modernizr schreibt in das <html> Element daraufhin Klassen, die die jeweiligen features representieren, wie zBsp.: `<html class="js no-cssgradients canvas">`. Als Entwickler kann man via JavaScript oder CSS dementsprechend handeln:

{% highlight javascript %}
if (Modernizr.flexbox) {
    doSomething();
} else {
    loadPolyfill();
}
{% endhighlight %}

Oder in CSS:

{% highlight css %}
html.no-cssgradients .layout {
    background-color: #bada55; // Anstelle von linear-gradient
}
{% endhighlight %}

Feature Detection stellt eine logische und effektivere Erweiterung zum bis vor kurzem noch gängigen UA Browser Sniffing dar, bei dem abhängig vom Browser andere Stylsheets oder JavaScript ausgeführt wurde. Modernizr erlaubt es, moderne features früh auch in produkten Umgebungen (bspw. Kundenprojekte) einzusetzen.


#### Weiterführendes

+ [modernizr.com](https://modernizr.com/)

### Boilerplates

Boilerplates sind Code-Sammlungen oder Default-Projekte, mit denen neue Projekte schnell begonnen werden können. Damit sparen sie viel repetitive Arbeit. Jede Website hat einen `<head>` und benötigt ungefähr dieselben Dinge.

Die meisten Entwickler bauen sich über kurz oder lang eine eigene Boilerplate zusammen, mit den Schnipseln an Code die sie eigentlich immer wiederholen. Abhängig von der Person und dem eigenen Workflow, kann das von Person zu Person ganz unterschiedlich sein.

Die meisten Boilerplates kommen mit dem Nötigsten um ein Front End Projekt zu starten, ersetzen aber nicht die Arbeit an der Codebase. Ihr Ziel ist es, den Anfang zu erleichtern.

#### HTML5 Boilerplate

Zum Bekanntesten Vertreter der Boilerplates gehört die HTML5-Boilerplate. Sie verlässt sich auf normalize.css und bringt neben default responsive mediaqueries außerdem hilfreiche kleine Utility Klassen und eine sehr gut dokumentierte .htaccess, die zur Konfiguration vom Apache Webserver verwendet wird.

Die Boilerplate kann einfach extended werden (zBsp. um Social Media Meta Tags) - mehr zu dem Prozess ist in der [Dokumentation](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/extend.md) zu finden.

#### Skeleton Boilerplate

Die Sekelton Boilerplate geht ein wenig weiter, und ist eine Art Mini-Framework. Neben Dingen, die man sich von einer Boilerplate erwartet, bietet es außerdem noch ein 12-Column Grid System, Typografie, Button, List & Formular-Styles an. Die Styles, die die Boilerplate dabei mitbringt sind leicht konfigurierbar und ersparen auch für Developer, die die meiste Zeit mit dem Schreiben von CSS verbringen genug Zeit.

Die Skeleton Boilerplate eignet sich am Besten für Developer, die weder die Zeit haben, sich ein ausgeklügeltes Frontend System auszudenken, noch sich mit der Terminologie und den Systemen von Frontend Frameworks auseinandersetzen wollen.

#### Google Web Starter Kit

Das Google Web Starter Kit kann man gerade noch als Boilerplate bezeichnen. Neben für Performance optimierten Templates und wenigen UI Komponenten sowie einigen Styles, bringt es zusätzlich noch Tools für den Build Prozess dank Gulp mit.

Das Web Starter Kit setzt grundsätzliche Kenntnisse über Performance Optimierung und den Umgang mit Build Tools voraus.

#### Weiterführendes

+ HTML5 Boilerplate - [h5bp.com](https://html5boilerplate.com/)
+ Skeleton Boilerplate - [getskeleton.com](http://getskeleton.com/)
+ Google Web Starter Kit - [developers.google.com](https://developers.google.com/web/tools/starter-kit/)
+ Get up and running with Google's Web Starter Kit - [webdesign.tutsplus.com](http://webdesign.tutsplus.com/tutorials/get-up-and-running-with-google-web-starter-kit--cms-21495)
+ An Introduction to the HTML5 Boilerplate - [youtube.com](https://www.youtube.com/embed/D9SyB6uPY7c?autoplay=1&vq=hd720)
+ How to use an HTML Boilerplate - [creativebloq.com](http://www.creativebloq.com/web-design/how-use-html-boilerplate-11513798)

## Frontend Frameworks

Unter Frontend Frameworks kann man grundsätzlich viel verstehen. In diesem Rahmen schließt es aber Frameworks aus, die HTML in JavaScript rendern und den Browser zu einer Runtime Environment machen (React, Angular, Ember, etc.). Stattdessen ist hier von Frameworks die Rede, die Entscheidungen im Bereich HTML, CSS & JavaScript minimieren. Sie stellen abgekapselte Komponenten zur Verfügung, die nach Bedarf verwendet und konfiguriert werden.

Bei Frontend Frameworks steht Konfiguration im Vorderund. Sie stellen nicht den Anfang einer Codebase dar, sondern sollen diese zum großen Teil ersetzen, sodass nur mehr fehlende, individuelle Anpassungen und Ergänzungen vorgenommen werden müssen. Damit eignen sie sich für Fälle, in denen man kein individuelles Layout benötigt, oder grundsätzlich die User Experience des Front Ends nicht großartig beeinflusst werden muss.

Am meisten Sinn macht ihre Verwendung bei Projekten, dessen meiste Arbeit nicht im Frontend stattfindet. Beispielsweise benötigen Kunden auf ihrer Website eine Möglichkeit einen bestimmten Datensatz zu bearbeiten, das rechtfertigt aber keine CMS Architektur, also wird ein kleiner Admin eingerichtet. Dafür eignet sich die Verwendung von Frontend Frameworks ideal.

Vor Allem für neue Entwickler und Designer stellen Bootstraß & Co eine verlockende Alternative dar und führen auch fragelos zu Ergebnissen. Dank mangelnder Kenntnisse über die Materie dahinter, wissen aber viele die damit arbeiten oft nicht, was sie tun, da ihnen nur die vom Framework zur Verfügung gestellten Möglichkeiten bekannt sind und sie nicht über Konfigurationslevel hinausgehen können.

Neue Webdeveloper denen oft noch ein intuities Verständnis für Webtechnologie fehlt, profitieren langzeitlich mehr davon, nur partiell auf externen Code zurückzugreifen und stattdessen selbst zu experimentieren und zu eignenen Schlüssen zu kommen.

### Bootstrap

Bootstrap ist unter den Frontend Frameworks die Gallionsfigur. Es bietet zahllose Komponenten und extensive Möglichkeiten zur Anpassung. Als Webdeveloper findet man sich bei der Verwendung von Bootstrap hauptsächlich beim Copy & Pasten.

Man kann das gesamte Framework als Grundlage für sein Webprojekt verwenden, allerdings wird dann vermutlich der meiste Code den Bootstrap zur Verfügung gestellt wird, auskommentieret oder überschrieben.

Es gibt jedoch auch die Möglichkeit, nur [einzelne Komponenten](http://getbootstrap.com/customize/) von Bootstrap zu verwenden (zBsp. für Formular-Elemente, Dropdowns oder die Typografie), was vermutlich eine gute Alternative ist.

### ZURB Foundation

Foundation richtet sich eindeutig an Webentwickler, die bereits Erfahrung in der Industrie haben. Zwar liefert es ebenfalls eine große Menge an fertigen Komponenten aus, allerdings bietet es mehr Optionen zum Arbeiten mit diesen an.

Ein großer Vorteil von ZURB Foundation ist, dass dank ARIA-roles Accessibility ready ist. Zusätzlich bietet foundation auch ein CLI (Commandline Interface), Sass-based Animations Library und ein Tool zum entwickeln von Email-Templates an.

### Pure CSS

> A set of small, responsive CSS modules that you can use in every web project.

Pure ist sehr klein und besteht nur aus einem stylsheet, das ebenfalls über ihr CDN inkludiert werden kann. Es ist im Gegensatz zu den meisten anderen Frameworks sehr klein.

### Weiterführendes

+ Bootstrap - [getbootsrap.com](http://getbootstrap.com/)
+ Zurb Foundation - [foundation.zurb.com](http://foundation.zurb.com/)
+ Whats new in Zurb Foundation 6 - [youtube.com](https://www.youtube.com/watch?v=8cbK06rKXrg&nohtml5=False)
+ All About Zurb Foundation - [youtube.com](https://www.youtube.com/watch?v=_vtzoIs82e4)
+ Semantic ui - [semantic-ui.com](http://semantic-ui.com/)
+ Pure CSS - [purecss.io](http://purecss.io/)
+ The 5 most popular frontend frameworks compared - [sitepoint.com](http://www.sitepoint.com/5-most-popular-frontend-frameworks-compared/)
+ Mark Otto: origin of bootstrap, frontend frameworks, etc - [shoptalkshow.com](http://shoptalkshow.com/episodes/153-mark-otto/)

## Static Site Generators

Static Site Generators sind Tools, die es Webdevelopern erlaubt, Websites zu managen ohne sich dabei auf serverseiten Code zu verlassen. Diese Tools generieren reguläre, statische HTML files.

Die Idee dahinter ist es, die Seite mit Hilfe von lokaler Technologie wie Ruby und Node in statische, zusammenhängende HTML-Datein zu kompilieren. Arbeitet man mit serverseitiger Technologie und Datenbanken, baut der Server aus verschiedenen Templates und eventuell Inhalten aus der Datenbank zusammen und schickt diese zum Client. Im Client landet letzendlich HTML. Dieser Schritt wird von Static Site Generators übernommen. So landet am Server das bereits fertig zusammengebaute HTML, das _Zusammenbauen_ findet aber am lokalen Rechner statt.

Das hat die großen Vorteile, dass auch Personen denen entweder das Wissen oder die Lust mit serverseitiger Technologie zu arbeiten fehlen, Websites mit Unterseiten und Artikel-basiertem Content ausliefern können. Einer der Nachteile ist, dass oft ein komfortables CMS zum Verwalten der Inhalte fehlt. Bedenkt man aber die Zielgruppe dieser Tools, ist das nicht unbedingt ein großes Problem.

### Jekyll

Jekyll gehört zu den bekanntesten, der Static Site Generators. Das Ruby basierte Tool ist sehr beliebt und sobald der Setup Prozess durchstanden ist, ist das arbeiten damit für die meisten Entwickler sehr intuitiv. Zudem kommt, dass sich rund um Jekyll weitere Tools und Plugins gebildet haben.

Jekyll muss zuerst auf dem System installiert werden, damit das möglich ist, muss die Programmiersprache Ruby installiert sein. Ist Ruby auf dem System vorhanden reicht eine Zeile, um Jekyll zu installieren.

{% highlight shell %}
gem install jekyll
{% endhighlight %}

Sobald der Installationsprozess abgeschlossen ist, ist Jekyll als Ruby Gem auf dem System verfügbar. Um ein neues Projekt in Jekyll zu starten, wechselt man mit `cd projekt_folder` in das Projekt und initiert ein neues Jekyll Projekt:

{% highlight shell %}
jekyll new .
{% endhighlight %}

Ist das directory nicht leer, braucht man zusätzlich noch das argument `--force`. Damit wird in den Ordner ein Jekyll Projekt installiert. Von dort aus können Templates, layouts, posts und pages editiert und erstellt werden. Mit `jekyll build` generiert jekyll ein System aus Ordnern und HTML-Files in den Ordner `_site`. Dies ist auch der Ordner, der so auf den Webserver geladen werden kann - er enthält alles, um die Website anzuzeigen.

#### Mehr zu Jekyll:

+ Jekyll (offizielle Seite & Dokumentation) - [jekyllrb.com](https://jekyllrb.com/)
+ Build a blog with Jekyll & GitHub Pages - [smashingmagazine.com](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
+ Getting started with Jekyll - [youtube.com](https://www.youtube.com/watch?v=iWowJBRMtpc)

### Weitere Static Site Generators

+ [middleman](https://middlemanapp.com/): Dieses Tool spricht Entwickler tendenziell eher an. Die Template Engine erlaubt zBsp. Schreiben von Ruby-Code. Es ist Jekyll grundsätzlich sehr ähnlich.
+ [wintersmith](http://wintersmith.io/): basiert auf Node.js; Template Engine ist Jade.
+ [hugo](https://gohugo.io/): _"A general purpose website framework"_ - Hugo zeichnet sich dadurch ab, dass es mehr out-of-the-box features hat. Hugo wurde in Go geschrieben, was das System mit abstand zum schnellsten macht, aber auch limitierungen mit sich bringt (zBsp. kein Support für Plugins). Ein weiterer Vorteil von Hugo, ist dass es keine Dependencies hat. Weder node, noch git, noch ruby sind notwendig, um damit zu arbeiten.

### Weiterführendes

+ 6 Static Blog Generators that aren't jekyll - [sitepoint.com](http://www.sitepoint.com/6-static-blog-generators-arent-jekyll/)
+ Why Static Site Generators are the next big thing - [smashingmagazine.com](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)
+ Track Static Site Generators - [staticgen](https://www.staticgen.com/)

## Umgang mit Teamdynamiken

Die meisten Entwickler arbeiten in Teams. Das Thema "Tools" ist da omnipräsent. Glücklicherweise sind die meisten Entwickler auch an die ständige Fluktuation an Tools und Technologie gewöhnt und generell eher offen für neue Zugänge oder Änderungen, solang man sie begründen kann.

Eine generell gute Empfehlung ist es, sich der effektiven Vorteile bewusst zu werden. Das ist gleich ein guter Anlass, um sich die Frage zu stellen, ob man tatsächlich einen Grund dafür hat, das Tool zu integrieren, oder man nur glaubt man bräuchte es, weil jeder Blogpost und Tweet sich damit beschäftigt.

Problematisch wird es, wenn verschiedene Teammitglieder verschiedene Technologien verwenden, die sich gegenseitig ausschließen, oder deren Workflow Einflüsse miteinander konkurrieren. In jedem Fall ist eine klare und direkte Kommunikation bei diesem Thema unausweichlich __bevor__ man damit produktiv zu Arbeiten beginnt.
