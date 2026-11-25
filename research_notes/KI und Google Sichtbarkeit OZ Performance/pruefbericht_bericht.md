# Prüfbericht zu "KI und Google Sichtbarkeit OZ Performance.md"

**Urteil: Nicht versandfertig. Zwei kritische und neun wichtige Punkte müssen vorher korrigiert werden; der Rest des Berichts ist den Notizen gegenüber sauber und in den Website-Fakten fast durchgehend live bestätigt.**

Zählung: **kritisch 2 · wichtig 9 · klein 8** (19 Befunde).

Geprüft am 25.11.2026: Bericht vollständig (283 Zeilen), sieben Notizdateien vollständig (ohne ecu_de_ablauf_versand.md), Live-Abruf von 35 Adressen auf www.ozperformance.de plus zwei Zweit-Domains (curl mit Browser-Kennung, nur lesend, 1 s Pause).

Nicht prüfbar aus dieser Sitzung: fremde Websites (kfz-reparatur24.de, motronik-service.de, repairfirst.de, club.autodoc.de lieferten keine Verbindung). Befund 1 stützt sich deshalb auf die Notizen und die im Bericht selbst verlinkten Adressen, nicht auf einen eigenen Abruf dieser Seiten.

Positiv und ohne Befund: kein Rangversprechen (der Bericht schließt einen garantierten Platz 1 ausdrücklich aus), Bewertungsablauf ohne Gegenleistung und ohne Vorfilter, Rechtsabschnitte mit Vorbehalt, Google-Update-Daten, Ask-Maps-Datum, ZF-Zahlen, Urteile (BGH 2018, OLG Frankfurt, OLG Bamberg, BGH-Logo-Urteil) und die Kernzahlen der KI-Studien stimmen mit den Notizen überein. Der Widerspruch zwischen den Notizen (drei Notizen sahen "UG" noch in Seitentiteln, das Audit nicht) ist im Bericht richtig zugunsten des Live-Audits aufgelöst; live bestätigt.

---

## Live-Stichproben (35 Abrufe, 27 Aussagen)

| # | Aussage im Bericht | Ergebnis | Gesehen |
|---|---|---|---|
| 1 | /getriebeinstandsetzung, /leistungen/getriebeinstandsetzung, /softwareoptimierung enden auf Fehlerseite | bestätigt | alle drei HTTP 404; Variante mit Schrägstrich 301 auf Variante ohne, dann 404 |
| 2 | Nur /preise und /preisrechner sind weitergeleitet | bestätigt | 301 nach /leistungen bzw. /termin |
| 3 | /motorinstandsetzung/, /getriebe, /agbs/, /leistungen/getriebespuelung "nicht einzeln live geprüft" | jetzt geprüft | alle 404, ebenso /getriebespuelung und /leistungen/softwareoptimierung |
| 4 | Sitemap meldet 24 Adressen, darunter Fehlerseite, zwei weitergeleitete, eine Hilfsseite | bestätigt | pages-sitemap.xml 21 + store-categories-sitemap.xml 3; enthält /404, /preise, /preisrechner, /termin/verwalten |
| 5 | Alle Leistungs-, Angebots-, Ratgeber-, Stadt- und Produktseiten fehlen in der Sitemap | bestätigt | kein Eintrag unter /leistungen/, /angebote/, /ratgeber/, /standorte/, /products/ |
| 6 | Ursache: Seitenvorlagen ohne Anmeldung | bestätigt | /_wix/pages.json: nur /category/[slug] und /products/[slug] tragen Kennungen |
| 7 | robots.txt sperrt keinen KI-Roboter | bestätigt | keine Regel für GPTBot, OAI-SearchBot, ClaudeBot, PerplexityBot, Bingbot; Abruf mit GPTBot-Kennung: 200, 69.119 Bytes wie mit Browser |
| 8 | "Kein Suchroboter ist ausgesperrt" | falsch (klein) | `User-agent: PetalBot / Disallow: /` (siehe Befund 14) |
| 9 | llms.txt von Wix, verlinkt nur die Startseite | bestätigt | ein Link "home", sonst MCP-Beschreibung; /llms-full.txt 404 |
| 10 | Ohne www leitet in einem Schritt auf www | bestätigt | https://ozperformance.de/kontakt 301 nach www |
| 11 | Kein "UG", kein "Performnce" auf der Website | bestätigt | in 28 geprüften Seiten 0 Treffer; Impressum: OZ Performance GmbH, HRB 21451 |
| 12 | P1735 nur auf drei Seiten | bestätigt (Stichprobe) | Treffer nur auf den zwei DQ381/DQ500-Angeboten und Mechatronik-Reparatur |
| 13 | Keine Seite mit Code in Titel oder Hauptüberschrift; 10666, P173500, "VW P1735" fehlen | bestätigt | Titel "DQ381/DQ500 Drucksensor Reparatur Bochum"; 0 Treffer für 10666, P173500, "VW P1735" |
| 14 | "Nirgends stehen Modellnamen wie Golf oder Tiguan im Zusammenhang mit dem Code" | falsch | siehe Befund 12 |
| 15 | Angebotsseite Drucksensor "ab 400 €" | bestätigt, aber unvollständig | siehe Befund 3 (1.200 € Komplettpaket steht daneben) |
| 16 | "Chiptuning" genau einmal | bestätigt | einmal als Reiterbeschriftung "Leistungssteigerung (Chiptuning)", zusätzlich nur in der Adresse chiptuning-konfigurator.de |
| 17 | Öffnungszeiten Mo–Fr 9–18, Sa 9–13 | bestätigt | Kontaktseite, Fußzeile und Firmendaten im Quelltext |
| 18 | "4,9 ★ 285 Google-Bewertungen", Rezension Klaus W., April 2026, Tiguan, P1736, am selben Tag fertig | bestätigt | wörtlich auf der Startseite |
| 19 | "1.500+ Getriebespülungen pro Jahr" | bestätigt | Startseite |
| 20 | ZF-Spülung ab 299 €, BMW 8HP ab 450 €, Übersichtskarte ab 300 € | bestätigt | jeweilige Seiten |
| 21 | 9G-Tronic "ab 550 €" stamme aus alten Suchtreffern | falsch | steht heute auf /angebote/automatikgetriebespuelung-mercedes-9g-tronic (Befund 13) |
| 22 | Kopfmenü nur "Leistungen & Preise", "Über uns", "Kontakt" | bestätigt | Header-Quelltext |
| 23 | Hauptüberschrift Spülungs-Seite "Getriebespülung & Wartung"; 30 von 34 Bildern ohne Beschreibung; keine Links zu den Ratgebern | bestätigt | 34 img, 30 mit alt=""; nur Link auf /ratgeber (Übersicht) |
| 24 | Karte "Meister-Wartung ab 1.899 €", Preis gehört zum Steuerkettenwechsel | bestätigt | Tabelle "1.899 € Steuerkettenwechsel N47 / B47" |
| 25 | Hauptknopf einiger Angebote führt zu Kleinanzeigen | bestätigt | "Zum Kleinanzeigen-Inserat" vor "Termin anfragen" |
| 26 | Shop: doppelte Hauptadresse, "All Products" | bestätigt | /category/all-products: Titel "All Products", zwei canonical-Angaben |
| 27 | Google-Bestätigungscode im Quelltext, kein Statistik-Code, Schriften von Google-Servern | bestätigt | google-site-verification vorhanden; kein gtag/GTM; fonts.googleapis.com und fonts.gstatic.com |
| 28 | Firmendaten-Typen im Quelltext (AutoRepair, FAQ, WebSite) | bestätigt | Startseite: AutoRepair, LocalBusiness, WebSite, FAQPage mit 6 Fragen |
| 29 | ZF: "Zertifizierter ZF-Partner", "ZF [pro]Tech Partner" neben "ZF Service Point"; kein Link zu ZF | bestätigt | alle drei Schreibweisen gefunden; ZF-Seite ohne Link auf aftermarket.zf.com |
| 30 | DPF/AGR-Angebot, AdBlue "Reparatur / Software", AGB mit Regeln zur DPF-Entfernung | bestätigt, im Bericht zu schwach | siehe Befund 4 |
| 31 | getriebespuelung-bochum.de: anderer Name, "Sa nach Vereinbarung", nennt OZ nicht | bestätigt | Titel "Getriebespülung Bochum …", 0 Treffer "OZ Performance", "Sa nach Vereinbarung" |
| 32 | getriebe-bochum.com zeigt "nicht gefunden" | bestätigt | HTTP 404 |
| 33 | /fehlercodes/… existiert noch nicht; /standorte/hattingen fehlt | bestätigt | 404 |
| 34 | "Eure zwei bestehenden Weiterleitungen zeigen, dass es [im Wix-Dashboard] funktioniert" | falsch | siehe Befund 2 |
| 35 | Wortzahlen (495, 320, 289 …), "35 Seiten", "73-mal", "243-mal" | nicht nachgezählt | Größenordnung plausibel, Zählmethode des Audits nicht reproduziert |

