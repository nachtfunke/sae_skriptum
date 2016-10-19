---
layout: unit
title: Mobile First
permalink: /module/mobile_devices/3/
categories: mobile_devices
excerpt: "Webdesign für kleine Bildschirme: Mit mobilen Browsern umgehen, mobile API's nutzen & Webentwicklung nach Mobile First"
navigation_group: module
theme: grape_4
order: 4
sub:
    id: "minisprint_b"
    title: "Projekt B: Crystal Gem Therapy"
---

# Mobile First

Der Begriff _mobile first_ wurde von Luke Wroblewski geprägt. Im seinem Buch, das denselben Namen trägt, beschreibt er die Quintessenz dieser Philosophie:

> Designing for mobile first not only prepares you for the explosive growth and new opportunities of the mobile internet, it forces you to focus and and enables you to innovate in ways you previously couldn't.

In Kürze, besagt _mobile first_, dass man im Web Design Prozess die kleinste Größe, in dem Fall das Smartphone, priorisiert. Webdevelopment reiht sich dabei nur in die Reihe der Disziplinen ein, auf die diese Phiolosphie Einfluss hat. Zwar kann mobile first auch nur in der Art und Weise wie wir HTML und CSS schreiben ausgedrückt werden, die größten Effekte zeigen sich aber in der Anwendung von _mobile first_ in allen Bereichen des Web Design.

## Umsetzung im Konzept & Design

Es ist selbstverständlich, dass Web / UI Design in dem kleinen Raum eines Smartphone Bildschirms ein großes Limit darstellt. Und das wird uns beim Design im Retrofitting sehr schnell bewusst, wenn wir realisieren, dass gewisse Konzepte nicht in mobilen Szenarien umsetzbar sind. Die Lösung dafür ist dann oft nur, auszublenden was nicht mehr funktioniert, oder die alternative, aufwändige Route gehen, und alternatives HTML / CSS via JavaScript ausliefern.

Mit diesem _Constraint_, einer Einschränkung im Hintergrund, so sieht man auch einen klaren Zusammenhang zwischen dem Boom von mobilen Browsern und der minimalistischen Design Bewegungen, wie Flat Design oder Material Design. Je Weniger Bestandteile im Design notwendig sind, desto leichter lassen sich diese skalieren. Eine visuell skeomorphistisch gestaltete Oberfläche lässt sich schwer responsive gestalten, weil ihr Layout oft nicht flexibel sein kann, konzeptionell gesehen.

![skeomorphistisch gestaltete Oberfläche]({{site.url}}/img/skeomorphism.jpg)

Für den kreativen Prozess, kann allerdings ein Constraint auch hilfreich sein. Grenzen machen kreativ. Als Designer sind wir es oft gewohnt, mit einer großen _Leinwand_ zu arbeiten, wir haben beinahe alle gestalterischen Freiheiten. Wo früher noch die Technik hinterherhinkte, haben wir heute dank CSS3, Canvas, WebGL, Video & Audio beinahe keinerlei Einschränkungen mehr und das kann hindernd sein.

Sind Design & Konzept auf _mobile first_ eingestimmt, so entstehen Interfaces, die auch auf kleinen Bildschirmen kein Downgrade zum Desktop darstellen. In diesem Prozess werden zwei weitere Schritte immer wichtiger, an denen auch Developer teilnehmen: Prototyping und Wireframing.

### Prototyping

Websites sind heute nicht mehr nur Dokumente und Browser Dokumenten-Viewer. Dank JavaScript ist der Browser als Runtime nicht mehr wegzudenken. Web Apps können heute nicht nur im Browser laufen, sondern können auch als Applikationen für Mac OSX, iOS, Windows oder Android ausgeliefert werden. Im Designprozess greift man daher oft auf Prototyping zurück.

Prototyping-Tools wie Invision, Figma oder Axure erlauben Proof of Concept in einer frühen Entwicklungsphase. Gerade in der aktuellen Zeit vergeht keine Woche, in der nicht ein neues Tool für Prototyping in der Community angeworben wird.

