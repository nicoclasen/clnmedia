# DESIGN.md

Stand: 2026-10-21
Vorherige Fassung (dunkel, Referenz pryzm.design) ist mit diesem Redesign
hinfällig und vollständig ersetzt.

Referenz für den Formenteil: https://www.northcdatacenters.com/de/
Übernommen wurden zwei Gedanken, nicht das Erscheinungsbild: die weiße
Tafel, die ein großes Bild überlappt, und die farbige Fläche mit
angeschrägter Kante. Winkel, Farbe und Einsatzhäufigkeit sind bewusst
anders gewählt, damit die Seite nicht wie eine Kopie wirkt.

---

## 1. Grundhaltung

Hell statt dunkel. Der Grund ist ein leicht warmes Off-White, die weißen
Flächen liegen darauf und tragen den Inhalt. Farbe gibt es genau eine:
ein warmes Gelb, und das ausschließlich als Fläche mit schwarzer Schrift
darauf. Gelbe Schrift auf Weiß kommt nicht vor, weder in Links noch in
Hervorhebungen noch in Zahlen.

Die Seite arbeitet nicht mit Effekten. Es gibt keine Verläufe, keinen
Schein hinter dem Hero, keine Leuchtkanten, keinen eigenen Cursor.
Tiefe entsteht über Flächenwechsel und die Überlappung von Tafel und
Bild, nicht über Licht.

## 2. Farben

| Token | Wert | Rolle |
|-------|------|-------|
| `--bg` | `#FFFFFF` | Seitengrund, reines Weiß |
| `--flaeche` | `#F1F0EC` | Chips, Platzhalter, ruhige Flächen |
| `--plate` | `#ECEAE4` | Fläche hinter den Projektbildern |
| `--text` | `#000000` | Überschriften, Zeichen, Linien |
| `--text-muted` | `#3A3A38` | Fließtext |
| `--text-dim` | `#63625C` | Meta-Zeilen, Mikrocopy |
| `--accent` | `#FFC400` | Gelb, **nur** als Fläche |
| `--accent-dark` | `#E8AE00` | Fokusring, Formularfokus |
| `--rand` | `max(48px, (100vw - 1560px)/2 + 48px)` | Fluchtlinie des Seiteninhalts |

Der Grund ist Weiß, nicht Creme. Creme mit Akzentfarbe ist genau der
Griff, den generierte Seiten nehmen, und die Seite wirkte damit matt.
Schwarz ist echtes Schwarz, kein getöntes Fast-Schwarz.

Die Seite **endet schwarz**: Fußzeile und Abschlussband laufen auf
`#000` beziehungsweise `#1A1A1A`. Der schwarze Block unter den
Leistungen nimmt das vorweg.

## 3. Die Schräge

Das einzige Formzitat. Immer derselbe Winkel: die Kante läuft über
`--cut` in der Höhe und `--cut * 2.6` in der Breite, also rund 21 Grad.
Nie 45 Grad, das wäre die Referenz.

Sie kommt an genau vier Stellen vor:

1. Projekttafel, an der Ecke zum Bild hin (`--cut: 22 bis 34px`)
2. Gelbe Fläche der Leistungskarten, unten rechts (`--cut: 20px`)
3. Gefüllte Knöpfe, unten rechts (`--cut: 9 bis 11px`)
4. Statuszeile im Hero und Kennzahl bei Champers, unten rechts

Mehr Stellen bekommt sie nicht. Jede weitere Schräge nimmt den
vorhandenen ihre Wirkung.

## 4. Projekte

Der ganze Bereich liegt auf `--plate` und laeuft randlos bis zur
Fensterkante. Dadurch sitzen die weissen Tafeln auf einer durchgehenden
Flaeche, statt als einzelne Rechtecke auf Weiss zu schweben.

Ein Projekt besteht aus zwei Teilen: `.work-visual` trägt das Bild auf
der Fläche `--plate`, `.work-content` ist die weiße Tafel.

Die Projektreihen laufen **bis an die Fensterkante**, nicht bis zum
Container. `.work-list` bricht dafür mit `margin-inline: calc(50% - 50vw)`
aus. Der Text in der Tafel hält trotzdem über `--rand` die Fluchtlinie
der übrigen Seite, sonst klebt er am Rand.

Beide liegen in derselben Rasterzeile eines zwölfspaltigen Grids und
überlappen sich um eine Spalte:

- `img-left`: Bild `1 / 8`, Tafel `7 / 13`, Schräge oben links
- `img-right`: Bild `6 / 13`, Tafel `1 / 7`, Schräge oben rechts