---

## Befunde

### Kritisch

**1. kritisch – Die Kernbehauptung zur P1735-Lücke widerspricht den eigenen Quellen des Berichts**

- Passagen: "Die einzige deutsche Seite, die genau diesen Code behandelt, erklärt ihn falsch (als General-Motors-Fehler)" (Zusammenfassung). "Die einzige deutsche Seite, die exakt auf den Code zielt, beschreibt ihn als General-Motors-Code für ein Schaltventil … Die richtige Erklärung steht auf englischen Seiten und verstreut in Foren." (Bauplan). "wo die deutsche Konkurrenz dünn und teils falsch ist" (Fazit).
- Fehler: Der Bericht verlinkt im selben Abschnitt mehrere deutsche Seiten, die genau diesen Code im Titel oder in der Adresse tragen und ihn richtig erklären: kfz-reparatur24.de/leistungen/p1735-p1736-dsg-reparatur/, motronik-service.de/…/p1735-p1736-positionsgeber-kupplung-1-2-elektrischer-fehler/, repairfirst.de/pages/fehlercodes/getriebe0129-p1735-dq381, ecu.de. Autodoc ist also nicht "die einzige".
- Beleg: technik_p1735_getriebespuelung.md, Abschnitt 1 und 2 (zusätzlich dias-automotive-engineering.com "…fehler-p1735-p1736-10666-10668-beheben", compramas-shop.de, Kleinanzeigen-Angebot Hanau). Die Aussage stammt aus serp_wettbewerb.md Abschnitt 5, dort aber mit Vorbehalt: "Whether a German competitor page for P1735 exists that the US-biased index did not return: unverified." Der Bericht hat den Vorbehalt gestrichen und die widersprechende Technik-Notiz nicht berücksichtigt.
- Folge: Der Inhaber plant mit einer leeren Nische. Tatsächlich stehen ihm mindestens vier bis sechs deutsche Reparaturanbieter mit eigener Codeseite und Preisen (299 €, ab 339 €) gegenüber. Die Erwartung "Seite 1 in 4 bis 12 Wochen" ruht mit auf dieser Annahme.
- Korrektur: "Das große deutsche Nachschlageportal (Autodoc) erklärt den Code falsch. Richtig erklären ihn mehrere deutsche Einsende-Reparaturbetriebe (kfz-reparatur24, motronik-service, repairfirst, ecu.de) auf eigenen Codeseiten, allerdings knapp, ohne Werkstattfall und ohne erklärten Komplettpreis. Die Lücke ist nicht 'niemand erklärt es', sondern 'niemand zeigt Diagnose, Fall und Komplettpreis einer Werkstatt vor Ort'. Wer bei google.de tatsächlich vorn steht, ist ungeprüft." Zusammenfassung, Bauplan, Zeitschätzung und Fazit entsprechend abschwächen.

