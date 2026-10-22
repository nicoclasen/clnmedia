# TODO

Offene Punkte für clnmedia.de. Erledigtes bitte löschen, nicht abhaken.

## Gestaltung

- [ ] **Foto im Hero.** Rechts oben Platz für ein Foto von Nico, die graue
      Faktenbox rückt direkt darunter und steht dann auf Höhe des
      Textblocks links. Aktuell steht die Faktenbox allein rechts, der
      Platz darüber ist bewusst frei gelassen.
      Format: Hochformat, etwa 1000 × 1250, freundlich und sachlich,
      gedämpfte Farben, kein Blau und kein Rot im Motiv.

- [ ] **Vierte Leistungskarte „Automatisierung mit KI".** Das Raster ist
      auf drei Spalten gesetzt und nimmt eine vierte Karte ohne
      Layoutänderung auf. Icon im selben Stil wie die drei vorhandenen:
      Inline-SVG, schwarze Flächen, 32 × 32 Viewbox.

## Bildmaterial

Vier Stellen auf der Seite warten auf Bilder. Alle im selben Griff:
natürliches Licht, gedämpfte Farben, kein Stockfoto-Lächeln, kein Blau
und kein Rot im Motiv, sonst konkurriert es mit Gelb.

- [ ] **Band unter dem Hero**, 2400 × 900, Querformat.
      Arbeitsplatz, Kamera, Notizen. Nicht frontal in die Kamera.
- [ ] **Abschlussband über der Fußzeile**, 2400 × 1000, dunkel.
      Liegt hinter „Offen für neue Projekte" mit dunkler Überlagerung,
      also ruhiges Motiv ohne viel Detail in der linken Hälfte.
- [ ] **Kontakt, neben dem Formular**, 1200 × 1400, Hochformat.
- [ ] **Über mich, zweites Bild unter dem Portrait**, 1200 × 1500.

## Aufräumen

- [ ] **Tote Bilddateien löschen.** Werden nicht mehr referenziert,
      liegen aber im Repo (jeweils `.jpg` und `.webp`, zusammen gut 3 MB):
      `campus-desktop`, `campus-indoor`, `campus-mobile`, `svs-1`,
      `svs-2`, `svs-3`, `uni-web-full`, `uni-web-hero`, `uni-handout`,
      `uni-camp-poster`, `champers-terminal`.

- [ ] **PNG-Fallbacks der Mockups verkleinern.** `campus-mockup.png`,
      `svs-mockup.png` und `uni-mockup.png` liegen bei 1,2 bis 1,6 MB.
      Sie laden nur in Browsern ohne WebP-Unterstützung, belasten aber
      das Repo. Entweder stark komprimieren oder ersatzlos streichen und
      das `<picture>` auf die WebP-Quelle reduzieren.

## Nach dem nächsten Push

- [ ] **Google Search Console.** Property für clnmedia.de anlegen und
      `sitemap.xml` einreichen. Ohne das sieht Google die Seite nicht.
- [ ] **Google Unternehmensprofil.** Für lokale Suchen wie
      „Webdesign Lübeck" der stärkste einzelne Hebel, stärker als alles
      auf der Seite selbst.