### Wireframing

Wireframes sind skizzenhafte Darstellungen von Website layouts. Responsive Webdesign und mobile first haben einen weiteren Begriff in den Fokus gerückt, _content first_. User besuchen Websites in erster Linie für ihren Content, den sie liefern. Content first erinnert uns daran, und schlägt vor, im Designprozess zuerst den Content zu strukturieren und diese in Wireframes abzubilden, bevor man in die nächste Phase übergeht.

Oft dienen Wireframes oder Protoypes als erste Codebase für das Projekt. Sowohl Wireframing, als auch Prototyping ist ein guter Usecase für das Verwenden von Frontend Frameworks.

## Umsetzung im Development

Im Development verändert sich auf den ersten Blick nicht viel. Wir wechseln `max-width` Mediaqueries durch `min-width` Mediaqueries aus.

``` css
@media screen and (max-width: 480px) {  } /* Wenn der Bildschirm nicht größer als 480px ist... */
@media screen and (min-width: 480px) {  } /* Wenn der Bildschirm nicht kleiner als 480px ist */
```

Im Development bedeutet das, dass zuerst die kleinste Version entsteht. Breakpoints nehmen eine andere Rolle ein, da es selten Fälle gibt, bei denen Layout _bricht_, wenn der Bildschirm vergrößert wird. In diesem Fall könnte man seine Breakpoints auch direkt an gängige Bildschirmauflösungen mappen, weil man selten riskiert, dass im Raum zwischen den Breakpoints layout bricht.

Arbeit man mit BrowserSync, so kann man nur empfehlen, die Website mit dem Smartphone anzusteuern, und das Smartphone als zweiten Bildschirm zu verwenden. Änderungen resultieren dank BrowserSnyc entweder in einer Style-Injection oder einem Refresh, was das Entwickeln sehr angenehm macht.

Im Entwicklungsprozess, bewegt man sich dann vom Smartphone langsam zum Desktop. Wer über ein Tablet verfügt, kann das an dieser Stelle benutzen und das Layout entsprechend anpassen, ansonsten reichen die Developer Tools des Browsers.

Im Retrofitting bedeutet jeder neue Breakpoint, dass etwas angepasst werden muss, weil es nicht mehr richtig sitzt. Dieses Gefühl verschwindet bei mobile first komplett. Jeder neue Breakpoint, bedeutet **mehr Platz** und mehr Freiheit.

Der User profitiert vermutlich am Meisten von diesem Ansatz. Anders als beim Retrofitting RWD, spürt der mobile User die restlichen Mediaqueries nicht, weil diese nur angewandt werden, wenn ein größerer Bildschirm die Seite aufruft. Je größer der Bildschirm, desto mehr Mediaqueries greifen.

## Features von mobilen Browsern nutzen

Mobile Browser laufen auf Betriebssystemen von mobilen Geräten und das bringt deren API's in die Reichweite des Web Design:

+ **Network Information**: Gibt informationen über Übertragungsrate bzw. das Netzwerk des Benutzers aus.
+ **Battery Status**: Gibt Informationen über den verfügbaren Akku des Geräts aus - wir könnten beispielsweise, die Frequenz von automatischen Speicherungen erhöhen, wenn der Akku des Geräts beinahe leer ist.
+ **Vibration**: Gibt Zugriff auf die Vibrationsfunktion des Geräts - zum Beispiel um Feedback bei Warnungen zu verstärken.
+ **Geolocation**: Lässt uns die Position eines Benutzers abfragen.
+ **Camera**: Wir können die eingebauten Kameras nutzen.
+ **Contacts**: Gibt uns einen Weg, auf die Kontaktliste eingeschränkt zuzugreifen.

Mit neuen Features von Smartphones, wird diese Liste eventuell weitergeführt.

### Weitere Meta Attribute