**2. kritisch – Der wichtigste erste Schritt (Weiterleitungen) stützt sich auf einen falschen Beweis**

- Passagen: "Das geht im Wix-Dashboard, auch als Tabellen-Import mit bis zu 500 Zeilen. Eure zwei bestehenden Weiterleitungen zeigen, dass es bei diesem Projekt funktioniert". "Die Weiterleitungen und den Anschluss der Search Console erledigt ihr selbst im Wix-Dashboard".
- Fehler: Die zwei bestehenden Weiterleitungen sind keine Dashboard-Einträge. /preise und /preisrechner sind programmierte Seiten des Projekts, die selbst weiterleiten. Sie beweisen nichts über die Weiterleitungsverwaltung im Dashboard. Ob diese bei einem Wix-Headless-Projekt auf Astro überhaupt greift, ist damit offen. Unklar ist auch, ob ein Dashboard-Eintrag für /leistungen/getriebeinstandsetzung wirkt, weil diese Adresse in die programmierte Vorlage /leistungen/[slug] fällt.
- Beleg live: https://www.ozperformance.de/_wix/pages.json führt `{"path":"/preise","srcFilePath":"/src/pages/preise/index.astro","static":true}` und `{"path":"/preisrechner","srcFilePath":"/src/pages/preisrechner.astro","static":true}`. Genau deshalb stehen beide auch in der Sitemap. Die Notiz website_audit.md Abschnitt 8 ("so the mechanism works on this project") hat denselben Fehlschluss; die Wix-Hilfeartikel dort beschreiben klassische Wix-Websites.
- Korrektur: "Zuerst eine einzige Weiterleitung im Wix-Dashboard anlegen (etwa /softwareoptimierung nach /leistungen/software-optimierung) und im privaten Fenster prüfen, ob sie greift. Greift sie, den Rest als Tabelle importieren. Greift sie nicht, trägt die Person, die den Code pflegt, die Weiterleitungen im Projekt ein, so wie /preise und /preisrechner heute schon gelöst sind." Den Satz "erledigt ihr selbst im Wix-Dashboard" streichen und die Zeile in Fahrplan und Tabelle "Firmendaten bereinigen" anpassen.

### Wichtig

**3. wichtig – Preis für die P1735-Reparatur: Der Bericht übersieht den Komplettpreis von 1.200 €, der schon auf der Website steht**

- Passagen: "Euer Preis 'ab 400 €' steht schon auf der Angebotsseite. Schreibt dazu, was er enthält (Aus- und Einbau, Öl, Grundeinstellung) und wo er endet." "Ein erklärter Komplettpreis wäre der erste belastbare im deutschen Netz." Fahrplan: "Preis ab 400 €". Google-Profil: "Drucksensor-Reparatur DQ381/DQ500 ab 400 €". Checkliste: "ihr Umfang … nicht geprüft".
- Fehler: Die Website trennt bereits zwei Preise. Auf /leistungen/mechatronik-reparatur steht: "400 € Steuergerät-Reparatur … Mechatronik ausgebaut anliefern oder per Post" und "1.200 € Komplettpaket schlüsselfertig: Aus- und Einbau der Mechatronik, Reparatur des Getriebesteuergeräts, Grundeinstellung und Adaptionsfahrt, Getriebeölwechsel + digitaler Serviceeintrag". Die zweite DQ381/DQ500-Angebotsseite nennt "ab 1.200 € … Komplettlösung inklusive Ölwechsel". Der Bericht legt dagegen nahe, die 400 € könnten Aus- und Einbau enthalten.
- Beleg live: https://www.ozperformance.de/leistungen/mechatronik-reparatur, https://www.ozperformance.de/angebote/getriebesteuergeraet-reparatur-dq381-dq500. In website_audit.md fehlt die 1.200-€-Angabe.
- Risiko: Eine Codeseite und ein Google-Profil mit "ab 400 €" ohne den Zusatz "ausgebaut angeliefert" wecken beim Kunden mit Auto vor der Tür eine falsche Preiserwartung, und KI-Antworten übernehmen genau diese Zahl.
- Korrektur: In Bauplan, Fahrplan und Profil-Liste beide Preise nennen: "ab 400 € bei angelieferter oder eingeschickter Mechatronik, 1.200 € als Komplettpaket mit Aus- und Einbau, Grundeinstellung und Ölwechsel (bitte bestätigen)". Den Satz zum "ersten Komplettpreis" ändern in: "Der Komplettpreis steht schon auf der Mechatronik-Seite; er gehört sichtbar auf die Codeseite."

**4. wichtig – DPF/AGR und AdBlue: Befund zu schwach beschrieben, Termin widersprüchlich**

