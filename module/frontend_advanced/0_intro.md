---
layout: unit
title: Intro
permalink: /module/frontend_advanced/0/
categories: frontend_advanced
excerpt: "Generelle Einführung in die Thematik & technische Vorraussetzungen."
navigation_group: module
theme: carrot_1
---

# Intro

Das Modul "Frontend Advanced" beschäftigt sich mit der Optimierung und Automatisierung von Arbeitschritten und Prozessen bei der Webentwicklung für das Frontend.

Verschiedene Ansätze und Tools verfolgen dabei unterschieliche Ziele: Manche Tools ermöglichen ein schnelles Arbeiten, wohingegen andere den Prozess verlangsamen, aber hingegen dafür sorgen, dass lesbarer, auch über mehrere Jahre und Projekiterationen hinweg lesbarer Code entsteht. Frameworks versuchen die Arbeit am Schreiben von Code zu minimieren, in dem sie generische Lösungen zur Verfügung stlelen, die vm Entwickler nur mehr konfiguriert werden müssen.

Entscheidend ist beim Erarbeiten dieser Themen einen skeptischen und offenen Blick zu behalten, der es einem erlaubt, zu entscheiden was zum eigenen Workflow, oder zum Workflow des Teams passt.

Gemeinsam haben alle Ansätze, dass sie uns als Entwicklern die Arbeit effizienter gestalter sollen und das hängt letztendlich vom Entwickler selbst ab.

## Themenüberblick

### Einheit 1 - workflow & toolchain

+ Localtunnel
+ HTML5-Boilerplate
+ Static Site Generators (Jekyll, Octopress, Middleman)
+ Frontend Frameworks (Foundation, Bootstrap, Web Starter Kit)
+ Dependency Management mit bower
+ modernizr


### Einheit 2 - guten Code schreiben

+ Methodologien (OOCSS, BEM, SMACSS, atomic design)
+ Pre- & Postprocessing (less.js, SASS, Stylus, PostCSS, HAML, Jade)
+ SASS (Nesting, Variables, Mixins, Functions, sass_maps, sourcmaps für devtools)
+ SCSS-Files Management mit ITCSS

### Einheit 3 - Arbeitschritte optimieren

+ Arbeiten mit Icons und Icon Fonts (FontAwesome, thenounproject.com, ionicons)
+ CodeKit, Prepos
+ Autoprefixer, Bless
+ critical CSS
+ Gulp, Grunt
+ Minify, Uglify, Image Optiziation

## Vorraussetzungen

Die meisten etablierten Tools laufen auf der Commandline. Man muss kein Commandline-Warlock sein, um mit diesen Tools umgehen zu können, aber damit sie überhaupt laufen, ist es zumindest notwendig, die technische Grundlage dafür zu schaffen.

### Ruby & Ruby Gems

Ruby ist die Grundlage für Static Site Generators wie Jekyll, Middleman und Octopress. Ruby steht auch als erste Vorraussetzung in dieser Liste, weil die später folgenden Vorraussetzungen mit Homebrew installiert werden können. Homebrew ist ein Package Manager für Mac OSX und basiert auf ruby.

#### Mac OSX

Unter Mac OSX ist ruby 2.0 bereits installiert. OSX Pre Yosemite kommt mit Ruby 1.8.7. Hat man bereits Homebrew installiert, reicht `brew install ruby`, um die neuere Version von ruby zu installieren.

#### Windows

