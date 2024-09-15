# Rueckwand24 Frontend Testaufgabe

## Projektübersicht

Dieses Projekt wurde als Frontend-Testaufgabe für Rueckwand24 im Rahmen des Bewerbungsprozesses für die Position des Frontend-Entwicklers entwickelt. Die Aufgabe bestand darin, eine Webseite zu erstellen, die vom minimalistischen Design von Apple inspiriert ist, und interaktive Funktionen unter Verwendung von **Vue.js**, HTML, CSS und JavaScript zu implementieren.

## Funktionen

Das Projekt umfasst die folgenden Funktionen:

- **Interaktive Bildfläche mit verschiebbaren Kreisen**
  - Benutzer können X- und Y-Koordinaten eingeben, um einen verschiebbaren Kreis über einem Bild zu positionieren.
  - Die Position des Kreises wird dynamisch aktualisiert, während er mit der Maus gezogen wird.
  - Es können mehrere Kreise hinzugefügt werden, die sich nicht gegenseitig überlappen.

- **Materialauswahl**
  - Der Benutzer kann aus fünf verschiedenen Materialien wählen.
  - Eine sanfte Animation zeigt visuell an, welches Material aktuell ausgewählt ist.

- **Senden-Funktion**
  - Nach dem Klicken auf die Schaltfläche „Senden“ werden die aktuellen Koordinaten der Kreise und das ausgewählte Material in der Browserkonsole protokolliert.

## Projektstruktur

Das Projekt ist in **Vue.js** komponentenbasiert aufgebaut und folgt der folgenden Struktur:

- **index.html**: Die Haupt-HTML-Datei, die die Seitenstruktur enthält.
- **main.js**: Die Haupt-JavaScript-Datei, die die Vue-Anwendung initialisiert.
- **App.vue**: Der Haupt-Container der Vue-Anwendung.
- **components**: Beinhaltet die einzelnen Vue-Komponenten:
  - **DraggableCircle.vue**: Komponente für den verschiebbaren Kreis.
  - **ImageSection.vue**: Komponente für den Bildbereich.
  - **InputSection.vue**: Komponente für die Eingabefelder zur Positionierung der Kreise.
  - **MaterialSelection.vue**: Komponente zur Auswahl der Materialien.
- **/assets**: Enthält die Bilddateien (z.B. atari-console.png).
- **/public**: Enthält statische Dateien wie Favicon und Icons.
  - **favicon-16x16.png, favicon-32x32.png, favicon-48x48.png**: Favicon-Dateien in verschiedenen Größen.
  - **android-chrome-192x192.png, apple-touch-icon.png**: Icon-Dateien für unterschiedliche Geräte.
- **README.md**: Diese Datei, die Details und Anweisungen für das Projekt enthält.

## Verwendete Technologien

- **Vue.js**: Zur Komponentisierung und Verwaltung der Anwendungslogik.
- **HTML**: Zur Strukturierung der Seite.
- **CSS**: Für das Styling, einschließlich abgerundeter Ecken, Schaltflächengrößen, Textgrößen und Animationen.
- **JavaScript**: Für die Funktionalität der verschiebbaren Kreise, Materialauswahl und Protokollierung der Daten in die Konsole.

## Feedback

Dieses Projekt war eine großartige Gelegenheit, meine Fähigkeiten in Vue.js, HTML, CSS und JavaScript unter Beweis zu stellen. Ich habe die Arbeit an dieser Aufgabe sehr genossen und fand es eine bereichernde Erfahrung.

Vielen Dank für diese Möglichkeit!