- Passagen: "die AGB enthalten Regeln zur Entfernung von Partikelfiltern … Das Audit hält solche Formulierungen für rechtlich heikel … Lasst diese Texte als Erstes prüfen." Fahrplan: dieselbe Prüfung erst "Bis Tag 30".
- Fehler: (a) "Als Erstes" und "Bis Tag 30" widersprechen sich. (b) Es geht nicht nur um Formulierungen. Die AGB beschreiben eine Leistung: "3a. DPF-Ausbau und Leeren des Partikelfilters. Beim DPF-Ausbauservice (z. B. 'DPF + AGR Sorglospaket') wird der Dieselpartikelfilter ausgebaut und geleert bzw. entfernt. Das Entfernen oder Leeren … ist für Fahrzeuge im öffentlichen Straßenverkehr nicht erlaubt. Die Betriebserlaubnis des Fahrzeugs erlischt … Wir führen diese Leistung ausschließlich für Motorsportzwecke durch." Die Angebotsseite bewirbt dasselbe Paket ohne diese Einschränkung für "Diesel-Fahrzeuge aller Marken" mit "passende[r] Softwarelösung", ab 450 €.
- Beleg live: https://www.ozperformance.de/agb, https://www.ozperformance.de/angebote/dpf-agr-sorglospaket. Notiz offpage_marke_recht.md Abschnitt 8 rät, solche Eingriffe "not advertise … at all".
- Korrektur: Sachverhalt im Bericht wörtlich benennen (AGB-Ziffer 3a, Widerspruch zur Angebotsseite), die anwaltliche Prüfung in die Zeile "Woche 1 bis 2" ziehen und empfehlen, die beiden Angebotsseiten bis zur Prüfung aus Menü, Sitemap und Google-Profil herauszuhalten. Weiterhin als Orientierung, nicht als Rechtsberatung kennzeichnen.

**5. wichtig – Keine Zuordnung alt nach neu; eine Altadresse hat gar keine Entsprechung**

- Passage: "Jede alte Adresse dauerhaft auf ihre neue Entsprechung weiterleiten". "mindestens /getriebeinstandsetzung, /leistungen/getriebeinstandsetzung, /softwareoptimierung und die übrigen Altadressen aus dem Suchindex".
- Fehler: Der Inhaber erfährt nicht, wohin. Für /motorinstandsetzung gibt es auf der neuen Website keine Entsprechung; wer sie pauschal auf die Startseite leitet, erzeugt eine Weiterleitung, die Google wie eine Fehlerseite behandelt. /leistungen/softwareoptimierung (laut serp_wettbewerb.md im Index) fehlt in der Liste. Alle genannten Altadressen sind inzwischen live geprüft (Stichprobe 3), der Hinweis "nicht einzeln live geprüft" kann entfallen.
- Korrektur: Tabelle einfügen:
  - /getriebeinstandsetzung, /leistungen/getriebeinstandsetzung → /leistungen/getriebe-instandsetzung
  - /softwareoptimierung, /leistungen/softwareoptimierung → /leistungen/software-optimierung
  - /getriebe, /getriebespuelung, /leistungen/getriebespuelung → /leistungen/automatikgetriebe-spuelung
  - /agbs → /agb
  - /motorinstandsetzung → nur weiterleiten, wenn es eine inhaltlich passende Seite gibt (am ehesten /leistungen/meister-wartung, falls Motorarbeiten weiter angeboten werden); sonst bewusst als "nicht gefunden" belassen.
  - Jeweils auch die Schreibweise mit Schrägstrich am Ende testen.

**6. wichtig – Die P1735-Seite soll online gehen, bevor der Meister den Inhalt bestätigt hat**

- Passagen: Fahrplan "Woche 1 bis 2: Seite P1735/P1736 … anlegen und veröffentlichen: Kurzantwort, Faktentabelle …", aber erst "Bis Tag 30: … Original-Fehlertext, … Prüfvermerk des Meisters." Dagegen im Bauplan: "eine fachliche Klarstellung, die ihr als Meisterbetrieb bestätigen müsst", und in der Analyse: Google verlange, "KI-Texte vor Veröffentlichung von Menschen auf Fakten prüfen zu lassen".
- Fehler: Der Plan widerspricht der eigenen Regel. Die Codebedeutung ist laut technik_p1735_getriebespuelung.md nur aus Anbieterquellen belegt ("Offizieller ODIS-/VCDS-Wortlaut im Original nicht verifiziert … **prüfen**"). Zwei bis vier Wochen stünde eine ungeprüfte Fachseite mit Aussage zum Weiterfahren online.
- Korrektur: In die Zeile "Woche 1 bis 2" aufnehmen: "Vor der Veröffentlichung liest der Meister Bedeutung, betroffene Getriebe und die Aussage zum Weiterfahren gegen und gleicht den Fehlertext mit dem eigenen Diagnosegerät ab. Der Prüfvermerk steht ab dem ersten Tag auf der Seite." Fotos, Video und ausführlicher Fall dürfen bis Tag 30 folgen.

**7. wichtig – Seitenzahlen im Fahrplan passen nicht zusammen und überfordern einen kleinen Betrieb**

- Passagen: "Startet mit 15 bis 30 Seiten … und ergänzt 5 bis 10 pro Monat." Fahrplan: Woche 1 bis 2 eine Seite, "Tag 31 bis 60: 8 bis 10 weitere", "Tag 61 bis 90: Auf 20 bis 30 Fachseiten ausbauen", "Laufend: 5 bis 10 neue Seiten pro Monat".
- Fehler: Nach Tag 60 stehen höchstens 11 Seiten. Der Sprung auf 20 bis 30 bis Tag 90 verlangt 9 bis 19 Seiten in einem Monat, mehr als das eigene Tempo "5 bis 10 pro Monat" und genau das Serienmuster, vor dem der Bericht warnt. Die Notiz google_seo_content.md nennt 15 bis 30 als Startbestand "for codes with real cases", nicht als 90-Tage-Ziel.
- Korrektur: Eine Zahlenreihe festlegen, etwa: Tag 30 eine Seite, Tag 60 sechs bis acht, Tag 90 zehn bis fünfzehn, danach drei bis fünf pro Monat, jede nur mit eigenem Fall. Den Satz "Startet mit 15 bis 30 Seiten" streichen oder als Zielbild nach etwa sechs Monaten kennzeichnen.

**8. wichtig – Herstellerintervalle sicherer dargestellt als belegt; Widerspruch zum eigenen Ratgeber der Website fehlt**