Mobile Browser unterstützen eine Fülle von zusätzlichen Meta-Attributen, über die wir Verhalten und Funktionen unserer Website steuern können. Beispielsweise können wir auf manchen Browsern der Browser-Leiste eine Farbe hinzufügen:

``` html
<meta name="theme-color" content="#bada55">
```

Oder wir können festlegen, dass iOS unsere Website im web-app-mode immer im fullscreen darstellt:

``` html
<meta name="apple-mobile-web-app-capable" content="yes">
```

Zu erwähnen ist hier allerdings, das diese Angaben noch nicht standardisiert sind und daher sehr browser spezifisch sind.

### Bekannte Hürden im mobile Web Development

Glücklicherweise werden mobile Betriebssysteme schnell geupdated und die meisten Browser unter Android durchlaufen auch ihren eigenen Update Zyklus, unabhängig vom Betriebssystem. Durch die starke Lokalisierung von Android, dauern Betriebssystem Updates allerdings oft Jahre. IOS wird jährlich geupdated, und verteilen sich grundsätzlich rapide. Es gibt selten einen Fall, bei dem wir mit alten iOS Versionen kämpfen müssen. Der Nachteil ist allerdings, dass der mobile Safari nur über das Betriebssystem Update geupdated werden kann, was dazu führt, dass oft Minor Patches nicht flächendeckend verfügbar sind, weil das Betriebssystem-Update iOS für eine Zeit lang lahm legt und das nicht jeder Benutzer in Kauf nehmen möchte.

Ein großer Dorn im Auge von Entwicklern ist Opera Mini. Der für mobile Geräte optimierte Browser wurde 2006 weltweit released und war für eine lange Zeit der beste Browser für Android und konnte sich dank Vorinstallationen auf vielen Geräten als Standardbrowser für User durchsetzen. Noch 2013 meldete Opera 300 Millionen aktive Opera Mini Nutzer. Der größte Anteil dieser Zahl setzt sich aus Nutzern aus Afrika, Russland, China und Brasilien zusammen. Opera Mini zeichnete sich durch sehr gute Performance und kurze Ladezeiten aus. Der Grund dafür ist, dass Website Requests über einen Opera Software Proxy laufen, der an dieser Stelle Website komprimiert und diese Version an den User zurücksendet. Das resultiert leider in sehr schlechtem Support von aktuellen Webstandards und HTML5 / CSS3 Features.

#### Unsupported in Opera Mini

+ Transitions
+ Animations
+ HTML Video
+ HTML Audio
+ Webfonts
+ calc()
+ border-radius
+ position: fixed
+ viewport-units
+ png-favicons
+ etc.

## Weiterführendes

+ Mobile First - [abookapart.com](https://abookapart.com/products/mobile-first)
+ Mobile First Responsive Web Design - [bradfrost.com](http://bradfrost.com/blog/web/mobile-first-responsive-web-design/)
+ Making a Case for Mobile First Designs - [sitepoint.com](http://www.sitepoint.com/making-case-mobile-first-designs/)
+ 10 HTML5 API's Worth Looking at - [sitepoint.com](http://www.sitepoint.com/10-html5-apis-worth-looking/)
+ Apple: Supported Meta Tags - [developer.apple.com](https://developer.apple.com/library/iad/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)
+ Configuring an iPhone Web App with Meta Tags - [code.tutsplus.com](http://code.tutsplus.com/tutorials/configuring-an-iphone-web-app-with-meta-tags--mobile-2133)
+ Color Browser Elements - [developers.google.com](https://developers.google.com/web/fundamentals/design-and-ui/browser-customization/theme-color)
+ Android: Add to Homescreen - [developer.google.com](https://developer.chrome.com/multidevice/android/installtohomescreen)
+ Wireframing Tool Balsamiq - [balsamiq.com](https://balsamiq.com/)
+ A Beginners Guide to Wireframing - [webdesign.tutsplus.com](http://webdesign.tutsplus.com/articles/a-beginners-guide-to-wireframing--webdesign-7399)
+ WTF Opera Mini?! - [operamini.tips](http://operamini.tips/#/)
