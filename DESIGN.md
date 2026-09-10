# DESIGN.md

Design-Referenz: https://pryzm.design
Erstellt: 2026-09-10
Status: Layout-Rhythmus verifiziert aus dem Seiten-Quelltext. Farb-, Typo- und
Abstandswerte sind als TODO markiert und müssen aus dem kompilierten CSS
ausgelesen werden (siehe Abschnitt "Offene Werte").

---

## 1. Grundhaltung

Dark-first. Die deklarierte Theme-Farbe ist `#0a0a0a` — kein reines Schwarz,
sondern ein minimal aufgehelltes Near-Black. Alles Weitere baut als Licht auf
diesem Grund auf: die Seite arbeitet nicht mit Flächenfarbe, sondern mit
Leuchten, Glas und Korn.

Das Teure an dieser Seite ist nicht Dekoration, sondern Zurückhaltung bei
gleichzeitig hoher Bildqualität. Die Struktur ist konventionell und ruhig; die
Spannung entsteht ausschließlich über bewegtes, hochwertiges Bildmaterial in
ansonsten sehr aufgeräumten Sektionen.

## 2. Layout-Rhythmus (verifiziert)

Jede inhaltliche Sektion folgt exakt demselben Dreiklang:

1. **Eyebrow** — ein einzelnes kurzes Wort in Kleinschrift über der Headline
   (`Flow`, `Remix`, `Embed`, `Pricing`, `FAQ`)
2. **Headline** — kurz, im Satzbau gesprochen, Sentence Case, nie mehr als eine
   Zeile Aussage
3. **Eine Zeile Subline**, dann **ein einzelner Link/CTA**

Diese Wiederholung ist das tragende Element. Kein Sektionstyp bricht aus dem
Muster aus, keine Sektion hat mehr als einen primären Handlungspfad.

**Sektionsabfolge:**

| # | Sektion | Inhaltstyp |
|---|---------|-----------|
| 1 | Header | Logo links, ein einzelner CTA rechts |
| 2 | Announcement | einzeilige Neuigkeit über dem Hero |
| 3 | Hero | Headline, eine Zeile Subline, CTA-Paar (primär + sekundär) |
| 4 | Hero-Media | Video-Loop (`.webm`), volle Breite, mit eigenem CTA darunter |
| 5 | Feature "Flow" | Eyebrow + Headline + Subline + Link + Bild |
| 6 | Gallery "Remix" | Raster aus Looks: Name, ein Satz Beschreibung, Tags |
| 7 | Feature "Embed" | wie 5, aber mit Code-Block statt Bild |
| 8 | Pricing | zwei Tiers, Monats-/Jahres-Toggle, Feature-Listen als Bullets |
| 9 | FAQ | Akkordeon, Fragen in gesprochener Sprache |
| 10 | Newsletter | Bild + Headline + ein Eingabefeld + Mikrocopy darunter |
| 11 | Closing CTA | wiederholt die Hero-CTAs wörtlich |
| 12 | Footer | Logo, ein Satz Positionierung, zweites Newsletter-Feld, 3 Linkspalten |

**Bemerkenswert:** Der Hero-CTA (`Open studio`) taucht auf der Seite fünfmal
auf — im Header, im Hero, unter dem Hero-Video, in der Preistabelle und im
Closing. Immer identisch beschriftet. Das ist Absicht: ein einziges Ziel, kein
konkurrierender Handlungspfad.

## 3. Content-Dichte

Niedrig bis mittel. Kein Fließtext über drei Zeilen außerhalb der FAQ. Feature-
Beschreibungen sind ein bis zwei Sätze. Die Gallery-Einträge tragen jeweils
genau einen beschreibenden Satz, sinnlich formuliert statt technisch.

Die Bullets in der Preistabelle sind Nutzenaussagen, keine Feature-Namen.

## 4. Media-Strategie

- Hero: Video-Loop (`.webm`), nicht Standbild
- Feature-Sektionen: `.webp`, je ein Bild pro Sektion, nie mehrere
- Gallery: gerastertes Vorschaubild pro Eintrag
- Footer: dekoratives Bild als Abschluss

Format `.webm`/`.webp` durchgängig — Ladezeit ist erkennbar Teil der
Qualitätshaltung.

## 5. Motion

**TODO — nicht aus dem Quelltext ablesbar.** Zu prüfen: ob Sektionen beim
Scrollen eingeblendet werden, ob es Parallax gibt, wie Hover-States auf den
Gallery-Karten reagieren. Vermutung aufgrund der Produktgattung (WebGL-
Hintergrundgenerator): Bewegung liegt im Bildmaterial selbst, das Interface
darum herum bewegt sich kaum.

## 6. Offene Werte (aus dem CSS zu ergänzen)