Die Bildseite bekommt auf der Überlappungsseite 13 Prozent zusätzlichen
Innenabstand, sonst verschwindet der Bildrand unter der Tafel.

Projektbilder sind freigestellte PNG-Mockups ohne Rahmen. Geräterahmen
aus CSS gibt es nicht mehr: wenn ein Mockup schon ein Gerät zeigt, wirkt
ein zweiter Rahmen darum gebastelt.

Die Seiten wechseln von Projekt zu Projekt. Unter 900px steht das Bild
oben und die Tafel rückt mit `-44px` darüber; die Reihenfolge wird dort
über `order` erzwungen, weil im Markup mal die Tafel und mal das Bild
zuerst steht.

Der Text in der Tafel sind genau drei Sätze: Aufgabe, was ich gemacht
habe, Ergebnis. Keine Labels davor, keine Zwischenüberschriften. Der
Knopf „Projekt ansehen" steht nur dort, wo es etwas Öffentliches zu
sehen gibt, derzeit allein bei der Campuskarte.

## 5. Leistungen

Drei weiße Karten nebeneinander. Oben links eine gelbe Fläche von
92 × 78px mit angeschrägter Unterkante, darin ein Strichzeichen als
Inline-SVG in `--text`. Die gelbe Fläche sitzt bündig in der Ecke, der
Text darunter hat seitlich Innenabstand.

Es sind bewusst drei und nicht vier: „Automatisierung mit KI" ist als
vierte Karte vorgesehen, soll aber noch nicht genannt werden.

## 6. Typografie

General Sans für alles. Barlow Condensed nur noch für die Wortmarke.
Keine Monoschrift, keine kursive Auszeichnungsschrift.

Keine Versalien, keine weite Sperrung. Die alte Labelsprache
(`PROJEKTE`, `01 · WEBDESIGN & FRONTEND`) ist ersatzlos entfallen,
samt Nummerierung. Kleinlabels unterscheiden sich jetzt über Größe und
Farbe vom Fließtext, nicht über die Form.

Überschriften laufen in Gewicht 500 bis 600, eng gesetzt
(`letter-spacing: -0.035em`), einzeilig und ohne farbige zweite Zeile.

## 7. Texte

- Schlicht und kurz. Keine Werbesprache, keine Schlagworte.
- Keine Gedankenstriche als Satzzeichen. Doppelpunkt, Komma oder Punkt.
- Barrierefreiheit wird nirgends als Stärke genannt. Die Kontraste
  stimmen trotzdem, das ist Handwerk und kein Verkaufsargument.
- Nichts behaupten, was nicht belegt ist. Fehlende Inhalte bekommen
  einen Platzhalter und eine Rückfrage.

## 8. Trennstriche

Es gibt praktisch keine mehr. Haarlinien über Überschriften, zwischen
Werdegangs-Einträgen und als Raster in den Werkzeugen sind entfallen,
weil sie das stärkste verbliebene Vorlagen-Signal waren. Gliederung
entsteht über Abstand, Flächenwechsel und gelbe Marker:

- Werdegang: Zeitraum als gelbes Schildchen links, kein Strich
- Werkzeuge: Gruppentitel mit gelbem Unterstrich, Einträge als Chips
- Projekt-Stichworte: Chips auf `--flaeche`, keine Punktekette

Ketten aus Mittelpunkten (`A · B · C`) sind überall ersetzt. Die
Disziplin eines Projekts steht als gelbes Schildchen, der Zeitraum
daneben in Grau.

## 9. Was es nicht mehr gibt

Rot in jeder Form. Den eigenen Cursor (der Zeiger war über Knöpfen
unsichtbar, das war ein Fehler und kommt nicht zurück). Den Schein
hinter dem Hero. Den grünen Reichweiten-Graph bei Champers, jetzt eine
gelbe Kennzahlfläche. Den Browserrahmen und den Hinweis „Gesamte Seite
scrollbar" bei der Uni Lübeck. Schatten hinter den Emojis.
Die Eyebrow-Zeilen. Die Nummerierung von Projekten, Leistungen und
Skill-Gruppen. Die Dekokoordinate im Hero. Die Pillen-Tags unter den
Projekten (jetzt eine Zeile mit Mittelpunkten). Die Unicode-Glyphen
als Leistungs-Icons (jetzt Inline-SVG). Den grünen Reichweiten-Graph
(jetzt eine graue Linie im Hintergrund).
