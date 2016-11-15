---
title: Intro
layout: unit
permalink: "/module/html_css/0/"
categories: html_css
excerpt: Initiales Setup und Basics für das Erstellen von HTML Dokumenten & Stylesheets
  - Wie man HTML & CSS lernt.
navigation_group: module
theme: tomato_1
---
Willkommen im Modul **HTML & CSS**! Das Skriptum unterscheidet sich grundsätzlich von den anderen Modulen insofern, als das der Inhalt hier nicht 1:1 der Reihenfolge in den Unterrichtseinheiten entspricht, sondern als Theoriereferenz gilt.

## HTML & CSS lernen

Wer in Webentwicklung & -design einsteigt, kommt nicht um HTML und CSS herum, allerdings kann es für Anfänger und auch erfahrene Programmierer oft schwer sein, die Konzepte auf die die Web-Plattform aufbaut zu verstehen.

### Das Blackbox-Problem

Während ihr am Anfang steht, kann es oft passieren, dass Webseiten oft wie eine Blackbox erscheinen, die irgendwelche magischen Dinge tut und am Ende was ausspuckt, was halbwegs so aussieht, wie wir es haben wollen. Aber das Web ist sehr strukturiert aufgebaut.

Das Vermitteln von Wissen kann bei diesem Problem nicht helfen, das einzige, was dieses Problem beseitigt, ist in die Box reinzusehen und darin herumzuwühlen, Dinge kaputt zu machen, zu verändern und neues zu _kreieren_.

> What separates design from art is that design is meant to be... functional. _[Cameron Moll](https://twitter.com/cameronmoll)_

Wer Webtechnologie lernen will - und das gilt nicht ausschließlich, aber vor Allem für HTML & CSS - muss es einsetzen. Diese Technologie will nicht nur erlernt werden, sie will **angewandt** werden.

### Übungen, Hausaufgaben und Mini-Sprints

Der Unterricht und das Modul HTML und CSS sind so gestaltet, dass es viel Raum für kreatives Ausprobieren lässt. Während Hausübungen als Möglichkeit für das Ausprobieren zuhause darstellen, sind Übungen dazu da, eine spezielle Portion Wissen und Können zu festigen. Mini-Sprints hingegen, stellen Projekte da, deren Dauer sich über mehrere Einheiten spannt und sowohl zuhause, als auch im Unterricht erledigt werden sollen.

* * *

## Editor-Setup für Atom

Natürlich können auch andere Editoren genutzt werden, an dieser Stelle gehe ich aber näher auf Atom ein, nachdem Atom [kostenfrei verfügbar](https://atom.io/) ist und dank open source über eine große Menge an Plugins (Packages) verfügt.

### Hilfreiche Settings

Diese Settings sind als Empfehlung zu sehen, nicht als must-have.

Unter `atom > preferences > editor` können die Editor Settings festgelegt werden.

#### Tabs & Indenting

Zur Einrücken wird die Tabulator-Taste verwendet. Hier unterscheiden Editoren zwischen **Soft-Tabs** und **Hard-Tabs**. Diese legen fest, welches _Zeichen_ verwendet wird, um diese Einrückung zu erzeugen. Die Einstellung ist unter `Tab-Type` zu finden.

Soft-Tabs verwendet Leerzeichen, Hard-Tabs verwendet das Tabulator-zeichen. Als zusätzliches Setting gibt es noch `auto`, bei dem Atom versucht jenen type zu verwenden, der bereits im file verwendet wurde.

Die `Tab-Size` legt die Größe der Einrückung fest, also viele viele Zeichen (leerzeichen bei soft, tabulatoren bei hard) beim Einrücken verwendet werden.

Zu Empfehlen sind **Soft-Tabs** mit einer Größe von **2 oder 4**. Als weiteres Setting ist `Show Indent Guide` zu empfehlen. Dabei erzeugt der Editor eine Linie, die die Einrückung visualisiert und eine große Hilfe beim sauberen schreiben von Code darstellt, vor Allem bei HTML.

#### Line-Wrapping

#### Sonstige Settings

Sehr zu empfehlen ist das Setting `Scroll Past End`. Das erlaubt es, über das untere Ende des Dokuments hinaus zu scrollen. So kann man den Arbeitsbereich immer in der Mitte des Bildschirms behalten.

In den `Core Settings` kann man das Setting `Use Custom Title Bar` setzen. Under MacOS verschwindet dann das System-Fenster und geht nahtlos in den Editor über.

## Packages

### autoclose-html

### linter

### pigments

### terminal-plus

### color-picker

### Weitere Packages

Wem diese Packages noch nicht genügen, der kann noch weiteren Empfehlungen folgen:

<iframe width="100%" height="auto" src="https://www.youtube.com/embed/DmKNDxlNLoE" frameborder="0" allowfullscreen=""></iframe>

## Entwicklungsumgebung mit Vagrant