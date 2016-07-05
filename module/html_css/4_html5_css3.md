---
layout: page
title: HTML5 & CSS3
permalink: /module/html_css/4/
categories: html_css
excerpt: "Vertiefung in HTML und CSS mit Fokus auf moderne Features."
navigation_group: module
theme: tomato_5
---

# HTML5 & CS3

Seit dem 28. Oktober 2014 ist HTML5 offiziell released und der aktuelle Standard für HTML. CSS3 befindet sich weiterhin in Entwicklung. Da einzelne Bereiche des CSS Specs simultan entwickelt werden, sind Teile von CSS3 bereits flächendeckend implementiert, während andere kaum oder gar nicht implementiert wurden.

HTML5 ist seit einigen Jahren der Standard in der Webentwicklung, daher verzichtet dieses Skriptum, ausführlich auf die Unterschiede zu dieser und ältere Versionen einzugehen und nutzt den Raum stattdessen, um auf wichtige Patterns und Konzepte beider Sprachen in Verbindung einzugehen.

## "Content" in HTML 5

HTML umschließt als Auszeichungssprache verschiedene Arten von Content. HTML umschließt auch weitere HTML Elemente, die somit ebenfalls zum Content werden. Welcher Content für welches Element geeignet ist, folgt nach bestimmten Regeln. HTML5 unterscheidet Content in verschiedene Kategorien, die alle in drei Typen eingeordnet werden: **Main-Content, Form-Content & Specific Content Categories**

### Main-Content

Main Content sammelt die geläufigsten Elemente und Arten von Content unter Regeln die die meisten Elemente teilen.

**Metadata Content:** In diese Kategorie fallen Elemente die das Verhalten oder die Präsentation des Dokumens verändern: `<base>, <command>, <link>, <meta>, <noscript>, <script>, <style> & <title>`

**Flow Content:** In dieser Kategorie befinden sich die meisten Elemente zum Auszeichnen von Text- & embeded Content. Flow Content wird wiederum unterteilt in:

**Sectioning Content:** In diese Kategorie fallen alle Elemente zum Sektionieren / Abtrennen durch Gruppierung von Content: ` <article>, <aside>, <nav> & <section>`. Zu dieser Kategorie gehören nicht `<header>` & `<footer>`, weil diese jeweils Teil einer Sektion sind, aber keine neue Sektion definieren.

**Heading Content:** Zu dieser Kategorie gehören die Headline-Elemente `<h1>` - `<h6>`.

***

### Sectioning Content & die Outline & HTML 5.1

Der Outline-Algorithmus in HTML5 ist Teil der Spezifikation seit 2008 wurde jedoch nie implementiert. Ursprünglich bedeutete er, dass der der hierarchie counter für heading content wieder bei `<h1>` begann, sobald eine neue Section geöffnet wurde.

``` html
<main>
  <h1>Willkommen auf dieser Seite.</h1>
	<p>Lorem Ipsum</p>
	<section class="related-articles">
		<h1>Ähnliche Beiträge</h1>
		<article>
			<h1>Article 1</h1>
		</article>
		<article>
			<h1>Article 2</h1>
		</article>
	</section>
</main>
```

Die Outline hätte dank dem Sectioning Content erkannt, dass die `<h1>` folgendenen Elemente headlines niedrigerer Hierarchie waren. Ohne diesen Algorithmus müssen aus den folgenden `<h1>`'s wieder `<h2>` & `<h3>` werden, egal in welcher Section sie aufgehen.