Unter Windows ist es zu empfehlen, den [RubyInstaller](http://rubyinstaller.org/downloads/) zu verwenden.

#### Weiterführendes

+ Installing Ruby - [ruby-lang.org](https://www.ruby-lang.org/en/documentation/installation/)
+ Ruby für Windows - [rubyinstaller.og](http://rubyinstaller.org/)
+ Homebrew - [brew.sh](http://brew.sh/)

### Git

> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

_[git-scm.com](https://git-scm.com/)_

Git hat sich in den letzten Jahren zum Industrie Standard für Version Control nicht nur bei Web Projekten etabliert. Die meisten Tools machen davon gebrauch. Damit man zumindest mit Tools wie Bower arbeiten kann, ist git eine technische Grundlage. Man muss dafür nicht mit Git umgehen können, es muss allerdings auf dem System vorhanden sein.

#### Mac OSX

Installation unter Mac OSX ist grundsätzlich problemlos. Im Terminal `git` eingeben installiert git, wenn es nicht bereits installiert ist, bzw gibt es eine Tabelle an Commands aus, auf die man zugreifen kann. `git --version` gibt die installierte Version aus.

Git kann auch über ein binary installiert werden. Dazu kann man sich die aktuellste Version einfach auf [git-scm.com runterladen](https://git-scm.com/download/mac) und regulär installieren.

Empfehlenswerter ist die Installation mit Homebrew, dafür muss zuerst Homebrew installiert werden. `brew` gibt wieder eine Liste an Commands aus. `brew doctor` scant nach potentiellen Problemen und gibt auch Lösungsvorschläge vor. Im Falle von Git, ist es zu empfehlen, die apple-git version durch die reguläre git-version mit Hilfe von Homebrew zu ersetzen.

#### Windows

Arbeiten mit Commandline Tools ist etwas anders, weil die Bash Shell (noch) nicht vorhanden ist. Git zu installieren, ist aber seit einiger Zeit kein großes Problem mehr. Auf git-for-windows.github.io findet man alle Infos dazu.

#### Weiterführendes

+ Installing Git - [git-scm.com](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
+ Installing Git on Mac OSX using Homebrew - [youtube.com](https://www.youtube.com/watch?v=WUviVWnvBM8)
+ Git vor Windows - [git-for-windows.github.io](https://git-for-windows.github.io/)
+ Installing Git and the Bash Shell on Windows - [youtube.com](https://www.youtube.com/watch?v=albr1o7Z1nw)

### node.js & NPM

> Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.

_[nodejs.org](https://nodejs.org/en/)_

Node.js und dessen Package Manager NPM ist die Grundlage von Tools wie bower, Grunt, Gulp uÄ.

#### Mac OSX

Damit Node unter Mac OSX läuft, muss zuerst Xcode installiert werden. Die darin enthaltenen Tools sind notwendig, um node.js zu compilen. Xcode kann über den App Store kostenfrei heruntergeladen und installiert werden.

Ist xcode fertig, installiert das command `brew install node` node.js. Es ist sehr zu empfehlen, Homebrew zu verwenden da es sich um die bequemste und schnellste Methode handelt. Ist der Installationsprozess zu ende, kann man testen, ob alles funktioniert: `node -v`, gibt die node.js version aus, `npm -v` gibt die NPM Version aus.

##### Weitere wichtige Infos zum Umgang mit NPM

NPM ist ein Package Manager für node.js und installiert npm_modules aus der NPM directory. Beim Installieren von NPM modules hat man immer die Wahl module global oder in das directory zu installieren, in dem man sich gerade befindet. Arbeitet man beispielsweise an einem Projekt und benötigt zBsp. gulp als taskrunner, so wechselt man mit `cd ordner_name` in das working directory und installiert mit `npm install gulp --save-dev` gulp als dependency. Es entsteht daraufhin ein neues file im root des ordners, `package.json` und ein ordner `node_modules`. Im node_modules-Ordner befindet sich das gulp node-module und dessen dependencies, und package.json hält diese devDependencies fest.

Viele Tools kommen also einerseits mit dem Commanline Interface (CLI), das global installiert wird, und dem node-module selbst, das projekt-spezifisch ist. Gibt man das Projekt an einen Teamkollegen weiter, kann dieser mit `npm install` alle devDependencies laden.

#### Windows

Anders als unter Mac OSX ist es hier zu empfehlen, Node.js direkt mit dem [Windows Installer](https://nodejs.org/en/download/) zu installieren. `node -v`,`npm -v` sollten wieder fehlerfrei ihre Versionsnummern ausgeben.

#### Weiterführendes

+ How to install Node.js and NPM on a Mac - [blog.teamtreehouse.com](http://blog.teamtreehouse.com/install-node-js-npm-mac)
+ How to install Node.js and NPM on Windows - [blog.teamtreehouse.com](http://blog.teamtreehouse.com/install-node-js-npm-windows)
+ Using a package.json - [docs.npmjs.org](https://docs.npmjs.com/getting-started/using-a-package.json)