- Passage (Bauplan Getriebespülung, "Was sagen die Hersteller?"): "VW: DQ250 alle 60.000 km, DQ381 120.000 km, DQ200 kein planmäßiger Wechsel."
- Fehler: (a) Quelle ist auto motor und sport, kein VW-Dokument. Die Notiz stuft DQ381 nur als "mittel" ein, nennt eine widersprechende Quelle mit 60.000 km und hält fest: "VW-Originalwartungstabelle … nicht belegt". Unter der Überschrift "Was sagen die Hersteller?" liest der Inhaber das als VW-Vorgabe. (b) Das ZF-Datenblatt mit 150.000 km ist von 2017, die 80.000-bis-120.000-km-Angabe wurde nur als Forenanhang von etwa 2019 gesehen. (c) Der eigene Ratgeber der Website empfiehlt pauschal "alle 60.000 bis 80.000 Kilometer" für Automatik und DSG. Übernimmt der Inhaber die Tabellenzeile, stehen auf seiner Website zwei verschiedene Intervalle, ohne dass der Bericht das anspricht.
- Beleg: technik_p1735_getriebespuelung.md Abschnitt 6 (Cited Findings und Gaps); live https://www.ozperformance.de/ratgeber/getriebeoel-wechseln-intervall-kosten.
- Korrektur: "Laut Fachpresse (nicht aus VW-Unterlagen geprüft): DQ250 alle 60.000 km, DQ381 meist 120.000 km, einzelne Quellen nennen 60.000 km; DQ200 ohne planmäßigen Wechsel. Vor Veröffentlichung gegen eure Herstellerunterlagen prüfen." Zusatz: "Herstellervorgabe und eure eigene Empfehlung (60.000 bis 80.000 km im Ratgeber) getrennt ausweisen und begründen."

**9. wichtig – Preisvergleich bei der Spülung ist einseitig**

- Passage: "Euer stärkster Aufhänger bleibt der Preis. Freie Spezialisten verlangen 2026 belegt etwa 620 bis 820 € für ein ZF 8HP und 490 bis 590 € für eine 7G-Tronic … Euer 'ab 450 €' für das BMW 8HP liegt darunter."
- Fehler: Die Notiz enthält auch einen günstigeren Wettbewerber mit demselben Gütesiegel: "Wildemann Getriebetechnik (ZF Service Point): Spülung ZF 6HP/8HP 'ab 350 €'" sowie Ratgeberspannen ab 300 €. Verglichen wird außerdem ein "ab"-Preis mit Komplettpreisen inklusive Ölwanne und Filter. Regionale Preise im Ruhrgebiet wurden nicht erhoben.
- Beleg: technik_p1735_getriebespuelung.md Abschnitt 8 (Cited Findings; Gaps: "Regionale Preise Ruhrgebiet/Bochum: nicht erhoben").
- Korrektur: "Belegte Angebote freier Spezialisten reichen von 'ab 350 €' (ein anderer ZF Service Point) bis 820 € für ein ZF 8HP. Euer 'ab 450 €' liegt im unteren Bereich. Ob es ein Preisvorteil ist, entscheidet der Leistungsumfang. Preise aus dem Ruhrgebiet fehlen." "Stärkster Aufhänger" streichen.

**10. wichtig – Kundenfall, Fotos und Videos ohne Hinweis auf Einwilligung und Anonymisierung**

- Passagen: "Der Tiguan-Fall mit P1736 aus der Rezension vom April 2026: Baujahr, Laufleistung, Beschwerde, Befund, Reparatur, Ergebnis, Fotos." "Ein 'Fall der Woche' mit Fahrzeug, Getriebe und Code im Titel". "ein realer Kundenfall von dort" (Stadtseiten).
- Fehler: Der Fall soll mit einer namentlich gezeichneten Rezension (Klaus W.) verknüpft und um Daten aus der Werkstattakte ergänzt werden. Dafür fehlt jeder Vorbehalt. Die Notiz verlangt ausdrücklich einen "anonymised real workshop case" (google_seo_content.md Abschnitt 2), und für Antworten auf Rezensionen nennt der Bericht selbst "ohne Kundendaten".
- Korrektur: Ergänzen: "Fälle anonymisiert veröffentlichen (kein Name, kein Kennzeichen, keine Fahrgestellnummer auf Fotos und in Videos) oder vorher die schriftliche Einwilligung des Kunden einholen. Auftragsdaten nicht mit einer namentlichen Rezension verknüpfen, wenn der Kunde nicht zugestimmt hat." In die Liste der anwaltlichen Prüfpunkte aufnehmen.

**11. wichtig – Hauptkategorie im Google-Profil: "wichtigste Einzelentscheidung", aber keine Entscheidungsregel**

- Passagen: "Die wichtigste Einzelentscheidung ist die Hauptkategorie … Steht bei euch 'Auto-Tuning-Werkstatt' vorn, arbeitet das gegen eure Getriebe-Anfragen. Ändert die Hauptkategorie einzeln und beobachtet zwei bis vier Wochen."
- Fehler: Der Bericht sagt nicht, auf welche Kategorie geändert werden soll. Die Notiz hat die Regel: Tragen die drei Kartenbetriebe für "Getriebespülung Bochum" die Getriebe-Kategorie, dann diese, sonst "Autowerkstatt" als Hauptkategorie und die Getriebe-Kategorie als erste Zusatzkategorie. Sie warnt zudem, "Getriebe-Fachhandel" sei eine Handelskategorie. Die Aussage zur Tuning-Kategorie ist in der Notiz eine Vermutung ("may be", "if so"), im Bericht eine Tatsache.
- Beleg: local_seo_bewertungen.md Abschnitt 4 Inferences und Abschnitt 1 Inferences; serp_wettbewerb.md Abschnitt 1 Inferences.
- Korrektur: Entscheidungsregel aus der Notiz in einem Satz übernehmen, "arbeitet das vermutlich gegen" schreiben und erklären, wo man die Kategorie eines Wettbewerbers sieht (in Google Maps unter dem Firmennamen).

