# Baumplaner NRW – Baumarten, individuelle Durchmesser und JPEG-Layout

Diese statische Browser-App basiert auf HTML, CSS, JavaScript und OpenLayers. Sie benötigt keinen Shiny- oder R-Server und kann über GitHub Pages veröffentlicht werden.

## Neue Funktionen

- Baumkreis auf der Karte anklicken, um den einzelnen Baum auszuwählen.
- Jedem Baum eine Baumart zuweisen: Apfel, Birne, Kirsche oder Pflaume. Die Baumarten haben unterschiedliche Farben.
- Optional einen individuellen Durchmesser pro Baum aktivieren. Wenn der Durchmesser geändert wird, versucht die App die Kreise kollisionsfrei auseinanderzuschieben. Der Kreis muss weiterhin vollständig im Maximalbereich liegen und Abstand zu Hindernissen halten. Falls keine gültige Anpassung gefunden wird, wird die letzte gültige Durchmesseränderung zurückgenommen.
- Den sichtbaren Kartenausschnitt als JPEG-Pflanzlayout exportieren. Das Layout enthält einen Kartenrahmen, Nordpfeil, Maßstabsbalken, Legende, Baumarten und eine Kurzstatistik.
- Die bestehenden Funktionen bleiben erhalten: NRW-DOP-WMS, Flurstücks-WMS, manuelles Polygon, optionaler Buffer, Hindernisse, Live-Hexagonalgitter und GeoJSON-Export für QGIS.

Individuelle Baumattribute gehören zur jeweiligen Position (Reihe/Spalte) des Hexagonalgitters. Wenn das Gitter gedreht oder verschoben wird, wandern diese Attribute mit dieser Gitterposition.

## Lokal testen

Nicht per Doppelklick als `file:///...` öffnen. Stattdessen:

1. Lege `index.html` in einen Ordner.
2. Öffne diesen Ordner im Explorer, gib `cmd` in die Adresszeile ein und drücke Enter.
3. Starte einen lokalen Server:

   ```bat
   py -m http.server 8000
   ```

4. Öffne im Browser `http://localhost:8000/`.

Eine Internetverbindung wird benötigt, da Karten und JavaScript-Bibliotheken extern geladen werden.

## Auf GitHub Pages veröffentlichen/aktualisieren

1. Lade `index.html` sowie `.nojekyll` in das Stammverzeichnis deines GitHub-Repositorys hoch.
2. Überschreibe die alte `index.html` und bestätige die Änderung mit `Commit changes`.
3. Öffne `Settings` → `Pages` und stelle bei Bedarf `Deploy from a branch`, Branch `main` und Ordner `/(root)` ein.
4. Öffne die veröffentlichte Website und lade sie mit `Strg+F5` neu, damit kein alter Browsercache benutzt wird.

## Wichtige Hinweise

- Die Baumkreise und Hindernisse werden browserseitig geometrisch geprüft. Die individuelle Durchmesseränderung verwendet eine lokale Kollisionsentspannung; sie ist keine globale Optimierung und kann eine Änderung zurückweisen, wenn sie unter den bestehenden Bedingungen nicht gültig untergebracht werden kann.
- Das JPEG exportiert den sichtbaren Kartenbereich. Der Export kann bei externen Rasterdiensten scheitern, falls der WMS-Server Canvas-Zugriff per CORS nicht erlaubt. In diesem Fall funktionieren die Kartenanzeige und GeoJSON-Exporte möglicherweise trotzdem; ein serverseitiger Kartenexport wäre dann eine Alternative.
- Das GeoJSON wird in WGS 84 exportiert. QGIS kann es bei Bedarf nach EPSG:25832 transformieren.
- Die App ist ein Planungswerkzeug und keine amtliche Vermessung. Dienste und externe Bibliotheken benötigen Internetzugriff.


## Fehlerkorrektur: Bäume werden nicht angezeigt

In dieser Version wird OpenLayers als `OlMap` importiert, sodass die nativen JavaScript-Maps `treeOverrides` und `treeStyleCache` weiterhin `clear()`, `has()`, `get()` und `set()` unterstützen. Wenn du die vorige Version veröffentlicht hast, ersetze die alte `index.html` durch diese Version und lade die Website mit Strg+F5 neu.
