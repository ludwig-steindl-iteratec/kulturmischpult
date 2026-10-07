# Kulturmischpult

Ein kleines Anschauungswerkzeug für den Workshop zur Firmenkultur. Vier Regler – Gemeinschaft, Pioniergeist, Leistung und Ordnung – nach dem Competing Values Framework (Cameron & Quinn) und ein live mitlaufendes Kulturprofil; optional dazu eine dreistufige Mischungsauswertung.

Es ist **kein Messinstrument** (kein OCAI), sondern ein Bild zum Besprechen. Leitsatz: *Es gibt keine gute oder schlechte Kultur, nur eine passende oder unpassende.*

## Online

| Variante | Adresse |
| --- | --- |
| Ohne Auswertung (für alle) | https://ludwig-steindl-iteratec.github.io/kulturmischpult/ |
| Mit Mischungsauswertung | https://ludwig-steindl-iteratec.github.io/kulturmischpult/auswertung.html |

Beide Varianten sind dieselbe Datei `index.html`: Ohne Zusatz zeigt sie nur Pult und Kulturprofil, mit `index.html?auswertung` zusätzlich rechts die Mischungsauswertung. `auswertung.html` leitet nur dorthin weiter. Änderungen am Mischpult also immer nur in `index.html` machen.

Das Repo ist öffentlich – die Variante mit Auswertung ist nicht geheim, nur nicht verlinkt.

## Nutzung

**Online** über die Adressen oben – auch am Handy voll bedienbar.

**Offline:** `index.html` doppelklicken. Die Datei öffnet sich im Browser und funktioniert komplett ohne Server, Installation oder Internetverbindung. Für die Auswertung im Browser `?auswertung` an die Adresse anhängen oder `auswertung.html` öffnen (beide Dateien im selben Ordner).

- Im Kopf des Mischpults zwischen **Ist (heute)** und **Soll (in 2 Jahren)** umschalten. Die Regler steuern immer den gewählten Stand. Der jeweils andere Stand ist als gestrichelte Marke am Regler und als zweite Fläche im Diagramm zu sehen – so wird die Lücke sichtbar. Ist ist immer durchgezogen, Soll immer gestrichelt.
- **Schwerpunkt:** Im Kulturprofil zeigt ein Punkt, wohin die Kultur insgesamt neigt (gefüllt = Ist, hohl = Soll); ein Pfeil zeigt die Richtung von Ist zu Soll. Gleich hohe Regler ergeben die Mitte, nur ein hoher Regler dessen Ecke – das Gesamtniveau spielt keine Rolle.
- **↺** rechts im Pult-Kopf stellt Ist und Soll wieder auf die Mitte (50).
- Regler bedienen: die **Kappe** mit Maus oder Finger anfassen und ziehen (ein Klick auf die Schiene verschiebt nichts), oder per Tastatur (Tab zum Regler, dann Pfeiltasten; mit Shift in 10er-Schritten; Bild auf/ab, Pos1/Ende). **Doppelklick bzw. Doppeltipp auf die Kappe** setzt den Regler auf die Mitte (per Tastatur: Taste 0 oder Entf).
- **Steckbrief:** Klick oder Tipp auf den Namen eines Kanals (ⓘ) öffnet einen kurzen Steckbrief des Typs – Führung, Denkweise, Verhalten. Gut für den Theorieteil.
- **⎙ Drucken** (rechts oben) gibt das Ergebnis kompakt aus: Tabelle mit Ist, Soll und Differenz je Typ und die Raute; in der Variante mit Auswertung zusätzlich die Mischungsauswertung für Ist und Soll nebeneinander. Im Druckdialog lässt sich auch „Als PDF speichern“ wählen. Gedruckt wird immer im Hellmodus.
- Rechts oben zwischen Hell- und Dunkelmodus umschalten. Am Beamer ist der Hellmodus meist besser lesbar.
- Für die Beamer-Präsentation: Browser in den Vollbildmodus schalten (F11 bzw. ⌃⌘F am Mac).