Mehr zu dem Thema in einem aktuellen Artikel von [html5doctor.com](http://html5doctor.com/computer-says-no-to-html5-document-outline/).
Ein Tool, um zu Testen wie die tatsächliche Outline dann aussieht bietet der [Nu HTML Checker](https://validator.w3.org/nu/).

***

**Phrasing Content:** Hierzu gehört Text und die dazugehörigen Elemente, die diese Art von Content beschreibung.

**Embedded Content:** Embedded Content ist Teil des Phrasing Contents. Es handelt sich hierbei um Content oder Resourcen Imports: ` <audio>, <canvas>, <embed>, <iframe>, <img>, <math>, <object>, <svg>, <video>`.

**Interactive Content:** Hierbei handelt es sich um Elemente, die explizit für Interaktion konzipiert wurden. `<a>, <button>, <details>, <embed>, <iframe>, <keygen>, <label>, <select>, & <textarea>`.

**Palpable Content:** Elemente, die empty aber nicht _hidden_ sind. Beispielsweise das `<ul>` Element.

### Form-Content

Zum Form-Content gehören alle Elemente die Teil eines Formulars sind. Diese können jeweils wieder in **listed**, **lableable**, **submittable** und **resettable**.

### Weiterführendes

+ Content Categories - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)
+ Content Models - [dev.w3.org](https://dev.w3.org/html5/spec-preview/content-models.html)

## Formulare

Formulare sind seit jeher ein integraler und wichtiger, interaktiver Bestandteil von HTML Dokumenten. Sie erlauben das Übermitteln von Daten von Seiten des Users auf den Server. Darauf kann dann der Server entsprechend reagieren. Daraus ist zu schließen, dass eine serverseitige Komponenten immer notwendig für ein funktionierendes Formular ist, aber das ist nicht richtig. Ein Formular kann Daten auch an die Website selbst übermitteln und via JavaScript damit arbeiten.

Bei Formularen kommen Elemente zur Verwendung, die sogenannte **Widgets** erzeugen.

### Das notwenigste Formulargerüst

Das wichtigste Element für ein valides Formular ist das namensgebende `<form>` Element.

``` html
<form action="formularscript.php" method="post">
	<!-- Inhalt meines Formular -->
</form>
```

Neben der Auszeichnung eines Formulars ist dieses Element außerdem ein reguläres Block-Level Element. Obwohl alle Attribute des Elements optional sind, sind das `action` & `method` Attribut für die Funktion des Formulars essentiell.

Das `action` Attribut akzeptiert eine URI und legt den Ort fest, an den das Formular beim Übermitteln die Daten sendet. `method` definiert, welche HTTP-Methode zum Übermitteln verwendet werden soll, `post` oder `get`.

Damit das Formular auch abgeschickt (submitted) wird, brauchen wir ein ein Element dafür, ein Element, das per Click die Submission auslöst und die Daten aus dem Formular an die Location in `action` nach der in `method` definierten HTTP-Methode übermittelt:

``` html
<form action="formularscript.php" method="post">
	<!-- Inhalt meines Formular -->
	<button type="submit">senden</button>
</form>
```

Hier kommt ein neues Element ins Spiel, das `<button>` Element. Es umschließt nicht nur Text, sondern flow-content, es kann also auch HTML umschließen. Das Attribut `type` definiert hier die Art des Buttons, also in diesem Fall `type="submit"`. Dabei wird das DOM-Event "Submit" für das Formular ausgelöst.

Das `<button>` Element ist nicht limiert auf Formulare. Es kann auch außerhalb von Formularen verwendet werden. In seiner semantischen Funktion beschreibt es eine _klickbare Schaltfläche_.

Oft sieht man anstelle des Button-Elements ein anderes Element für Submitting:

``` html
<form action="formularscript.php" method="post">
	<!-- Inhalt meines Formular -->
	<input type="submit" value="senden">
</form>
```

Im Unterschied zum `<button>` Element kann dieses leere Element kein HTML als Label verwenden, sondern der in dem Attribut `value` stehende Text wird stattdessen verwendet.

### Formularelemente

Das wichtigste Element für Formulare ist das `<input>` Element. Über das `type` Attribut wird die Art des Widgets definiert. Mit HTML5 kamen eine Reihe an Input-Elementen hinzu, die unterschiedliche Adaption in den Browsern finden. Die häufigsten Inputs, die es bereits seit früheren Versionen gibt, sind jedoch gut supported: `button, text, checkbox, radio, submit, hidden, file, image, reset`. Neben diesen input-types kennt HTML5 noch unter anderem: `color, date, email, number, range, search, tel, url`.

Mit den Attributen `value` ist es möglich, für Input-Elemente default-values festzulegen. Beim Submitten wird dann dieser Wert übermittelt, insofern er nicht geändert wurde. Oft wird dieses Attribut dazu verwendet, um dem User zu kommunizieren, wie der gewünschte Value des Inputs aussehen soll, dafür ist allerdings das `placeholder`-attribut gedacht, dessen Inhalt nicht submitted wird.

``` html
<form action="formularscript.php" method="post">
	<div>
		<p>Wie lautet Ihr Name?</p>
		<input type="text" placeholder="Ihr Vor- & Nachname">
	</div>
	<input type="submit" value="senden">
</form>
```

Neue Input-Types sind großteils _progressively enhanced_, was bedeutet das sie relativ sicher zu verwenden sind. Erkennt der Browser den Type nicht, so wird daraus ein Text-Type Default.

Einige der Input-types haben keine auswirkungen auf das gerenderte Widget, allerdings erzeugen sie beispielsweise auf Smartphones oder tablets andere keyboards. `type="tel"` ruft so beispielsweise das keyboard für telefonnummern-eingabe auf, anstelle des default-text-keyboards.

#### Radio & Checkbox

Diese beiden Input-types unterscheiden sich etwas:

``` html
<form action="formularscript.php" method="post">
	<div>
		<p>Wie lautet Ihr Name?</p>
		<input type="text" name="vor_nachname" placeholder="Ihr Vor- & Nachname">
	</div>
	<div>
		<p>Wählen Sie eines aus:</p>
		Banane <input type="radio" name="frucht" value="banane" checked><br>
		Erdbeere <input type="radio" name="frucht" value="erdbeere"><<br>
		Apfel <input type="radio" name="frucht" value="apfel">
	</div>
	<div>
		<p>Wählen Sie eines oder mehrere aus:</p>
		Blau <input type="checkbox" name="farbe" value="blau"><br>
		Grün <input type="checkbox" name="farbe" value="gruen"><br>
		Lila <input type="checkbox" name="farbe" value="Lila"><br>
		lemonchiffon <input type="checkbox" name="farbe" value="wtf"><br>
		keine Farbe<input type="checkbox" name="farbe" value="keine" checked>
	</div>
	<input type="submit" value="senden">
</form>
```

Hier fallen einige Unterschiede aber erstmals zum Sinn hinter Checkboxes und Radiobuttons dem User eine Auswahl an verschiedenen Möglichkeit zu geben, und diese entweder auf eine Dieser zu limitieren oder nicht.

Bei Checkboxes kann der User eine oder mehrere dieser Values auswählen, bei Radiobuttons kann er nur einen der Value wählen.

Damit die übermittelten Daten auch ihrem Input-Feld zugewiesen werden können, kommt das `name`-attribut zur Verwendung. Es weißt dem Input quasi eine Bezeichnung zu. Bei radio- & checkboxes wird das name-attribut außerdem verwendet, um diese zu gruppieren. Das ist vor Allem bei radio's wichtig, weil immer nur ein value unter den radio's die mit name gruppiert sind übermittelt wird.

Ein weiteres Attribut ist das boolsche `checked` attribut. Hierbei kann man radios oder checkboxes vorauswählen.

#### Weitere Elemente

Mit dem `<select>` Element kann ein Auswahl an möglichen Inputs in Form eines Dropdown-Widgets erzeugt werden:

``` html
<form action="formularscript.php" method="post">
	<div>
		<p>Wie lautet Ihr Name?</p>
		<input type="text" name="vor_nachname" placeholder="Ihr Vor- & Nachname">
	</div>
	<div>
		<p>Wählen Sie eines aus:</p>
		<select name="frucht">
			<option value="erdbeere">Erdbeere</option>
			<option value="banane" selected>Banane</option>
			<option value="apfel">Apfel</option>
		</select>
	</div>
	<input type="submit" value="senden">
</form>
```

Hier hat das Attribut `selected` dieselbe Funktion wie `checked`, es selektiert den Value vor. `<select>` kann dank dem Attribut `multiple` sowohl checkboxes als auch radio's ersetzen. Da andere Widgets dafür verwendet werden, ist die Entscheidung selbst zu treffen, welches Element besser geeignet ist. Als Empfehlung sollte man große Auswahlen in einem Select-Element unterbringen, wenige in checkboxes oder raioboxes.

Das `<textarea>` Element zieht einen Block auf, in dem langer Text eingegeben werden kann. **Achtung:** Das Textarea-Element ist kein leeres Element:

``` html
<textarea rows="25"></textarea>
```

#### Weitere Attribute

Mit dem boolschen Attribut `disabled` kann ein Formular auf den Status `:disabled` gesetzt und kann nicht mehr interagiert werden.

Das boolsche Attribut `required` zeichnet ein Formular-Element als notwendig aus. Das Formular kann dann nicht angeschickt werden, wenn das Element einen leeren value zurückliefern würde.

`readonly` indiziert, dass der Value des Elements nicht verändert werden kann, sondern nur lesbar ist.

### Formulare strukturieren

Formulare können sehr komplex werden, daher bietet HTML eine Reihe an Möglichkeiten diese übersichtlich zu strukturieren und semantisch zu gruppieren.

Das `<fieldset>` Element gruppiert in Verbindung mit dem `<legend>` Element ganze Abschnitte in einem Formular.

``` html
<form action="formularscript.php" method="post">
	<fieldset>
		<legend>Persönliche Informationen</legend>
		<label for="name">Wie lautet Ihr Name?</label>
		<input type="text" name="vor_nachname" id="name" placeholder="Ihr Vor- & Nachname">
	</fieldset>
	<fieldset>
		<legend>Triviale Informationen</legend>
		<label for="unwichtig">Wählen Sie aus diesen Früchten:</label>
		<select name="frucht" id="unwichtig">
			<option value="erdbeere">Erdbeere</option>
			<option value="banane" selected>Banane</option>
			<option value="apfel">Apfel</option>
		</select>
	</fieldset>
	<input type="submit" value="senden">
</form>
```

Zusätzlich kommt hier noch das `<label>` Element in Verbindung mit dem Optionalen `for` Attribut zur Verwendung. Das `for` Attribut akzeptiert den namen einer ID eines Formular-Elements. Per Klick auf das Label-Element, wird das `:focus` event im Element mit der ID ausgelöst. Man kann denselben Effekt auch ohne das `for` Attribut auslösen, in dem man den entsprechenden input in das `<label>` Element wrapped.

### Styling von Formularen mit CSS

Formulare visuell zu verbessern / zu verändern kann ein haarsträubendes Unterfangen werden. Einige dieser Elemente können völlig normal mit CSS verändert, während andere in manchen Browsern beinahe gar nicht angepasst werden können. Ihr Default Styling ist zusätzlich sehr inkonsistent durch die Browser hindurch. Viele verlassen sich deswegen auf Libraries die es sich zum Ziel gemacht haben, dieses Problem visuell zu lösen, oder rendern mit JavaScript eigene Widgets, deren Styling dann völlig dem Developer obliegt.

Formular-Design ist eine Disziplin für sich, daher gehen wir hier auf einige wichtige Basics in CSS ein:

#### Mit den States :focus, :hover, :active arbeiten

Bei Interaktiven Elementen ist es sehr wichtig, mit den States ihre Interaktivität auch zu kommunizieren. Ein Element das keinerlei visuelles Feedback gibt, egal in welchem Status es sich befindet, kommuniziert dem User nicht, was er wissen muss. Daher ist das Arbeiten mit den States `:hover` & `:focus` sehr wichtig. Hier ist zu empfehlen, mit einfachen Modifizierungen seitens CSS zu kommunizieren. Natürlich kann CSS das Element auch rotieren lassen, wenn es angeklickt wird und eventuell gibt es dafür auch einen Grund, aber _weniger ist immer mehr._

Zusätzlich kann man mit CSS auch auf die States `:checked`, `:valid`, `:invalid`, `:disabled`, `:required` und mehr reagieren.

#### spezifische Pseudoelemente

Wird ein Platzhalter-Text mit dem `placeholder` Attribut gesetzt, so handelt es sich dabei um ein Pseudo-Element, dass mit CSS selektiert und daher auch modifiziert werden kann. Für diese Selektor sind _noch_ vendor prefixes notwendig:

``` css
::-webkit-input-placeholder {
	color: red;
}

:-moz-placeholder { /* Firefox 18- */
	color: red;
}

::-moz-placeholder {  /* Firefox 19+ */
	color: red;
}

:-ms-input-placeholder {
	color: red;
}
```

### Weiterführendes

+ HTML Forms Guide - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms)
+ Sending and Retrieving Data from HTML Forms - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Sending_and_retrieving_form_data)
+ `<button>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
+ `<input>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
+ `<select>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)
+ `<textarea>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)
+ `<fieldset>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
+ `<label>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label)
+ Styling HTML Forms - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Styling_HTML_forms)
+ Advanced Form Styling - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Advanced_styling_for_HTML_forms)
+ Style Web Forms using CSS - [sitepoint.com](https://www.sitepoint.com/style-web-forms-css/)
+ Styling :placeholder - [css-tricks.com](https://css-tricks.com/snippets/css/style-placeholder-text/)

## Audio & Video

Seit HTML5 können wir Audio und Video Files auch ohne Flash auf Websites anzeigen. Zwar entscheiden sich heute viele aus unterschiedlichen Gründen dafür, Audio und Video Content auf externen Plattformen, wie Youtube, Vimeo, Facebook oder Soundcloud zu hosten, dennoch gibt es praktische Anwendungsfälle, in denen man eventuell auf externe Platformen verzichten möchte oder muss.

### Video

Das `<video>` Element wird verwendet, um Videofiles anzuzeigen:

``` html
<video src="videos/vid.webm" controlls preload="auto">
  Ihr Browser unterstützt HTML5-Videos leider nicht :(
</video>
```

Das Video-Element wrapped flow-content, der angezeigt wird, wenn das Video-Element nicht vom Browser unterstützt wird. Das Video Element kann auch eine reihe an `<source>` Elementen, wie beim `<picture>` Element beinhalten. Unterschiedliche Browser unterstützen unterschiedliche Media-Extensions.

Neben den `<source>` Elementen können außerdem eine Reihe an `<track>` Elementen mitgegeben werden, die time-based Data laden können. Beispielsweise Metadaten, Captions, Chapters aber in erster Linie Subtitles.

Eine Reihe an Attributen kann außerdem für das Video-Element verwendet werden. Viele davon sind boolsche Attribute, wie `controlls`, `autoplay`, `loop` oder `muted`. Mit `poster` kann außerdem eine URL zu einem Bild übergeben werden, dass angezeigt wird, bis der erste frame geladen werden konnte.

### Audio

Das `<audio>`-Element ist beinahe identisch in seiner Handhabung mit dem Video-Element. Es unterstützt autoplay, loop, controlls sowie `<track>`'s und verschiedene `<source>`'s. Zusätzlich lässt sich noch `volume` als attribut spezifizieren.

### Weiterführendes

+ `<video>` - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)
+ Using HTML5 Audio & Video - [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video)

## custom attributes

In HTML5 kann man mit Hilfe des `data-*` Attributes, eigene Attribute definieren. Das custom-attribute kann einen beliebigen namen haben, solange ihm `data-` vorhergeht.
