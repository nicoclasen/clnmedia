# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Was das ist

Portfolio-Website von Nico Clasen (clnmedia.de). Reine statische Seite: drei HTML-Dateien, keine Dependencies, kein Build, kein Test-Setup, kein `package.json`. Sprache der Inhalte ist Deutsch.

## Entwicklung

Es gibt keinen Build- und keinen Lint-Schritt. Zum Ansehen einen statischen Server im Projektwurzelverzeichnis starten:

```
npx serve .
```

`serve` loest `/impressum` und `/datenschutz` auf die passenden `.html`-Dateien auf und verhaelt sich damit wie die Produktion. `python -m http.server` tut das **nicht**: die beiden Rechtsseiten laufen dort in einen 404, weil die Links wurzel-absolut und ohne Endung gesetzt sind. Wer die Seite nur ueberfliegen will, kann Python nehmen und die Rechtsseiten direkt unter `/impressum.html` aufrufen.

Noch naeher an der Produktion ist `vercel dev`, das `vercel.json` samt `cleanUrls` mitliest.

Ueber `file://` oeffnen funktioniert nicht: alle Asset-Pfade sind wurzel-absolut (`/images/...`).

Deployment laeuft ueber Vercel. `vercel.json` setzt `cleanUrls`, die Rechtsseiten sind also unter `/impressum` und `/datenschutz` erreichbar, nicht unter `.html`.

## Aufbau

- [index.html](index.html) — die komplette Seite. Ein einziger `<style>`-Block am Anfang, ein einziger `<script>`-Block am Ende, dazwischen das Markup. Sektionen sind mit `<!-- ===== NAME ===== -->` abgetrennt und tragen die IDs, auf die die Navigation ankert: `work`, `services`, `about`, `skills`, `contact`.
- [impressum.html](impressum.html), [datenschutz.html](datenschutz.html) — eigenstaendige Seiten mit eigener Kopie der CSS-Variablen und des Cursor-/Nav-Skripts. Sie haben kein mobiles Menue.
- [images/](images/) — Seitenbilder liegen nur als `.webp` vor, siehe unten.

Es gibt keine gemeinsame CSS- oder JS-Datei. Design-Tokens (`--bg`, `--accent`, `--font-display` …) stehen dreimal im Repo, einmal pro HTML-Datei. Farb- oder Schriftaenderungen muessen in allen drei Dateien nachgezogen werden.

## Gestalterische Haltung

Die Seite folgt [DESIGN.md](DESIGN.md). Vor Änderungen an Layout, Typografie oder Copy dort die Abschnitte 1 bis 7 lesen. Die Regeln, die man am leichtesten versehentlich bricht:

- **Gelb ist eine Fläche, keine Schriftfarbe.** `--accent` darf als Hintergrund mit schwarzer Schrift darauf stehen, nie als `color` auf hellem Grund. Das gilt auch für Links, Zahlen, Punkte und Hover-Zustände. Wer eine neue Stelle einfärbt, prüft das zuerst.
- **Die Schräge kommt an vier Stellen vor**, immer im selben Winkel (`--cut` hoch, `--cut * 2.6` breit, also rund 21 Grad): Projekttafel, gelbe Fläche der Leistungskarten, Knöpfe, Statuszeile im Hero. Jede weitere Schräge schwächt die vorhandenen.
- **Keine Versalien, keine weite Sperrung.** Kleinlabels unterscheiden sich über Größe und Farbe, nicht über die Form. Die alten Eyebrow-Zeilen und die Nummerierung sind entfallen und kommen nicht zurück.
- **Der Seitengrund ist reines Weiss.** Projekttafeln und Leistungskarten heben sich ueber Schatten und die getoente Bildflaeche ab, nicht ueber eine andere Fuellfarbe. Creme als Grund kommt nicht zurueck, die Seite wirkte damit matt.
- **Keine Effekte.** Keine Verläufe, kein Schein, keine Leuchtkanten, kein eigener Cursor. Tiefe entsteht über Flächenwechsel und die Überlappung von Tafel und Bild.
- **Drei Sätze pro Projekt**: Aufgabe, was ich gemacht habe, Ergebnis. Keine Labels davor. Der Knopf „Projekt ansehen" steht nur dort, wo es etwas Öffentliches zu sehen gibt.
- **Texte schlicht und kurz.** Keine Werbesprache, keine Schlagworte, keine Gedankenstriche als Satzzeichen. Barrierefreiheit wird nirgends als Stärke genannt.
- **Keine Trennstriche.** Haarlinien über Überschriften, zwischen Werdegangs-Einträgen und als Raster in den Werkzeugen sind entfallen. Gliederung entsteht über Abstand, Flächenwechsel und gelbe Marker. Wer einen Strich einbaut, baut das stärkste Vorlagen-Signal wieder ein.
- **Keine Ketten aus Mittelpunkten** (`A · B · C`) und keine Pfeile hinter Knopftexten. Beides sind Vorlagen-Tells.
- **Der Zeiger bleibt sichtbar.** `cursor: none` steht an sieben Stellen in den älteren Ebenen und wird am Ende des Style-Blocks überschrieben. Nicht wieder aktivieren.
- **Projektreihen laufen bis zur Fensterkante**, der Text darin hält über `--rand` die Fluchtlinie der Seite.
- **Die Navigation ist nicht mehr fest.** Sie steht per `position: absolute` am Seitenanfang und scrollt mit nach oben weg. Grund: Safari auf dem iPhone setzt feste Elemente unter die Statusleiste, waehrend der Inhalt dahinter durchscrollt, und hinterlaesst dort einen Streifen. Weder `viewport-fit=cover` noch eine Abdeckung noch das Entfernen von `overflow-x` haben das geloest. Nur solange das Menue offen ist, wird die Leiste ueber `.nav.menu-aktiv` wieder fest, sonst waere das Kreuz zum Schliessen nicht erreichbar.
- **Die Seite endet schwarz.** Fußzeile `#000`, Abschlussband `#1A1A1A` direkt an der Oberkante der Fußzeile (`.footer { padding-top: 0 }`), der Block unter den Leistungen nimmt es vorweg.
- **Der Arbeiten-Bereich liegt auf `--plate`**, randlos bis zur Fensterkante. Die weissen Tafeln sitzen auf dieser durchgehenden Flaeche, statt als einzelne Rechtecke auf Weiss zu stehen.
- **Unterstriche an Links** liegen als `::after` unter dem Text und werden beim Zeigen dicker und tiefer. Kein Fuellen der ganzen Zeile mit Gelb, das sah nach Marker aus.
- **`--text-dim` nicht aufhellen.** `#63625C` liegt knapp über 4,5:1 auf Weiß. Jeder hellere Wert bricht die Lesbarkeit von Meta-Zeilen und Mikrocopy.