**Datenschutz:** Es werden keine Daten erhoben oder übertragen. Nur der letzte Reglerstand wird lokal im Browser gemerkt, damit er nach dem Neuladen noch da ist (beide Varianten teilen sich diesen Stand). Abschalten: in `CONFIG` `merken: false` setzen.

## Einbetten

Mit `index.html?einbettung` zeigt die Seite nur Pult und Kulturprofil, ohne Kopf, Auswertung und Speichern, und skaliert sich als Ganzes in den Rahmen – gedacht für ein `<iframe>`, z. B. in den Einführungsfolien.

Nachrichten per `postMessage` (Zielursprung `"*"`, damit es auch mit lokal geöffneten Dateien funktioniert):

| Richtung | Nachricht | Wirkung |
| --- | --- | --- |
| Seite → Mischpult | `{ thema: "light" \| "dark" \| null }` | Hell/Dunkel übernehmen |
| Seite → Mischpult | `{ werte: { ist: {…}, soll: {…} }, modus: "ist" \| "soll" }` | Ist, Soll und Modus setzen (ohne Rückmeldung) |
| Mischpult → Seite | `{ kulturmischpult: "bereit" }` | einmal nach dem Start |
| Mischpult → Seite | `{ kulturmischpult: "werte", ist: {…}, soll: {…} }` | nach jeder Änderung durch Bedienung |

Werte sind Objekte `{ clan, adhocracy, market, hierarchy }` mit ganzen Zahlen von 0 bis 100.

## Texte und Werte anpassen

Alle Texte, Schwellenwerte, Farben und Startwerte stehen gesammelt im Block `CONFIG` am Anfang des `<script>`-Teils in `index.html`. Nur die Texte zwischen den Anführungszeichen bzw. die Zahlen ändern, speichern, im Browser neu laden.

| Was | Wo in `CONFIG` |
| --- | --- |
| Bezeichnungen „untersteuert / gut ausgesteuert / übersteuert“ | `zustaende` |
| Typnamen | `typen` → `name` (die englischen Originalbegriffe werden bewusst nicht angezeigt) |
| Farben je Typ (iteratec-Schema) | `typen` → `farbe` |
| Schwellen (0–29 / 30–70 / 71–100 usw.) | `schwellen` |
| Erklärungstexte je Regler | `typen` → `texte` |
| Steckbriefe (Führung, Denkweise, Verhalten) | `typen` → `steckbrief`, Überschriften in `steckbriefTitel` |
| Namen der Kombinationen („Die ehrgeizige Familie“ …) – Auswertung | `paare` |
| Balance-Texte – Auswertung | `balance` |
| Spannungstexte Gemeinschaft ↔ Leistung, Pioniergeist ↔ Ordnung – Auswertung | `spannungen` |
| Wert der Mitte (Doppeltipp, ↺) und Tooltip-Text | `reglerMitte`, `zuruecksetzenText` |
| Reglerstand merken | `merken` |

Platzhalter wie `{A}` oder `{typ}` in den Texten werden automatisch durch den passenden Typnamen ersetzt und sollten stehen bleiben.

## Veröffentlichen

GitHub Pages veröffentlicht den Stand von `main` (Ordner `/`) automatisch. Nach einem Push ist die neue Fassung nach etwa einer Minute online; ggf. die Seite im Browser neu laden.

## Ausblick: Stufe 2

Ein Erhebungstool, bei dem alle Teilnehmenden anonym ihre Ist- und Soll-Werte abgeben und daraus ein gemitteltes Teamprofil entsteht, ist bewusst zurückgestellt (bräuchte einen Server). Die Struktur ist vorbereitet: Die Auswertung steckt in der eigenständigen Funktion `auswerten(werte)`. Sie nimmt ein Objekt `{ clan, adhocracy, market, hierarchy }` mit Werten von 0 bis 100 entgegen und kann genauso mit gemittelten Teamwerten gefüttert werden.