### Klein

**12. klein – Falsche Aussage zu Modellnamen auf der eigenen Website**

- Passage: "Nirgends stehen Modellnamen wie Golf oder Tiguan im Zusammenhang mit dem Code".
- Live: /leistungen/mechatronik-reparatur führt im DQ381/DQ500-Block "Fahrzeuge: VW Golf 7, Tiguan, Tiguan Allspace, T-Roc, Touran, Arteon, Passat, …" direkt neben "Fehlercodes P1735 / P1736". Die Tiguan-Rezension mit P1736 steht auf allen drei P1735-Seiten. Die Seite erklärt auch schon, warum der Text "Positionsgeber" lautet ("Die Kupplungsposition wird aus den Drucksensoren im Getriebesteuergerät berechnet").
- Korrektur: "Modellnamen stehen bisher nur in einer Liste auf der Mechatronik-Seite, nicht in Titel, Überschrift oder Kurzantwort." Im Bauplan vermerken, dass die Positionsgeber-Erklärung von der Mechatronik-Seite übernommen werden kann.

**13. klein – Preisangaben: "ab 550 €" ist kein Altbestand; Profil-Liste greift der Preisentscheidung vor**

- Passagen: "die alten Suchtreffer zeigten noch 'ab 249 €' und für die 9G-Tronic 'ab 550 €'." und "Automatikgetriebe-Spülung ab 300 €" in der Liste für das Google-Profil.
- Live: Die 9G-Tronic-Angebotsseite nennt heute "ab 550 €". "249 €" kommt sichtbar nirgends mehr vor. Die Profil-Liste schreibt "ab 300 €" fest, obwohl der Bericht zwei Absätze vorher verlangt, erst zwischen 299 und 300 € zu entscheiden.
- Korrektur: "Alt war nur 'ab 249 €'. Die 9G-Tronic steht aktuell bei 'ab 550 €'." In der Profil-Liste: "Spülung zum vereinheitlichten Preis (299 oder 300 €)".

**14. klein – "Kein Suchroboter ist ausgesperrt" stimmt nicht wörtlich**

- Live: robots.txt enthält `User-agent: PetalBot / Disallow: /` (Suchroboter von Huawei) und eine Wartezeit für AhrefsBot und dotbot. Für Deutschland ohne Bedeutung.
- Korrektur: "Keiner der wichtigen Suchroboter (Google, Bing) und keiner der KI-Anbieter ist ausgesperrt."

**15. klein – Zählfehler und Reihenfolge im Fahrplan**

- Passage: "Die ersten fünf Zeilen sind die Reparatur des Neubaus und haben Vorrang vor allem anderen."
- Fehler: Der Block "Woche 1 bis 2" hat acht Zeilen; Zeile vier ist die neue P1735-Seite, also keine Reparatur. Zeile eins (Weiterleitungen) braucht die Adressliste aus der Search Console, die erst Zeile drei anschließt. Zeile fünf verlinkt die Stadtseiten stärker, obwohl der Bericht sie als "nah an Brückenseiten" einstuft und erst an Tag 31 bis 60 bereinigt.
- Korrektur: Reihenfolge: Search Console anschließen, Weiterleitungen, Sitemap, Verlinkung (ohne Stadtseiten, bis diese überarbeitet sind), dann die neue Seite. "Die ersten vier Zeilen" schreiben.

**16. klein – Erwartung an die Weiterleitungen zu glatt; Search-Console-Aussage zu absolut**

- Passagen: "Suchtreffer: lösen die Weiterleitungen", "Verschwindet mit den Weiterleitungen", "Niemand sieht derzeit, welche der 62 Seiten im Index stehen".
- Fehler: /preise ist bereits weitergeleitet und stand laut Audit am 25.11.2026 trotzdem noch mit dem Titel "OZ Performance UG … Preise" im Suchindex. Das Umschreiben dauert Wochen. Den Bestätigungscode hat irgendein Google-Konto gesetzt (website_audit.md: "property appears to be verified via meta tag by some Google account"); dieses Konto kann die Daten sehr wohl sehen.
- Korrektur: "verschwinden nach den Weiterleitungen innerhalb einiger Wochen". "Über Wix sieht derzeit niemand …; findet sich das Google-Konto nicht, die Website in der Search Console neu bestätigen."

**17. klein – Studien ohne die Einschränkungen der Notizen zitiert**

Jeweils Passage, fehlende Einschränkung laut ki_suche_geo.md und google_seo_content.md, Korrektur:
- "erhält laut Seer Interactive rund 120 % mehr Klicks": Seer nennt Ursache und Wirkung ausdrücklich unbewiesen; zitierte Seiten liegen weiter 38 % unter Suchen ohne KI-Antwort. Halbsatz ergänzen.
- "die bislang größte Studie (AirOps …)": "größte" steht in keiner Notiz. Streichen.
- "Riesenratgeber über 5.000 Wörter am schlechtesten": Die Notiz führt eine widersprechende Studie (längere Seiten erhielten mehr Zitate). "in dieser Studie" ergänzen.
- "Empfohlene Betriebe hatten im Schnitt 4,1 bis 4,3 Sterne": Gemini 3,9; Daten betreffen US-Filialketten. Ergänzen.
- "Schema-Markup … keinen messbaren Effekt auf KI-Zitate" (Zusammenfassung): Der Test umfasste nur Seiten, die schon über 100 Zitate hatten. "in einem Test an bereits zitierten Seiten".
- "Seit Oktober 2026 verlangt Google zudem …": laut Notiz nur über Branchenpresse berichtet ("reportedly"). "laut Branchenpresse".
- "von 76 % auf rund 38 % gefallen": laut Notiz teils Methodenwechsel. Halbsatz ergänzen.
- "Größter Fahrzeugbestand, bekannter Serienfehler" (Rangliste, Rang 1): in serp_wettbewerb.md als Schätzung markiert. "vermutlich".
- "Einsendepreise von 299 €": Die Notiz sagt nur "Steuergerätereparatur: 299 € bei einem Anbieter". "Reparaturpreise".
- Modelltabelle "Golf 7 und 8" mit Quelle kfz-reparatur24: Golf 8 stammt laut Notiz von repairfirst. Zweite Quelle angeben. Die eigene Website und ACtronics nennen zusätzlich das DQ380; in Überschrift und Faktentabelle erwähnen oder bewusst weglassen.

