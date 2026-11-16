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

## Geprüft, nichts zu tun

Cookies, `localStorage` und `sessionStorage`: die Seite nutzt nichts davon,
gemessen auf allen drei Seiten. Ein Einwilligungsbanner nach § 25 TDDDG ist
deshalb nicht nötig. Externe Anfragen beim Seitenaufruf: keine.
Wer das ändert (Analyse-Tool, eingebettete Karte, externes Video,
Schriften von fremden Servern), muss die Lage neu bewerten.

## Lokale Auffindbarkeit (Ziel: Kundenanfragen aus der Region)

Reihenfolge nach Wirkung. Die ersten beiden kann nur Nico selbst machen,
sie sind zusammen wichtiger als alles auf der Seite.

- [ ] **Google Search Console.** Property für clnmedia.de anlegen, am
      einfachsten über die Vercel-Integration oder per DNS-TXT-Eintrag.
      Dann `sitemap.xml` einreichen und für die Startseite einmal
      „Indexierung beantragen". Ohne das kann eine neue Domain, auf die
      nichts verlinkt, monatelang unentdeckt bleiben.

- [ ] **Google Unternehmensprofil.** Für Suchen wie „Webdesign Lübeck"
      der stärkste einzelne Hebel, weil er in die Kartenergebnisse führt,
      wo keine Agenturseite mit dutzenden Unterseiten im Weg steht.
      Als Dienstleistungsgebiet anlegen, ohne öffentliche Adresse:
      - Hauptkategorie: Webdesigner
      - Weitere: Grafikdesigner, Werbeagentur, Internetmarketing-Dienst
      - Gebiet: Lübeck, Bad Segeberg, Bad Oldesloe, Neumünster
      - Keine Lübecker Adresse erfinden. Das fällt auf und kostet das Profil.

- [ ] **Die ersten Links setzen.** Auf clnmedia.de verlinkt bisher nichts,
      und das ist für eine neue Domain die eigentliche Decke. Kostenlos und
      in eigener Hand: LinkedIn-Profil (Feld „Website"), GitHub-Profil,
      Instagram-Bio, E-Mail-Signatur. Dazu auf Nachfrage: SV Schackendorf,
      Champers. Jeder echte Link zählt mehr als jede weitere Textänderung.

