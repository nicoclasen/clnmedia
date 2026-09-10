# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Was das ist

Portfolio-Website von Nico Clasen (clnmedia.de). Reine statische Seite: drei HTML-Dateien, keine Dependencies, kein Build, kein Test-Setup, kein `package.json`. Sprache der Inhalte ist Deutsch.

## Entwicklung

Es gibt keinen Build- und keinen Lint-Schritt. Zum Ansehen einen statischen Server im Projektwurzelverzeichnis starten:

```
python -m http.server 8000
```

Ueber `file://` oeffnen funktioniert nicht: alle Asset-Pfade sind wurzel-absolut (`/images/...`).

Deployment laeuft ueber Vercel. `vercel.json` setzt `cleanUrls`, die Rechtsseiten sind also unter `/impressum` und `/datenschutz` erreichbar, nicht unter `.html`.

## Aufbau

- [index.html](index.html) — die komplette Seite. Ein einziger `<style>`-Block am Anfang, ein einziger `<script>`-Block am Ende, dazwischen das Markup. Sektionen sind mit `<!-- ===== NAME ===== -->` abgetrennt und tragen die IDs, auf die die Navigation ankert: `work`, `services`, `about`, `skills`, `contact`.
- [impressum.html](impressum.html), [datenschutz.html](datenschutz.html) — eigenstaendige Seiten mit eigener Kopie der CSS-Variablen und des Cursor-/Nav-Skripts. Sie haben kein mobiles Menue.
- [images/](images/) — jedes Bild liegt als `.webp` und `.jpg` vor.

Es gibt keine gemeinsame CSS- oder JS-Datei. Design-Tokens (`--bg`, `--accent`, `--font-display` …) stehen dreimal im Repo, einmal pro HTML-Datei. Farb- oder Schriftaenderungen muessen in allen drei Dateien nachgezogen werden.

## Gestalterische Haltung

Die Seite folgt der Referenz in [DESIGN.md](DESIGN.md). Vor Änderungen an Layout, Typografie oder Copy dort Abschnitt 7 und 8 lesen. Die vier Regeln, die man am leichtesten versehentlich bricht:

- **Ein Sektionsmuster.** Eyebrow (ein Wort), Headline in Sentence Case, eine Zeile Subline, höchstens ein Link. Keine Sektion bekommt einen zweiten Handlungspfad.
- **Ein CTA, wortgleich.** "Gespräch starten" steht viermal auf der Seite und wird nie umformuliert. Neue Buttons übernehmen genau diesen Text oder es kommt keiner dazu. Der Abschlussblock im Footer bleibt bewusst ohne Knopf, weil das Kontaktformular direkt darüber steht.
- **Das Interface bleibt still.** Bewegung gehört in die Case-Animationen, nicht in Hover-States. Rot ist auf Punktgröße beschränkt: Logo-Dot, Statuspunkt, Fokus-Ring, Hover-Farbe von Sektionslinks.
- **Eine Schriftfamilie.** General Sans trägt Fließtext, Headlines und über `--font-label` auch alle Kleinlabels. Es gibt keine Monoschrift mehr. Barlow Condensed (`--font-display`) bleibt nur für Wortmarke und Icons.
- **Große Headlines** laufen in General Sans, Gewicht 500, eng gesetzt und ohne Versalien. Die zweite Zeile steht in `--text-muted`, nicht in der Akzentfarbe.

Die zugehörigen Regeln liegen gebündelt am Ende des Style-Blocks in [index.html](index.html) unter der Überschrift **"STILLE EBENE"**. Sie ist die letzte Ebene vor dem Reduced-Motion-Block und gewinnt damit gegen alles darüber. Neue Regeln dieser Haltung gehören dorthin, nicht in die früheren Ebenen.

Achtung bei den Farbtoken: `index.html` enthält **zwei** `:root`-Blöcke. Maßgeblich ist der zweite unter "ART DIRECTION 2026". Änderungen im ersten Block bleiben wirkungslos.

## Muster, an die man sich halten sollte

**Interaktive Cases als gekapselte IIFE.** Jede Animation im Work-Bereich ist ein eigener `(() => { … })()`-Block, der zuerst sein Element per `getElementById` sucht und bei `null` sofort zurueckkehrt. Ausgeloest wird fast alles ueber einen `IntersectionObserver`, der sich nach dem ersten Treffer per `unobserve` selbst abmeldet. Neue Effekte bitte genauso bauen, damit das Entfernen eines Cases nichts anderes bricht.

**`prefers-reduced-motion` respektieren.** Alle laufenden Animationen (Auto-Scroll im Browserfenster, aufsteigende Emojis, Reichweiten-Zaehler) pruefen `window.matchMedia('(prefers-reduced-motion: reduce)')` und zeigen dann den Endzustand statt der Bewegung.

**Eigener Cursor.** `body { cursor: none }` plus ein `.cursor`-Div, das der Maus folgt und bei Hover ueber `a, button, .work-item, .service-card, .career-block` waechst. Unter 768px und bei `(hover: none)` wird beides zurueckgesetzt. Neue klickbare Elementklassen in die Hover-Liste im Skript aufnehmen.

**Bilder.** Immer als `<picture>` mit WebP-Source und JPG-Fallback, immer mit `width`, `height`, `loading="lazy"` und `decoding="async"`. Beim Hinzufuegen eines Bildes beide Formate erzeugen.

**Hochkante Formate auf kleinen Schirmen.** Das Kampagnen-Board zeigt ein Motiv in drei Seitenverhaeltnissen, darunter einen Skyscraper mit 1:3,75. Breitengesteuerte Bilder laufen damit auf dem Telefon extrem in die Laenge, deshalb sind die Hoehen unter 969px gedeckelt: Tablet zeigt alle drei nebeneinander auf einer Grundlinie, das Telefon das Querformat oben und die beiden Hochformate darunter. Zwei Fallen dabei: das erste Kind des Boards ist die Badge, Positionsselektoren muessen deshalb `nth-of-type` verwenden, und eine feste Mindesthoehe erzeugt am unteren Rand des Tablet-Bereichs Ueberlauf.

**Kontaktformular.** Laeuft ueber Web3Forms. Der Access Key steht als `hidden`-Input im Markup, dazu ein unsichtbares Honeypot-Feld. Abgesendet wird per `fetch` ohne Seitenwechsel, Rueckmeldung landet in `#formStatus`; im Fehlerfall wird auf die Mailadresse verwiesen.

**Umlaute.** Im Markup werden Umlaute teils als HTML-Entity (`&uuml;`) geschrieben, teils direkt. Beides existiert, im umgebenden Abschnitt konsistent bleiben.

## Commits

Commit-Nachrichten sind deutsch, knapp und beschreiben das sichtbare Ergebnis, nicht die Technik ("Logo wieder klein, Auswahlmenue lesbar"). Umlaute werden darin umschrieben: ue, ae, oe.