**18. klein – Zweit-Domains: Wo die Weiterleitung eingerichtet wird, fehlt**

- Passage: "Gehört sie euch, leitet ihr sie am besten Seite für Seite auf die passenden Seiten der Hauptdomain weiter."
- Fehler: getriebespuelung-bochum.de ist laut Audit keine Wix-Website ("separate small PHP/nginx site"). Die Weiterleitung muss beim dortigen Anbieter eingerichtet werden, nicht im Wix-Dashboard. Für die Unterseiten Dortmund und Essen fehlt das Ziel, falls die Stadtseiten reduziert werden.
- Korrektur: Einen Satz ergänzen: "Einzurichten beim Anbieter, bei dem diese Website liegt. Dortmund- und Essen-Seite auf die Spülungs-Seite leiten, nicht auf Stadtseiten, die später wegfallen könnten."

**19. klein – Sprache und Fachwörter für einen Laien**

- "Wix Headless mit dem Baukasten Astro": zwei Sätze zuvor heißt es "keine klassische Wix-Baukasten-Seite mehr". Dasselbe Wort für Gegensätzliches. Besser: "mit dem Programmiergerüst Astro".
- "62 auffindbare Seiten": gemeint ist "für Suchmaschinen zugelassen". Da der Befund gerade lautet, dass 43 davon schwer zu finden sind, ist "auffindbar" missverständlich. Besser: "62 Seiten, die in den Suchindex dürfen".
- "FAQ-Sterne und FAQ-Kästen im Suchergebnis": "FAQ-Sterne" gibt es nicht. Besser: "FAQ-Kästen und eigene Bewertungssterne im Suchergebnis".
- "Brückenseiten" steht in der Tabelle "Firmendaten bereinigen", erklärt wird das Wort erst drei Abschnitte später. Erklärung an die erste Stelle ziehen.
- Unerklärt bleiben "Suchindex/Index" (trägt den ganzen ersten Teil), "Markup-Test", "Korrelation etwa 0,74" und "301". Je ein Halbsatz genügt, etwa: "Korrelation: 1 wäre ein vollständiger Gleichlauf, 0 gar keiner".
- Der empfohlene Seitentitel "P1735 / P1736 (P173500) VW-DSG: Bedeutung, Ursache, Kosten | OZ Performance" hat rund 75 Zeichen; das Audit bemängelt Titel über 60 Zeichen. Kürzen oder den Hinweis geben, dass Google das Ende abschneidet.

---

## Nachprüfung

**Urteil: freigegeben.** Alle 19 Befunde sind behoben. Die Korrekturen haben keinen neuen kritischen oder wichtigen Fehler erzeugt. Drei kleine Punkte sind neu; sie halten den Versand nicht auf, die ersten beiden sollten aber noch mit je einem Halbsatz bereinigt werden.

Geprüft am 25.11.2026: korrigierter Bericht vollständig neu gelesen (296 Zeilen), 23 weitere Live-Abrufe (nur lesend, 1 s Pause). Fremde Websites waren weiterhin nicht erreichbar.

### Stand der 19 Befunde

| # | Befund | Stand | Beleg im korrigierten Bericht |
|---|---|---|---|
| 1 | P1735 "einzige deutsche Seite" | behoben | Zusammenfassung, Bauplan, Zeitplan-Hinweis und Fazit nennen jetzt die deutschen Anbieterseiten und "im günstigen Fall"; siehe aber neuen Punkt N2 |
| 2 | Weiterleitungen im Dashboard, falscher Beweis | behoben | Test einer einzelnen Weiterleitung zuerst, sonst im Code; /preise und /preisrechner als programmierte Seiten benannt; Hinweis zu /leistungen/getriebeinstandsetzung |
| 3 | 400 € und 1.200 € | behoben | Bestandsaufnahme, Bauplan, Google-Profil, Fahrplan und Checkliste nennen beide Preise gleich |
| 4 | DPF/AGR | behoben | Sachverhalt wörtlich, Prüfung in Woche 1 bis 2, im Text und im Fahrplan gleich |
| 5 | Zuordnung alt nach neu | behoben | Tabelle vorhanden, live geprüft (unten) |
| 6 | P1735-Seite vor Meisterprüfung | behoben | Prüfung vor Veröffentlichung in der Fahrplanzeile und in der Checkliste |
| 7 | Seitenzahlen | behoben | 1 / 6 bis 8 / 10 bis 15 / danach 3 bis 5 pro Monat, an allen vier Stellen gleich; "15 bis 30" als Zielbild nach sechs Monaten rechnerisch stimmig |
| 8 | Herstellerintervalle | behoben | Quelle und Unsicherheit genannt, Widerspruch zum eigenen Ratgeber angesprochen |
| 9 | Preisvergleich Spülung | behoben | "ab 350 €" des anderen Service Points aufgenommen, "stärkster Aufhänger" gestrichen |
| 10 | Einwilligung und Anonymisierung | behoben | Bauplan, Regeln, Stadtseiten, YouTube, Rechtsabschnitt, Checkliste |
| 11 | Hauptkategorie | behoben | Entscheidungsregel und Fundort in Google Maps ergänzt, "vermutlich" |
| 12 | Modellnamen | behoben | |
| 13 | 9G-Tronic-Preis, Profil-Liste | behoben | |
| 14 | PetalBot | behoben | |
| 15 | Zählung und Reihenfolge | behoben | Search Console steht vor den Weiterleitungen; "die ersten vier Zeilen" stimmt; Stadtseiten zurückgestellt |
| 16 | Wirkung der Weiterleitungen, Search Console | behoben | |
| 17 | Studien-Einschränkungen | behoben | alle zehn Unterpunkte umgesetzt |
| 18 | Zweit-Domain | behoben | |
| 19 | Sprache | behoben | neuer Seitentitel hat 56 Zeichen (nachgezählt) |