Diese Werte sind für ein Design-System zwingend und hier bewusst leer, statt
geraten:

- **Farbsystem**: bekannt ist nur `#0a0a0a` (Theme-Color). Fehlen: Textfarben
  primär/sekundär, Rahmenfarbe, Akzentfarbe, Surface-Abstufungen für Karten
- **Typo-Skala**: Schriftpaarung, Größen für Eyebrow / H1 / H2 / Body / Mikrocopy,
  Zeilenhöhen, Letter-Spacing der Eyebrows
- **Abstandssystem**: Basiseinheit, vertikaler Sektionsabstand, Innenabstände
  von Karten und Preisboxen
- **Radien**: Karten, Buttons, Eingabefelder
- **Container-Breite** und Rasterverhalten der Gallery über Breakpoints

## 7. Übertragbare Prinzipien

Unabhängig von den konkreten Werten sind das die Regeln, die diese Seite teuer
wirken lassen:

1. Ein einziges Sektionsmuster, ausnahmslos durchgehalten
2. Ein einziger primärer CTA, wörtlich identisch wiederholt
3. Near-Black statt Schwarz als Grund
4. Bewegtes Bildmaterial als einziger visueller Aufwand — das Interface bleibt still
5. Headlines gesprochen, nicht beworben; Sentence Case
6. Mikrocopy unter jedem Eingabefeld, die Bedenken vorwegnimmt
7. Sichtbare Großzügigkeit im Leerraum statt zusätzlicher Elemente

---

## 8. Umsetzung auf clnmedia.de (2026-09-10)

Wie die sieben Prinzipien auf dieser Seite gelandet sind. Der Code dazu liegt
gebündelt am Ende des Style-Blocks in `index.html` unter der Überschrift
**"STILLE EBENE"**.

| Prinzip | Umsetzung |
|---------|-----------|
| 1 Ein Sektionsmuster | Jeder `.section-header` ist ein Block: Eyebrow (ein Wort), Headline, eine Zeile Subline, höchstens ein Link. Die Nummerierung in den Eyebrows ("Arbeiten / 002") ist entfallen. |
| 2 Ein CTA | "Gespräch starten" steht viermal auf der Seite: Navigation, Hero, Arbeiten-Kopf, Leistungs-Block. Wortgleich, nie umformuliert. |
| 3 Near-Black | `--bg: #0A0A0A` im maßgeblichen Token-Block ("ART DIRECTION 2026"). |
| 4 Stilles Interface | Rahmen-Hover neutral statt rot (`--border-hover`), Projektkacheln ohne Farbwechsel. Bewegung bleibt in den Case-Animationen. |
| 5 Sentence Case | Alle großen Headlines laufen in General Sans, Gewicht 500, eng gesetzt, ohne Versalien. Die zweite Zeile steht in `--text-muted` statt in Rot. |
| 5b Eine Schriftfamilie | Die Monoschrift ist ersatzlos entfallen. Eyebrows, Labels, Buttons und Mikrocopy laufen über `--font-label` ebenfalls in General Sans, versal und weit gesperrt. |
| 6 Mikrocopy | "Antwort in der Regel innerhalb von 24 Stunden" unter dem Hero-CTA, dazu der Datenschutz-Hinweis unter dem Absenden-Knopf. |
| 7 Leerraum | Sektionsabstand auf `clamp(104px, 15vh, 184px)`, Sublines auf je eine Zeile gekürzt, Index-Marker im Hero auf die Ortsangabe reduziert. |

Bewusst abweichend von der Referenz:

- **Kein Announcement-Balken über dem Hero.** Die vorhandene Eyebrow-Zeile
  trägt dieselbe Information. Ein zweites Band wäre ein zusätzliches Element
  gewesen und hätte Prinzip 7 widersprochen.
- **Der Closing-Block trägt keinen Knopf.** In der Referenz wiederholt das
  Closing die Hero-CTAs. Hier steht direkt darüber das Kontaktformular, ein
  Knopf würde also auf den Container unmittelbar darüber zeigen. Der Abschluss
  bleibt deshalb eine reine Aussage: Headline, eine Zeile, dann die Trennlinie
  zur Wortmarke.
- **Keine Monoschrift.** JetBrains Mono wirkte technisch statt hochwertig und
  ist samt Google-Fonts-Einbindung entfallen. Die Seite lädt nur noch General
  Sans (Fontshare) und Barlow Condensed für Wortmarke und Icons.
- **Rot bleibt als Markenfarbe erhalten**, aber nur noch in Punktgröße: Logo-Dot,
  Statuspunkt, Fokus-Ring, Hover-Farbe der Sektionslinks und ein weicher
  Schein hinter dem Hero.
- **Der eigene Cursor bleibt unangetastet.**