Die Regeln liegen gebündelt am Ende des Style-Blocks in [index.html](index.html), in dieser Reihenfolge: **„LABELS ENTFERNT"**, **„HELLE EBENE"**, **„PROJEKTE"**, **„LEISTUNGEN"**, **„DRITTE RUNDE"**, **„PROJEKTE BIS AN DEN RAND"**, **„WERDEGANG, WERKZEUGE, PORTRAIT"**. Maßgeblich ist immer die unterste: die früheren Ebenen sind historisch gewachsen und werden grossteils überschrieben. Neue Regeln gehören ans Ende, nicht in die früheren Ebenen.

Achtung bei den Farbtoken: `index.html` enthält **zwei** `:root`-Blöcke. Maßgeblich ist der zweite unter "ART DIRECTION 2026". Änderungen im ersten Block bleiben wirkungslos. Die Token stehen außerdem je einmal in `impressum.html` und `datenschutz.html`; Farbänderungen müssen in allen drei Dateien nachgezogen werden.

## Muster, an die man sich halten sollte

**Interaktive Cases als gekapselte IIFE.** Jede Animation im Work-Bereich ist ein eigener `(() => { … })()`-Block, der zuerst sein Element per `getElementById` sucht und bei `null` sofort zurueckkehrt. Ausgeloest wird fast alles ueber einen `IntersectionObserver`, der sich nach dem ersten Treffer per `unobserve` selbst abmeldet. Neue Effekte bitte genauso bauen, damit das Entfernen eines Cases nichts anderes bricht.

**`prefers-reduced-motion` respektieren.** Alle laufenden Animationen (Auto-Scroll im Browserfenster, aufsteigende Emojis, Reichweiten-Zaehler) pruefen `window.matchMedia('(prefers-reduced-motion: reduce)')` und zeigen dann den Endzustand statt der Bewegung.

**Kein eigener Cursor mehr.** Das `.cursor`-Div und das zugehoerige Skript liegen noch im Markup, sind aber per `display: none` und `cursor: auto` stillgelegt. Nicht wiederbeleben, es war eines der Vorlagen-Signale.

**Bilder.** Nur noch WebP, ein schlichtes `<img src="/images/....webp">` ohne `<picture>` und ohne JPG- oder PNG-Fallback. Die Fallbacks waren bis zu 1,6 MB schwer und wurden von keinem Browser der letzten fuenf Jahre je angefordert. Immer mit `width`, `height`, `loading="lazy"` und `decoding="async"`.

Drei Ausnahmen bleiben in anderen Formaten, weil sie keine Seitenbilder sind: `og-image.jpg` (manche Scraper verstehen kein WebP), `champers-reel-poster.jpg` (Poster des Videos) und `nico-clasen.jpg` (steht so in den strukturierten Daten).

**Hochkante Formate auf kleinen Schirmen.** Das Kampagnen-Board zeigt ein Motiv in drei Seitenverhaeltnissen, darunter einen Skyscraper mit 1:3,75. Breitengesteuerte Bilder laufen damit auf dem Telefon extrem in die Laenge, deshalb sind die Hoehen unter 969px gedeckelt: Tablet zeigt alle drei nebeneinander auf einer Grundlinie, das Telefon das Querformat oben und die beiden Hochformate darunter. Zwei Fallen dabei: das erste Kind des Boards ist die Badge, Positionsselektoren muessen deshalb `nth-of-type` verwenden, und eine feste Mindesthoehe erzeugt am unteren Rand des Tablet-Bereichs Ueberlauf.

**Kontaktformular.** Laeuft ueber Web3Forms. Der Access Key steht als `hidden`-Input im Markup, dazu ein unsichtbares Honeypot-Feld. Abgesendet wird per `fetch` ohne Seitenwechsel, Rueckmeldung landet in `#formStatus`; im Fehlerfall wird auf die Mailadresse verwiesen.

**Umlaute.** Im Markup werden Umlaute teils als HTML-Entity (`&uuml;`) geschrieben, teils direkt. Beides existiert, im umgebenden Abschnitt konsistent bleiben.

## Commits

Commit-Nachrichten sind deutsch, knapp und beschreiben das sichtbare Ergebnis, nicht die Technik ("Logo wieder klein, Auswahlmenue lesbar"). Umlaute werden darin umschrieben: ue, ae, oe.