### Live-Prüfung der neuen Zuordnungstabelle

| Adresse | Status | Bewertung |
|---|---|---|
| /getriebeinstandsetzung, /leistungen/getriebeinstandsetzung | 404 | wie im Bericht |
| /softwareoptimierung, /leistungen/softwareoptimierung | 404 | wie im Bericht |
| /getriebe, /getriebespuelung, /leistungen/getriebespuelung | 404 | wie im Bericht |
| /agbs | 404 | wie im Bericht |
| /motorinstandsetzung | 404 | wie im Bericht |
| dieselben mit Schrägstrich am Ende (vier getestet) | 301 auf die Fassung ohne Schrägstrich, dann 404 | deckt sich mit dem Hinweis "auch mit Schrägstrich testen" |
| Ziel /leistungen/getriebe-instandsetzung | 200 | in Ordnung |
| Ziel /leistungen/software-optimierung | 200 | in Ordnung |
| Ziel /leistungen/automatikgetriebe-spuelung | 200 | in Ordnung |
| Ziel /agb | 200 | in Ordnung |
| Ziel /leistungen/meister-wartung | 200 | in Ordnung, siehe N3 |
| /_wix/pages.json (neu als Beleg verlinkt) | 200 | /preise und /preisrechner dort weiter als programmierte Seiten geführt |

Weitere neu eingefügte Aussagen, live bestätigt: AGB-Absatz 3a steht im achten Abschnitt "Hausregeln für Softwarearbeiten, Tuning, Sonderfunktionen, DPF-Ausbau und Umbauten", die Zitate stimmen wörtlich; Angebotsübersicht führt "DPF/AGR Sorglospaket ab 450 €" und "AdBlue Reparatur / Software"; 400 € "ausgebaut anliefern oder per Post" und 1.200 € Komplettpaket auf der Mechatronik-Seite; Fahrzeugliste und Positionsgeber-Erklärung dort vorhanden.

Zusammenfassung und Fazit decken sich mit dem Hauptteil (Reihenfolge der ersten zwei Wochen, P1735-Einschätzung, Zeitangaben, kein Rangversprechen).

### Neu (alle klein)

**N1. klein – Sitemap-Zeile im Fahrplan widerspricht der DPF-Zeile**

- Passage: "Sitemap im Code reparieren: alle Leistungs-, Angebots-, Ratgeber-, Stadt- und Produktseiten aufnehmen" gegenüber zwei Zeilen darunter "Bis dahin beide Seiten aus Angebotsübersicht, Sitemap und Google-Profil heraushalten".
- Korrektur: in der Sitemap-Zeile ergänzen "außer den beiden Angeboten DPF/AGR und AdBlue, solange die Prüfung läuft".

**N2. klein – Beschreibung der deutschen Anbieterseiten ist nicht belegt (Formulierung stammt aus meinem eigenen Korrekturvorschlag zu Befund 1)**

- Passagen: "allerdings knapp, ohne Werkstattfall und ohne erklärten Komplettpreis" (Zusammenfassung); "Diese Seiten sind knapp, zeigen keinen Werkstattfall und nennen Preise nur für das eingeschickte Bauteil … 'niemand zeigt Diagnose, Fall und Komplettpreis einer Werkstatt vor Ort'" (Bauplan).
- Fehler: Keine dieser Seiten wurde je vollständig gelesen. technik_p1735_getriebespuelung.md hält fest, dass alle Befunde aus Suchauszügen stammen. Dieselbe Notiz führt außerdem einen deutschen Werkstattfall zum DQ381 (herzdrive.com, "Audi-Praxisfall DQ381/0GC"). "Niemand" ist damit zu absolut. Mein Vorschlag aus der ersten Prüfung war an dieser Stelle selbst zu sicher formuliert.
- Korrektur: "soweit aus den Suchauszügen erkennbar knapp und ohne erklärten Komplettpreis; ein Werkstattfall fand sich nur vereinzelt" und "kaum jemand zeigt" statt "niemand zeigt". Die Seiten vor Veröffentlichung einmal selbst ansehen.

**N3. klein – Hinweis zum Ziel für /motorinstandsetzung**

- Passage: "am ehesten /leistungen/meister-wartung, falls ihr Motorarbeiten weiter anbietet".
- Live: Die Seite behandelt Wartung, Inspektion und BMW-Steuerketten; die Wörter Motorinstandsetzung, Motorreparatur oder Motorüberholung kommen dort nicht vor. Der Bericht macht die Weiterleitung bereits von einer Entscheidung abhängig, deshalb kein Fehler.
- Empfehlung: Halbsatz ergänzen "die Seite erwähnt Motorinstandsetzung bisher nicht; ohne passenden Absatz dort lieber nicht weiterleiten".
