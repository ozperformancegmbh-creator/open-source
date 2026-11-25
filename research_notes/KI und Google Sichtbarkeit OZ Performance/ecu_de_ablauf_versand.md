# ecu.de (Glaubitz GmbH & Co. KG, Zittau): Angebotsstruktur, Auftragsablauf, Versand — Vorbild für einen Einsende-Konfigurator bei OZ Performance (Stand: 25.11.2026)

**Wichtiger Hinweis zur Quellenlage (gilt für alle Abschnitte):**
- **ecu.de konnte NICHT direkt gelesen werden.** Jede URL (Startseite, Unterseiten, PDF-Formulare) lieferte per curl HTTP 403 mit einer ~1,4 MB großen JavaScript-Sicherheitsprüfungs-Seite ("Sicherheitsprüfung, Sie werden weitergeleitet ... Schutzmaßnahme gegen einen laufenden Hackerangriff ... Enable JavaScript and cookies to continue"). Der Body enthält nur Kopf-/Fußnavigation, keinen Inhalt. Ein Playwright-Aufruf und ein Abruf über die Wayback Machine wurden von der Sitzungs-Sicherheitsrichtlinie abgelehnt; die Bot-Sperre wurde nicht umgangen. WebFetch kann ecu.de nicht auflösen.
- **Direkt gelesen (curl, 25.11.2026):** nur (a) Kopf-/Fußnavigation und Impressumszeile der ecu.de-Challenge-Seite, (b) dhl.de-Seiten (Preisübersicht national, Geschäftskunden: Retoure, Kunde werden, Paket, Developer Portal, Partnersysteme, Express "Reparaturen & Rückführungen").
- **Alles andere = Suchmaschinen-Auszüge (WebSearch-Snippets/Zusammenfassungen)** der jeweils verlinkten Seiten. Diese sind mit **[Auszug]** markiert, direkt Gelesenes mit **[direkt]**. Auszüge können veraltet oder unvollständig sein; wörtliche Zitate sind nur so genau wie das Snippet. Vor Übernahme von Preisen/Feldbezeichnungen in einen Live-Konfigurator bitte im Browser gegenprüfen.
- Nicht erreichbar (weder curl noch WebFetch): actronics.de, ecutesting.com, hixa.de, getriebe1.de, dsg-getriebe-reparatur.de, ecu.eu, developer.dhl.com (403), support.wix.com, wix.com, sendcloud.de.

## 1. Katalogstruktur von ecu.de (Marke → Gerätekategorie → Gerätetyp → Teilenummer)

### Takeaway
ecu.de ist ein vierstufiger Katalog: Fahrzeugmarke → Gerätekategorie (z. B. "Getriebesteuergerät / Wählhebel") → Gerätetyp/Getriebefamilie (z. B. "DSG 7-Gang DQ200 (0AM)") → einzelne Teilenummern-Seite; der Haupteinstieg ist eine Teilenummernsuche. Der Preis hängt am Gerätetyp (einheitlicher "Standardbearbeitungspreis" je Typ), nicht an der einzelnen Teilenummer.

### Cited Findings
- Betreiber ist die Glaubitz GmbH & Co. KG, Görlitzer Straße 53, 02763 Zittau; Experten-Hotline 03583 554780 (8–18 Uhr), info@ecu.de; Claim "ecu.de - Prüfung & Reparatur von Fahrzeugelektronik" **[direkt, Fußzeile der Challenge-Seite]** — [ecu.de](https://www.ecu.de/)
- Hauptnavigation: "Auftrag", "FAQ", "Über uns", "Kontakt", "Abholung"; Fußnavigation: "Reparaturprozess", "Versand", "AGBs", "Impressum", "Haftungsausschluss", "Datenschutz", "Sitemap", "Referenzen", "Presse", "Kundenstimmen", "Stellenangebote", "Partner/Links" sowie Info-Landingpages "Reparatur Drosselklappe", "Reparatur Standheizung / Zuheizer", "Reparatur Servolenkung", "ABS-/ ASR-/ ESP-Steuergerät Reparatur", "Motorsteuergerät Reparatur", "Getriebesteuergerät Reparatur", "Tacho / Kombiinstrument Reparatur" **[direkt]** — [ecu.de](https://www.ecu.de/)
- URL-Muster der Katalogebenen (aus Suchtreffern): Marke `/opel-54`; Marke+Kategorie `/vw-(volkswagen)/tacho-display-kombiinstrument-reparatur-3079`; Gerätetyp `/vw-volkswagen/getriebesteuergerät-wählhebel/dsg-7-gang-dq200-(0am)-7722`; Teilenummer `/…/volkswagen-vw-0am300048g-0am927769d-temic-00401065b2-161382.html`; parallel existieren "/t/…"-Varianten derselben Typseiten **[Auszug]** — [Typseite DQ200](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)-7722), [Teilenummernseite](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)/volkswagen-vw-0am300048g-0am927769d-temic-00401065b2-161382.html)
- Teilenummern-Seiten sind nach dem Muster "MARKE + Fahrzeughersteller-Teilenummer(n) + Gerätehersteller + Gerätehersteller-Nummer" betitelt, z. B. "AUDI 02E927770AJ 02E300011CF 02E325025AJ TEMIC 00406177A2" oder "BMW 7541027 Bosch 0260550008 ZF 0501213727" **[Auszug]** — [Audi DQ250](https://ecu.de/audi/getriebe-steuerger%C3%A4t/dsg-6-gang-dq250-%2802e%29/audi-02e927770aj-02e300011cf-02e325025aj-temic-00406177a2-132893.html), [BMW 6HP](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp/bmw-7541027-bosch-0260550008-zf-0501213727-147391.html)
- Kategorien je Marke (Beispiel Opel): ABS/ASR/ESP-Steuergerät, Getriebesteuergerät, Motorsteuergerät, Navigation/Radio/Display, Tacho / Kombiinstrument; weitere Kategorie bei Audi: "Abgasnachbehandlung" (SCR Steuergerät) **[Auszug]** — [Opel](https://ecu.de/opel-54), [Audi SCR](https://ecu.de/t/audi/abgasnachbehandlung/scr-steuerger%C3%A4t-6807)
- Die Hauptnavigation des Katalogs ist eine Teilenummernsuche; ecu.de rät, Teilenummer und Fahrzeugdaten bereitzuhalten, weil ein Steuergerät oft nur über die Teilenummer, nicht über Fahrzeugdaten zuordenbar ist **[Auszug]** — [Steuergeräte reparieren](https://ecu.de/steuergeraete-reparieren-138.htm), [Sie und ecu.de](https://ecu.de/sie-und-ecude-157.htm)
- Markenliste reicht alphabetisch bis u. a. Peugeot, Porsche, Renault, Skoda, Toyota, VW (Volkswagen), Yamaha (auch Motorrad-/Nicht-Pkw-Marken) **[Auszug, Fragment]** — [Steuergeräte reparieren](https://ecu.de/steuergeraete-reparieren-138.htm)
- Datensatz-IDs der Teilenummernseiten liegen im Bereich ~100.000–163.000 (z. B. -102148, -161382, -162987) **[Auszug, aus URLs]** — [Beispiel](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)/volkswagen-vw-0am300043d-0am927769e-a2c73603907-162987.html)

#### Getriebebezogene Einträge (repräsentative Beispiele, alle **[Auszug]**)
Preisdarstellung in den Snippets: zwei Beträge hintereinander, z. B. "446,00 € 375,00 € *" — siehe Inferenz unten (Brutto/Netto).

| # | Typseite (Kategorie "Getriebesteuergerät / Wählhebel") | Beispiel-Teilenummer | Genannte Fehler / Codes | Preis (brutto / netto) | Laufzeit | Quelle |
|---|---|---|---|---|---|---|
| 1 | VW – DSG 7-Gang DQ200 (0AM), Steuergerät-Reparatur | 0AM300048G / 0AM927769D TEMIC 00401065B2 | P1604 (Endstufenfehler Steuergerät) "in der Regel am Steuergerät reparabel" | "ab" 357,00 € / 300,00 € | (nicht im Auszug) | [Link](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)/volkswagen-vw-0am300048g-0am927769d-temic-00401065b2-161382.html) |
| 2 | VW/Audi – DQ200 (0AM), "Überholung Mechatronik" (Hydraulikmodul) | 0AM325025D | P17BF (Hydraulikpumpe, Spielschutz aktiv), P0841, P189C — "können mit einer Überholung des Hydraulikmoduls behoben werden" | 655,00 € / 550,00 € | 3–4 Tage + 2 Tage Versand | [VW](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)/volkswagen-vw-0am325025d-157432.html), [Audi-Typseite](https://ecu.de/t/audi/getriebe-steuerger%C3%A4t/dsg-7-gang-dq200-(0am)-7719) |
| 3 | VW – DQ200 mit 0CW-Nummer (in derselben DQ200-Typgruppe geführt) | 0CW300047T / 0AM927769G TEMIC 00402922B5 | (nicht im Auszug) | wie Typ DQ200 | – | [Link](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)/volkswagen-vw-0cw300047t-0am927769g-temic-00402922b5-160858.html) |
| 4 | VW – DSG 6-Gang DQ250 (02E) | (Typseite) | "keine Kommunikation"; Kundenmeldung P1829, P0776; eine Seite: Reparatur "vorübergehend nicht möglich" | 536,00 € / 450,00 € bzw. 381,00 € / 320,00 € (zwei Leistungsvarianten) | (nicht im Auszug) | [Link](https://ecu.de/t/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-6-gang-dq250-(02e)-3682) |
| 5 | DQ250 – Zusatzleistung "Datenübertragung" | – | Datenübernahme auf anderes Gerät | 226,00 € / 190,00 € | – | [Link](https://ecu.de/t/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-6-gang-dq250-(02e)-3682) |
| 6 | Audi – DQ250 (02E) | 02E927770AJ / 02E300011CF / 02E325025AJ TEMIC 00406177A2 | wie Typ | wie Typ | – | [Link](https://ecu.de/audi/getriebe-steuerger%C3%A4t/dsg-6-gang-dq250-%2802e%29/audi-02e927770aj-02e300011cf-02e325025aj-temic-00406177a2-132893.html) |
| 7 | Skoda – DQ250 (02E) | 02E927770AS / 0D9300042M / 02E325025AS TEMIC 00406611B2 | wie Typ | wie Typ | – | [Link](https://ecu.de/skoda/getriebesteuergerät/dsg-dq250-(02e)/skoda-02e927770as-0d9300042m-02e325025as-temic-00406611b2-130247.html) |
| 8 | VW – DSG 7-Gang DQ381 / DQ500 (0GC / 0DL) Bosch | 0GC325025D | P0805 "Kupplungsstellungs-Sensor Funktion fehlerhaft", P1735, P1736 (Kupplungspositionssensoren); Hinweis: nach Einbau Grundeinstellung mit Diagnosetester nötig | 446,00 € / 375,00 € | 2–3 Tage + 2 Tage Versand | [Typseite](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq381-dq500-%280gc-0dl%29-bosch-6426), [Teilenr.](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq381-dq500-%280gc-0dl%29-bosch/volkswagen-vw-0gc325025d-139400.html) |
| 9 | VW – DSG 7-Gang DQ500 (0BH / 0BT) Continental | 0BT300046G / 0BH927711G Continental 5WP25011AA | Hinweis "ohne Schieberkasten (EHS) einsenden"; nach Einbau Grundeinstellung mit Diagnosetester | 417,00 € / 350,00 € | 3 Tage + 2 Tage Versand | [Link](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq500-%280bh-0bt%29-continental/volkswagen-vw-0bt300046g-0bh927711g-continental-5wp25011aa-138217.html) |
| 10 | Audi – DQ500 (0BH / 0BT) Continental | 0BH300011K / 0BH927711C Continental 5WP25003AC | wie Typ | wie Typ | – | [Link](https://ecu.de/audi/getriebe-steuerger%C3%A4t/dsg-7-gang-dq500-(0bh-0bt)-continental/audi-0bh300011k-0bh927711c-continental-5wp25003ac-158222.html) |
| 11 | Audi – S-Tronic 7-Gang DSG DL501 0B5 | 4G2927156M / 0B5927256F / 0B5927156K TEMIC 2841476112300 | "Pins am Anschlussstecker des Steuergerätes durch Feuchtigkeit beschädigt/zerstört – keine Diagnose möglich"; beim Ausbau abgerissene Stecker | 417,00 € / 350,00 € (eine Seite: 406,00 € für Bj. 2010–2013) | (nicht im Auszug) | [Typseite](https://ecu.de/t/audi/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/s-tronic-7-gang-dsg-dl501-0b5-5990), [Teilenr.](https://ecu.de/audi/getriebesteuerger%C3%A4t/s-tronic-7-gang-dsg-dl501-0b5/audi-4g2927156m-0b5927256f-0b5927156k-temic-2841476112300-140653.html) |
| 12 | Audi – Multitronic (V30) | 01J927156DB TEMIC 00107183A4 | (nicht im Auszug) | 333,00 € / 280,00 € | 4–5 Tage + 2 Tage Versand | [Link](https://ecu.de/audi/getriebe-steuerger%C3%A4t/multitronic-v30/audi-01j927156db-temic-00107183a4-102148.html) |
| 13 | BMW – Steuergerät 6-Gang Automatik ZF 6HP | 7541027 Bosch 0260550008 ZF 0501213727 | Hinweis: "nur wie im Bild dargestellt, dass Getriebesteuergerät OHNE Schieberkasten (EHS) einsenden" | 417,00 € / 350,00 € | 2–3 Tage + 2 Tage Versand | [Typseite](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp-6854), [Teilenr.](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp/bmw-7541027-bosch-0260550008-zf-0501213727-147391.html) |
| 14 | BMW – ZF 6HP (Continental-Variante) | 7319819 Continental 5WK75010AA ZF 6058007112 | wie Typ | wie Typ | – | [Link](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp/bmw-7319819-continental-5wk75010aa-zf-6058007112-148628.html) |
| 15 | Mercedes – VGS / NAG2 7G-Tronic (722.9) | A0002702900; A0335456632 Siemens 5WP21012; A0034460310 Continental 5WP21302 | interner Drehzahlsensor (VGS) und Wählbereichssensor (VGS) defekt (Gutmann-Codes) | 357,00 € / 300,00 € | 1–2 Tage + 2 Tage Versand | [Typseite](https://ecu.de/t/mercedes-steuergeraete-reparatur/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/vgs-nag2-7g-tronic-(722.9)-5150), [Teilenr.](https://ecu.de/mercedes-steuergeraete-reparatur/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/vgs-nag2-7g-tronic-%28722.9%29/mercedes-a0002702900-119026.html) |

- Zu DQ200 und DQ381 gibt es zusätzlich redaktionelle "Technische Information"-Seiten für Werkstätten (z. B. "Demontagehinweis DSG DQ200": Mechatronik vor Ausbau per Diagnosetester in Neutral-/Demontageposition bringen; "Reparatur DQ381 für Audi, Seat, Skoda & VW") **[Auszug]** — [Demontagehinweis DQ200](https://ecu.de/technische-information-demontagehinweis-dsg-dq200-337.htm), [DQ381 Werkstatt-Info](https://ecu.de/dq381---technische-werkstatt-information-303.htm)
- Für das DQ250 bietet ecu.de eine eigene "Spezialverpackung DSG DQ 250" mit 25 EUR Pfand zzgl. Versand und MwSt.; Pfand wird bei Rückgabe erstattet (Versandkosten nicht), kostenlose Abholung der Verpackung über Hotline möglich **[Auszug]** — [Spezialverpackung DQ250](https://ecu.de/abholung/spezialverpackung-dsg-dq-250-221.htm)

### Inferences
- Die doppelte Preisangabe ist sehr wahrscheinlich **Bruttopreis (durchgestrichen/klein) + Nettopreis (hervorgehoben)**, nicht "Listenpreis/Aktionspreis": 300 × 1,19 = 357; 350 × 1,19 = 416,50 ≈ 417; 375 × 1,19 = 446,25 ≈ 446; 450 × 1,19 = 535,50 ≈ 536; 550 × 1,19 = 654,50 ≈ 655; 280 × 1,19 = 333,20 ≈ 333. Die Suchmaschinen-Zusammenfassungen haben das teils als Rabatt fehlgedeutet. ecu.de führt also netto (B2B-Logik) und zeigt brutto daneben.
- Größenordnung des Katalogs: ID-Bereich bis ~163.000 deutet auf eine sechsstellige Zahl an Teilenummern-Datensätzen und Typ-IDs im Bereich bis ~7.700 hin; eine exakte Zahl der Marken/Einträge ist nicht belegt (siehe Gaps).
- ecu.de repariert bei Getrieben überwiegend die **Elektronik (TCU)**, ausdrücklich "ohne Schieberkasten (EHS)"; nur beim DQ200 gibt es zusätzlich die hydraulische "Überholung Mechatronik". Für OZ Performance (Getriebe-Spezialist) ist die Trennung "nur Steuergerät" vs. "komplette Mechatronik inkl. Hydraulik" als Konfigurator-Option übertragbar.
- Für einen eigenen Konfigurator genügt eine viel kleinere Datenstruktur: Getriebefamilie (DQ200/DQ250/DQ381/DQ500/DL501/…) → Leistung (Steuergerät-Reparatur / Mechatronik-Überholung / Datenübertragung) → Preis + Laufzeit + typische Fehlercodes + Einsendehinweis; Teilenummer als Freitext-/Validierungsfeld statt als eigener Katalogdatensatz.

### Gaps
- Exakte Anzahl Marken und Katalogeinträge: nicht ermittelbar (Seite gesperrt, kein Snippet mit Gesamtzahl).
- Keine ecu.de-Treffer für ZF 8HP-Mechatronik und Multitronic 0AW; ob diese Typen im Katalog fehlen oder nur nicht indexiert sind, ist offen.
- Ob es eine Suche nach Fehlercode gibt, ist nicht belegt (belegt ist nur die Teilenummernsuche).
- Laufzeiten/Fehlerlisten für DQ250 und DL501 nicht im Auszug enthalten.

## 2. Aufbau einer einzelnen Reparatur-Angebotsseite

### Takeaway
Eine Typ-/Teilenummernseite kombiniert: Teilenummern, reparierbare Fehlerbilder/Fehlercodes, Standard-Festpreis je Gerätetyp (brutto + netto, teils "ab"), Laufzeit "X Tage + 2 Tage Versand", Einsende- und Einbauhinweise sowie Standardklauseln zu Mehrkosten. Kein Befund = nur Prüfpauschale.

### Cited Findings
- Preislogik: "Der Reparaturpreis ist ein Standardbearbeitungspreis für das jeweilige Gerät."; bei "besonders schweren Schäden wie bspw. zerstörten Prozessoren reparieren wir ggf. nach Absprache zu höherem Reparaturpreis"; "Bei Schäden durch Fremdeingriff berechnen wir eine Bearbeitungsgebühr"; Versand kommt hinzu **[Auszug]** — [BMW ZF 6HP](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp-6854), [722.9](https://ecu.de/t/mercedes-steuergeraete-reparatur/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/vgs-nag2-7g-tronic-(722.9)-5150)
- MwSt.-Darstellung: "Nettopreise verstehen sich zzgl. der gesetzlichen Mehrwertsteuer"; Bruttopreise inkl. MwSt.; auf der Versandseite: "Alle Preise sind Nettopreise, zzgl. der gesetzlichen Mehrwertsteuer von 19%" **[Auszug]** — [722.9](https://ecu.de/t/mercedes-steuergeraete-reparatur/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/vgs-nag2-7g-tronic-(722.9)-5150), [Versand](https://ecu.de/auftrag/versand-43.htm)
- "ab"-Preis kommt vor (DQ200 Steuergerät "ab 300,00 €"), daneben Festpreise (Mechatronik-Überholung 550,00 € netto) **[Auszug]** — [DQ200](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq200-(0am)-7722)
- Laufzeitformat: "1-2 Tage + 2 Tage Versand" (722.9), "2-3 Tage + 2 Tage Versand" (6HP, DQ381), "3-4 Tage + 2 Tage Versand" (DQ200-Überholung), "4-5 Tage + 2 Tage Versand" (Multitronic) **[Auszug]** — Quellen siehe Tabelle Abschnitt 1
- Fehlerbeschreibung je Typ: Liste reparierbarer Codes plus Klartext (z. B. P0805/P1735/P1736 beim DQ381; P17BF/P0841/P189C beim DQ200-Hydraulikmodul) und Abgrenzung, welche Fehler am Steuergerät bzw. am Hydraulikmodul liegen **[Auszug]** — [DQ381](https://ecu.de/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq381-dq500-%280gc-0dl%29-bosch-6426), [DQ200 Audi](https://ecu.de/t/audi/getriebe-steuerger%C3%A4t/dsg-7-gang-dq200-(0am)-7719)
- Einsendehinweis mit Bild ("nur wie im Bild dargestellt ... OHNE Schieberkasten (EHS) einsenden"); bei manchen Geräten zusätzlich einzusendende Teile (z. B. Ford-Focus-Motorsteuergerät: Kombiinstrument und Schlüssel) **[Auszug]** — [BMW 6HP](https://ecu.de/bmw/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/steuerger%C3%A4t-6-gang-automatik-zf-6hp/bmw-7541027-bosch-0260550008-zf-0501213727-147391.html), [Ford](https://ecu.de/ford/motorsteuerger%C3%A4t/edc16c34/ford-9m5112a650mb-bosch-0281016740-106462.html)
- Einbauhinweis: nach Prüfung/Reparatur von DQ381/DQ500 ist nach dem Einbau eine Grundeinstellung mit Diagnosetester durchzuführen (also nicht reines Plug & Play) **[Auszug]** — [DQ500](http://ecu.de/vw-(volkswagen)/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq500-(0bh-0bt)-continental-5295)
- Statusvermerk möglich: eine DQ250-Seite meldet, Reparaturen seien "vorübergehend nicht möglich" **[Auszug]** — [DQ250](https://ecu.de/t/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-6-gang-dq250-(02e)-3682)
- Kein Fehler feststellbar: "15 – 20 % der eingeschickten Steuergeräte" zeigen keinen Fehler; dann wird nur die Prüfgebühr berechnet **[Auszug]** — [Reparaturprozess](https://ecu.de/auftrag/reparaturprozess-5.htm)
- Prüfpauschale laut FAQ: 50 € zzgl. MwSt. und Versand, Erhöhung auf 70 € ab 01.07.2026 angekündigt **[Auszug; ob die Erhöhung umgesetzt wurde, nicht verifiziert]** — [FAQ](https://ecu.de/faq-39.htm)
- Mehraufwand wird berechnet, wenn Geräte durch (fremde) Reparaturversuche beschädigt oder irreparabel wurden **[Auszug]** — [Reparaturauftrag allg. PDF](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf)
- Gewährleistung: "Sie erhalten 24 Monate Gewährleistung auf alle Reparaturen unseres Internetangebotes."; laut FAQ 2 Jahre ab Reparaturdatum auf dem Garantiesiegel und nur bei unbeschädigtem Siegel; bei Auftrag über eine Werkstatt Abwicklung nur über diese Werkstatt **[Auszug]** — [Mercedes-Seite](https://ecu.de/reparatur-mercedes-benz-steuergeraete-121.htm), [FAQ](https://ecu.de/faq-39.htm)
- Prozess im Haus: Sichtprüfung → Eingangstest auf Prüfstand (Fehler reproduzieren) → Austausch defekter Bauteile → Ausgangstest **[Auszug]** — [Reparaturprozess](https://ecu.de/auftrag/reparaturprozess-5.htm)
- Daneben Verkauf von Neu-/Reman-Teilen (Landingpage "Bestellung eines Neuteil oder Remanteil", 2 Jahre) und Ankauf von Steuergeräten **[Auszug]** — [Neuteil/Reman](https://ecu.de/landingpage---bestellung-eines-neuteil-oder-remanteil-318.htm), [Ankauf](https://ecu.de/kontakt/ankauf-144.htm)

### Inferences
- ecu.de arbeitet nicht mit Warenkorb + Vorabzahlung, sondern mit "Preis als Orientierung → Einsendung → Prüfung → ggf. Abweichung nach Absprache → Rechnung". Der Seitenpreis ist ein Regelpreis mit drei offenen Flanken (schwerer Schaden, Fremdeingriff, kein Fehler).
- Pflichtelemente einer Angebotsseite für OZ: Leistungsumfang, Netto/Brutto-Preis, Laufzeit ab Wareneingang + Versandtage, reparierbare Fehlercodes, "Was einsenden / was nicht", "Was nach dem Einbau nötig ist", Prüfpauschale bei "kein Fehler", Zuschlag bei Fremdeingriff, Gewährleistungsdauer und Siegelbedingung.

### Gaps
- Express-Reparatur (beschleunigte Bearbeitung) und deren Aufpreis: nicht belegt; belegt ist nur Express-**Versand**.
- Pfand/Kaution auf Reparaturen: nicht belegt (Pfand nur für die DQ250-Spezialverpackung).
- Höhe der Bearbeitungsgebühr bei Fremdeingriff und aktueller Stand der Prüfpauschale (50 € vs. 70 €): nicht verifiziert.

## 3. Auftragsprozess Schritt für Schritt und Felder des Reparaturauftrags

### Takeaway
Kein Shop-Checkout: Der Kunde erzeugt einen "Reparaturauftrag" — entweder als mehrstufiges Online-Formular (Ergebnis: druckbarer Auftrag + ggf. Versandetikett-PDF) oder als herunterladbares PDF je Gerätekategorie — unterschreibt ihn und legt ihn dem Paket bei. Die Unterschrift dient zugleich der AGB-Annahme und dem Verzicht auf das Abwarten der Widerrufsfrist.

### Cited Findings
- Online-Strecke "So funktioniert es": Schritte Fahrzeugdaten → Fehlerbeschreibung → Kontaktdaten und Referenzen → "Packliste zur Einsendung" → Abholung → Rückversand und Zahlung; am Ende erhält man den fertigen Reparaturauftrag zum Ausdrucken, unterschreibt ihn und legt ihn bei; bei beauftragter Abholung zusätzlich den Frachtbrief/das Versandetikett zum Ausdrucken **[Auszug]** — [So funktioniert es](https://ecu.de/sie-und-ecude/so-funktioniert-es-191.htm)
- Die Online-Formulare liegen unter `/form/<id>`, `/form/inquiry/<id>`, `/form/productDataModify`, `/form/successRequest` (Seitentitel jeweils "Reparaturauftrag") — d. h. der Einstieg erfolgt aus einer Teilenummernseite heraus mit vorbelegten Gerätedaten, die änderbar sind **[Auszug, aus URLs/Titeln]** — [Formular](https://ecu.de/form/105201), [Anfrage](https://ecu.de/form/inquiry/146960)
- Erster Formularschritt = Gerätedaten mit Teilenummernsuche; Felder "Gerätehersteller", "Geräteherstellerteilenummer", "Fahrzeugherstellerteilenummer" **[Auszug]** — [Formular](https://ecu.de/form/104327)
- PDF-Formulare zum Download unter "Reparaturaufträge ecu.de" (ecu.de/auftrag), getrennt nach Gerätekategorie: allgemein (`06_2023_reparaturauftrag_allg.pdf`), ABS (`…_abs.pdf`), EZS/elektronisches Zündschloss (`…_ezs.pdf`), Kombiinstrument (`reparaturauftrag_ki.pdf`), Hochvolt (`reparaturauftrag_hochvolt.pdf`); zusätzlich "Abholauftrag" (`abholauftrag.pdf`) **[Auszug]** — [Auftragsseite](https://ecu.de/auftrag-8.htm), [allg.](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf), [ABS](https://ecu.de/cms/media/06_2023_reparaturauftrag_abs.pdf), [EZS](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf), [KI](https://ecu.de/cms/media/reparaturauftrag_ki.pdf), [Hochvolt](https://ecu.de/cms/media/reparaturauftrag_hochvolt.pdf), [Abholauftrag](https://ecu.de/cms/media/abholauftrag.pdf)
- "Jeder Sendung muss ein ausgefüllter Reparaturauftrag beiliegen"; möglichst vollständig ausfüllen **[Auszug]** — [Auftragsseite](https://ecu.de/auftrag-8.htm)
- Zitierte Feldbezeichnungen der PDF-Formulare **[alle Auszug]**:
  - Kopf/Abschnitt "1. Kundendaten": "[ ] Ich bin Bestandskunde", "Kundennr: …" — [allg.](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf)
  - E-Mail-Hinweis: "* Es wird Ihnen eine Benachrichtigung zu Posteingang, [Auftragsstatus und Rückversand mit Paketverfolgung an die angegebene E-Mail-Adresse gesendet]" — [EZS alt](https://ecu.de/cms/media/reparaturauftrag_ezs.pdf)
  - "Fahrzeugdaten": "Bitte legen Sie eine Kopie des Fahrzeugscheins bei" — ersatzweise Schlüsselnummern HSN/TSN, FIN, Erstzulassung — [allg.](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf)
  - "Fehlerbeschreibung": "Fehlerspeicher ausgelesen?", "Fehlercodes vorhanden? [ ] nein [ ] ja (wenn ja, bitte unbedingt Fehlercode angeben)", "Verwendetes Diagnosegerät"; Fehlerprotokoll beilegen — [allg. alt](https://ecu.de/cms/media/reparaturauftrag_allg.pdf)
  - Zahlung/Abwicklung: Ankreuzfelder "Kostenvoranschlag", "Rechnung", "Nachnahme", "Vorkasse" (Kreditkarte, Überweisung, PayPal) sowie Feld "Freigabe Reparaturaufwand" — [EZS](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
  - "Rückversand": "Standardversand | Express | Abholung in Zittau"; Express Samstagszustellung innerhalb Deutschlands "(zzgl. Aufpreis)" — [KI](https://ecu.de/cms/media/reparaturauftrag_ki.pdf)
  - Option, beide Einheiten überholen zu lassen, mit "Aufpreis" — [allg.](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf)
  - Haftung: "Die Glaubitz GmbH & Co. KG übernimmt keine Haftung beim Verlust nicht aufgeführter Teile." (→ Packliste der eingesandten Teile) — [EZS](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
  - Widerruf: "Die Glaubitz GmbH & Co. KG wird unverzüglich aufgefordert mit der Reparatur sowie allen zum Auftrag gehörenden Leistungen vor Ende meiner 14-tägigen Widerrufsfrist zu beginnen. Mir ist bewusst, dass bei fristgerechtem Widerruf für die bereits erbrachten Leistungen ein Wertersatz zu zahlen ist." — [EZS](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
  - "Die AGB, sowie Informationen zum Widerrufsrecht sind einsehbar unter ecu.de/agb" — [allg.](https://ecu.de/cms/media/06_2023_reparaturauftrag_allg.pdf)
  - Eigentums-/Berechtigungserklärung: Gerät befindet sich rechtmäßig im Besitz und wird legal genutzt; ist der Auftraggeber nicht Fahrzeughalter, muss er die Rechtmäßigkeit mit dem Eigentümer klären (v. a. EZS/Wegfahrsperre) — [EZS](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
  - Datum + Unterschrift: "Unterschreiben Sie diesen bitte und schicken ihn im Paket mit" — [So funktioniert es](https://ecu.de/sie-und-ecude/so-funktioniert-es-191.htm)
- FAQ: Zur Bearbeitung müssen die AGB auf dem Reparaturauftrag per Unterschrift akzeptiert werden **[Auszug]** — [FAQ](https://ecu.de/faq-39.htm)
- Kundennummer/alte Auftragsnummer beschleunigt die Zuordnung; Neukunden erhalten bei Paketeingang Kunden- und Auftragsnummer **[Auszug]** — [FAQ](https://ecu.de/faq-39.htm)
- Vorbereitungshinweis: Fehlerspeicher auslesen, bevor das Steuergerät ausgebaut oder die Batterie abgeklemmt wird (Fehlercodes gehen sonst teils verloren) **[Auszug]** — [Reparaturprozess](https://ecu.de/auftrag/reparaturprozess-5.htm)
- Wird keine Rückversandart gewählt: Bestandskunden erhalten die Versandart des letzten Auftrags, Neukunden Express **[Auszug]** — [Versand](https://ecu.de/auftrag/versand-43.htm)

### Inferences
- Minimal-Datenmodell eines Einsende-Auftrags (abgeleitet): (1) Gerät: Marke, Gerätetyp, Fahrzeughersteller-Teilenummer, Gerätehersteller + -nummer; (2) Fahrzeug: HSN/TSN, FIN, Erstzulassung oder Fahrzeugschein-Upload; (3) Fehler: Freitext, Fehlerspeicher ausgelesen ja/nein, Codes, Diagnosegerät, Protokoll-Upload; (4) Kunde: Bestandskunde/Kundennr., Privat/Werkstatt, Rechnungs-/Lieferadresse, E-Mail für Statusmeldungen, eigene Referenz; (5) Packliste (was liegt im Paket); (6) Hinversand: selbst / Abholung; (7) Rückversand: Standard / Express / Samstag / Selbstabholung; (8) Zahlung: Vorkasse / Nachnahme / Rechnung (B2B); Kostenvoranschlag gewünscht ja/nein bzw. Freigabegrenze; (9) Einwilligungen: AGB, Widerrufsbelehrung + sofortiger Leistungsbeginn, Berechtigungserklärung; (10) Datum/Unterschrift.
- Die Felder "Kilometerstand", "vorherige Reparaturversuche" sind in den Auszügen nicht als eigene Felder belegt; inhaltlich wird Fremdeingriff aber über Gebühren sanktioniert — für OZ empfiehlt sich ein explizites Ja/Nein-Feld.
- Kategoriespezifische Formulare (ABS, EZS, KI, Hochvolt) zeigen: Zusatzfragen hängen am Gerätetyp. Ein Konfigurator sollte Getriebe-spezifische Zusatzfelder haben (Getriebekennbuchstabe, Ölstand/-wechsel, Symptome kalt/warm, Kupplung getauscht?).

### Gaps
- Vollständiger Wortlaut und Reihenfolge aller Formularfelder: nicht direkt lesbar (PDFs gesperrt); Zitate stammen aus Snippets von PDF-Versionen "06_2023" und älteren Versionen.
- Ob "Kilometerstand" und "bisherige Reparaturversuche" als Felder existieren: nicht belegt.
- Ob das Online-Formular eine digitale Unterschrift/Checkbox akzeptiert oder zwingend den Ausdruck verlangt: Auszüge sprechen nur vom Ausdruck mit Unterschrift.

## 4. Versand: Einsendung, Abholung, Rückversand, Verpackung, Ausland

### Takeaway
Einsendung wahlweise selbst frankiert oder per kostenpflichtigem Abholauftrag (DHL Express/UPS, 10 € netto, Etikett als PDF per E-Mail, bis 1.500 € versichert). Rückversand standardmäßig per DHL, Kosten nach Größe/Gewicht ohne öffentliche Preistabelle; Express, Samstag und Nachnahme gegen Aufpreis.

### Cited Findings (ecu.de, alle **[Auszug]**)
- Abholung: online oder per Fax-Formular beauftragbar; Dienstleister DHL Express (auch UPS genannt); Kosten 10 EUR netto zzgl. MwSt. innerhalb Deutschlands, Ausland abweichend; Abholzeitfenster ab 12:00 Uhr, mindestens 2 Stunden — [Abholung](https://ecu.de/abholung-202.htm), [Abholauftrag PDF](https://ecu.de/cms/media/abholauftrag.pdf)
- Nach Online-Auslösung: E-Mail mit Zusammenfassung und "persönlichem Versandetikett im PDF-Format" zum Ausdrucken — [Abholung](https://ecu.de/abholung-202.htm)
- Versicherung: Abholauftrag bis 1.500 EUR Warenwert versichert; Höherversicherung mind. 5 € bzw. 0,5 % des Warenwerts (Beispiel im Formular: 2.500 € Warenwert = 12,50 €) — [Abholauftrag PDF](https://ecu.de/cms/media/abholauftrag.pdf)
- Verpackung: Pakete müssen frei von Gefahrgut-Aufklebern und alten Versandetiketten sein; Gefahrgutlabel verursachen Zusatzkosten, die weiterberechnet werden — [So funktioniert es](https://ecu.de/sie-und-ecude/so-funktioniert-es-191.htm), [Versand](https://ecu.de/auftrag/versand-43.htm)
- Spezialverpackungen (DSG DQ250; VL300) als Leihverpackung mit 25 EUR Pfand — [DQ250](https://ecu.de/abholung/spezialverpackung-dsg-dq-250-221.htm), [VL300](https://ecu.de/abholung/spezialverpackung-vl300-255.htm)
- "Gesonderte Hinweise bei verölten Steuergeräten" als eigene Infoseite — [Hinweise](https://ecu.de/gesonderte-hinweise-bei-veroelten-steuergeraeten-238.htm)
- Rückversand: "Die Versandkosten sind abhängig von Paketgröße und Gewicht"; genaue Berechnung über Hotline bzw. Versandkostenrechner; Inland: Normalversand oder Express; Ausland: Normalversand per Vorkasse — [Versand](https://ecu.de/auftrag/versand-43.htm)
- Rückversand in der Regel per DHL; Nachnahme derzeit nur über DHL Express und UPS; zusätzliche Nachnahmegebühr; Express-Samstagszustellung in Deutschland mit Aufpreis — [FAQ](https://ecu.de/faq-39.htm), [Versand](https://ecu.de/auftrag/versand-43.htm)
- Zollbestimmungen-Seite mit Zolltarifnummern je Gerätekategorie für Nicht-EU-Sendungen — [Zollbestimmungen](https://ecu.de/auftrag/versand/zollbestimmungen-99.htm)
- Selbstabholung: Option "Abholung in Zittau" im Formular — [KI-Formular](https://ecu.de/cms/media/reparaturauftrag_ki.pdf)

### Inferences
- ecu.de verkauft **kein** einfaches "DHL-Paketlabel" für die Einsendung, sondern einen Express-Abholservice mit Pauschale. Ein günstiges vorfrankiertes DHL-Paketlabel (Retoure) wäre für OZ ein Differenzierungsmerkmal.
- Mechatroniken sind ölhaltig: Verpackungsvorgaben (Öl ablassen, öldicht verpacken, keine Gefahrgutlabel) und ggf. Leihverpackung mit Pfand sind für ein Getriebe-Einsendeangebot relevanter als bei reiner Elektronik.

### Gaps
- Konkrete Rückversandpreise (Standard, Express, Samstag, Nachnahme) von ecu.de: keine öffentliche Tabelle in den Auszügen; ein Snippet nennt widersprüchlich "0,00 EUR Bearbeitungsgebühr".
- Auslandstarife: nicht ermittelbar.

## 5. Status, Kommunikation, Zahlung, B2B

### Takeaway
Kommunikation läuft per E-Mail in drei Stufen (Posteingang, Auftragsstatus, Rückversand mit Tracking). Privatkunden zahlen per Vorkasse oder Nachnahme nach Fertigstellung; Werkstätten werden ab dem 2. Auftrag auf Rechnung (7 Tage) umgestellt. Ein Kostenvoranschlag ist optional ankreuzbar.

### Cited Findings (alle **[Auszug]**)
- E-Mail-Benachrichtigungen zu Posteingang, Auftragsstatus und Rückversand mit Paketverfolgung, sofern E-Mail im Auftrag angegeben — [EZS-Formular](https://ecu.de/cms/media/reparaturauftrag_ezs.pdf)
- Nach Abschluss des Auftrags und Rechnungserstellung: E-Mail mit Gesamtbetrag, Bankverbindung und Zahlungslink; "Sobald der Rechnungsbetrag bei uns vollständig eingegangen ist, wird die Sendung für den Versand vorbereitet", Übergabe an den Versender spätestens am nächsten Werktag; digitale Zahlungsbelege werden nicht als Nachweis akzeptiert — [Zahlungsoptionen](https://ecu.de/auftrag/zahlungsoptionen-256.htm), [FAQ](https://ecu.de/faq-39.htm)
- Vorkasse-Arten: Kreditkarte, Sofortüberweisung, PayPal, Überweisung (FAQ nennt zusätzlich Paydirekt) — [Zahlungsoptionen](https://ecu.de/auftrag/zahlungsoptionen-256.htm), [FAQ](https://ecu.de/faq-39.htm)
- Werkstattkunden/Kfz-Gewerbe: ab dem 2. Auftrag Umstellung auf Rechnung mit 7 Tagen Zahlungsziel; Glaubitz behält sich Umstellung auf Vorkasse/Nachnahme vor; Werkstätten können jederzeit Vorkasse/Nachnahme wählen — [FAQ](https://ecu.de/faq-39.htm), [Zahlungsoptionen](https://ecu.de/auftrag/zahlungsoptionen-256.htm)
- Nachnahme: Inland nur via DHL Express und UPS; Ausland (außer Österreich) Nachnahme nur via UPS, sonst Vorkasse — [Zahlungsoptionen](https://ecu.de/auftrag/zahlungsoptionen-256.htm)
- Kostenvoranschlag und "Freigabe Reparaturaufwand" als Formularfelder — [EZS-Formular](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
- Rechnungen in EUR; schrittweise Einführung digitaler Rechnungszustellung; steuerfreie EU-Rechnung nur bei exakt passender Rechnungsadresse/USt-IdNr. — [FAQ](https://ecu.de/faq-39.htm)
- Zielgruppenseite "Sie und ecu.de" (Werkstätten/Privat) — [Sie und ecu.de](https://ecu.de/sie-und-ecude-157.htm)

### Inferences
- Zahlung erfolgt **nach** Reparatur, **vor** Rückversand (Privat) — passend zum Modell "Preis kann nach Befund abweichen". Für Wix bedeutet das: kein Pflicht-Checkout beim Absenden des Konfigurators; Zahlungslink (z. B. Wix Payments/PayPal-Rechnung) nach Befund.
- Statusstufen für OZ: Auftrag angelegt → Paket eingegangen → Befund/KVA → Freigabe → Reparatur fertig/Rechnung → bezahlt → versandt (Tracking).

### Gaps
- Online-Auftragsverfolgung/Kundenportal mit Login: nicht belegt.
- Händlerrabatte/Preisstaffeln für Werkstätten: nicht belegt (nur Zahlungsziel).
- Klarna: nicht belegt.
- Ablauf der KVA-Freigabe (Frist, Kosten bei Ablehnung): nicht belegt.

## 6. Rechtliche/kaufmännische Texte

### Takeaway
Kernbausteine bei ecu.de: 24 Monate Gewährleistung an unbeschädigtes Garantiesiegel gebunden, ausdrückliche Aufforderung zum Leistungsbeginn vor Ablauf der 14-tägigen Widerrufsfrist mit Wertersatzhinweis, Haftungsausschluss für nicht aufgelistete Teile, Berechtigungserklärung bei wegfahrsperrenrelevanten Geräten, Hinweis auf nötige Grundeinstellung nach Einbau.

### Cited Findings (alle **[Auszug]**)
- Gewährleistung 24 Monate auf alle Reparaturen; FAQ: 2 Jahre ab Reparaturdatum laut Garantiesiegel, nur bei unbeschädigtem Siegel; Werkstattaufträge nur über die Werkstatt — [Mercedes-Seite](https://ecu.de/reparatur-mercedes-benz-steuergeraete-121.htm), [FAQ](https://ecu.de/faq-39.htm)
- Widerruf (Verbraucher, Dienstleistung): Wortlaut siehe Abschnitt 3 (sofortiger Beginn + Wertersatz); AGB/Widerrufsinformationen unter ecu.de/agb — [EZS-Formular](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
- Haftung eingesandte Teile: keine Haftung für nicht aufgeführte Teile — [EZS-Formular](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
- Wegfahrsperre/Fahrberechtigung: Im Rahmen der Reparatur (EZS) erfolgt Programmierung und/oder Neuanlernen des Fahrberechtigungssystems; Kunde bestätigt rechtmäßigen Besitz/legale Nutzung, Nicht-Halter müssen Legitimation klären — [EZS-Formular](https://ecu.de/cms/media/06_2023_reparaturauftrag_ezs.pdf)
- Nach Einbau: DQ381/DQ500 Grundeinstellung mit Diagnosetester; bei extern verursachten Defekten ggf. Adaptionswerte zurücksetzen bzw. weitere Arbeiten am Fahrzeug — [DQ500](http://ecu.de/vw-(volkswagen)/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-7-gang-dq500-(0bh-0bt)-continental-5295), [Reparaturprozess](https://ecu.de/auftrag/reparaturprozess-5.htm)
- Datenübernahme als kostenpflichtige Einzelleistung (DQ250 "Datenübertragung" 190 € netto) — [DQ250](https://ecu.de/t/vw-volkswagen/getriebesteuerger%C3%A4t-w%C3%A4hlhebel/dsg-6-gang-dq250-(02e)-3682)
- Vergleich Markt: Grundeinstellung der Schaltsteller und Adaptionsfahrt "ausschließlich am Fahrzeug" (az-teile); Teilenummer 0AM vs. 0CW vorab prüfen, FIN im Bestellkommentar — [az-teile](https://www.az-teile.de/dq200-mechatronik-reparieren-oder-tauschen/)

### Inferences
- Da das reparierte Originalgerät zurück ins selbe Fahrzeug geht, bleiben Codierung/Wegfahrsperre normalerweise erhalten; "Plug & Play" ist bei DSG aber nur eingeschränkt richtig, weil Grundeinstellung/Adaption nötig ist — das sollte OZ als Pflichthinweis führen (und als Upsell: Einbau + Grundeinstellung in Bochum).
- Für einen Verbraucher-Fernabsatzvertrag über eine Dienstleistung braucht OZ: Widerrufsbelehrung + Muster-Widerrufsformular, ausdrückliche Zustimmung zum vorzeitigen Beginn (Checkbox), Wertersatzhinweis; seit 19.06.2026 ist außerdem für online geschlossene Verbraucherverträge der elektronische Widerrufsbutton relevant (rechtlich prüfen lassen — hier nicht recherchiert).

### Gaps
- AGB-Volltext von ecu.de (Haftungsgrenzen beim Transport, Aufbewahrungs-/Verwertungsfristen nicht abgeholter Geräte, Datenlöschung): nicht lesbar und nicht in Auszügen.
- Keine Aussage von ecu.de zu "Plug & Play" oder Datenlöschung gefunden.
- Keine anwaltlich geprüften Aussagen; rechtliche Punkte sind nur Strukturhinweise.

## 7. Vergleichsanbieter (alle aus Suchauszügen; Websites nicht direkt erreichbar)

### Takeaway
Das Muster "Gerät/Getriebetyp wählen → Auftrag online anlegen → Formular beilegen → einsenden → Reparatur zum Festpreis → Rückversand" ist marktüblich; Unterschiede liegen bei Zielgruppe (ACtronics nur B2B mit Konto), Preislogik (Festpreis vs. Befund+Freigabe), Rückversand (oft kostenlos) und Garantie (12–36 Monate).

### Cited Findings (alle **[Auszug]**)
- **ACtronics (actronics-gmbh.de):** 5 Schritte "Konto erstellen → Auftrag starten → Teil einsenden → Reparatur wird gestartet → Reparatur erfolgreich – Versand"; arbeitet "ausschließlich mit Werkstätten und Markenhändlern" (Privatkunden nur über Werkstatt); Werkstatt übermittelt Diagnoseinformationen; Teil wird eingesandt oder auf Wunsch abgeholt; 2 Jahre Garantie auf die Revision; Bearbeitung "in der Regel 48 Stunden" bzw. "wenige Tage"; eigene Kategorie "DSG-Getriebe Reparatur für Werkstätten"; Katalog nach Produktgruppe → Gerätetyp (z. B. /abs-steuergerat/bosch-5-7, /motorsteuergerat/bosch-edc16c35) — [ACtronics Start](https://www.actronics-gmbh.de/), [Bosch 5.7](https://www.actronics-gmbh.de/abs-steuergerat/bosch-5-7), [DSG](https://www.actronics-gmbh.de/dsg-getriebe), [FRM](https://www.actronics-gmbh.de/zentral-steuergerat/bmw-footwell-control-module-frm)
- ACtronics UK: Konto erforderlich, Antrag wird vom Kundenservice geprüft — [actronics.co.uk DQ200](https://www.actronics.co.uk/tcu/dsg-7-dq200-0am)
- **ECU Testing (ecutesting.com, UK):** Online-Bestellformular; Versandlabels per E-Mail zum Ausdrucken, Kurierabholung wird organisiert; Status-Updates per SMS und E-Mail in jeder Phase; lebenslange Garantie (laut Kundenbewertungen); bei "kein Fehler" Rückerstattung abzüglich Prüfgebühr und Porto — also Vorabzahlung im Shop; Kategorie "DSG Mechatronic Repair" — [Trustpilot](https://www.trustpilot.com/review/www.ecutesting.com?page=4), [reviews.co.uk](https://www.reviews.co.uk/company-reviews/store/ecu-testing-ltd/y5e), [Kategorie DSG](https://www.ecutesting.com/categories/dsg-mechatronic-units/)
- **UX-Motoring (ux-motoring.de):** "Formular ausfüllen, beilegen, verpacken, absenden"; 1–2 Werktage nach Wareneingang; "Festpreis ab 89 €"; bis zu 36 Monate Garantie; Seiten je Getriebe DQ200/DQ250/DQ381/DQ500 — [DSG-Reparatur](https://www.ux-motoring.de/dsg-reparatur), [DQ200](https://www.ux-motoring.de/dsg-doppel-kupplungs-schlatgetriebe-dq200)
- **stg24.de:** Reparatur als Shop-Produkt mit Warenkorb ("VW DSG7 DQ200 Getriebesteuergerät Reparatur" 399,00 €), ca. 2 Werktage, 24 Monate Gewährleistung, kostenloser Rückversand deutschlandweit — [stg24](https://stg24.de/produkt/vw-dsg7-dq200-gang-mechatronik-reparatur/)
- **Repair First (repairfirst.de):** Shop-Kollektion "DQ200 Reparatur & Austausch", 339 € zzgl. MwSt., 2–4 Werktage — [repairfirst](https://repairfirst.de/collections/dq200-reparatur-austausch)
- **getriebe.biz:** "Mechatronik einsenden bundesweit": zuerst schriftlicher Befund mit Ursache und Kostenrahmen, Reparatur erst nach Freigabe — [getriebe.biz](https://getriebe.biz/einsenden)
- **az-teile.de:** "DSG Getriebe Instandsetzung: einsenden, wir reparieren"; Rückversand innerhalb Deutschlands kostenfrei per DHL oder DPD; Hinweis 0AM/0CW, FIN angeben — [az-teile Einsenden](https://www.az-teile.de/dsg-getriebe-instandsetzung-einsenden/)
- **Rezek (steuergeraetrezek.de):** 1 Jahr Garantie auf DQ200-Reparatur — [Rezek](https://steuergeraetrezek.de/7-gang-dsg-mechatronik-dq200-reparatur/)

### Inferences
- Drei Flow-Varianten am Markt: (A) Katalog + Reparaturauftrag ohne Vorabzahlung (ecu.de); (B) Shop-Produkt mit Checkout und Vorabzahlung, Erstattung minus Prüfgebühr bei "kein Fehler" (stg24, Repair First, ECU Testing); (C) Einsendung → Befund → Freigabe (getriebe.biz). Für eine Wix-Seite ohne Shop-Zwang ist A/C als Formular-Wizard am einfachsten; B wäre mit Wix Stores umsetzbar.
- Kostenloser Rückversand und klare Garantiezahl (24 Monate) sind bei den DSG-Spezialisten Standard-Verkaufsargumente; ecu.de berechnet Versand separat.

### Gaps
- HIXA, Getriebe1, dsg-getriebe-reparatur.de, ecu.eu: keine verwertbaren Suchtreffer, Websites nicht erreichbar.
- Keine der Vergleichsseiten direkt gelesen; Preise/Garantien ungeprüft.

## 8. DHL-Integration für einen Kleinbetrieb (Deutschland, 2026) und Wix-Versand-Apps

### Takeaway
Ohne Vertrag: DHL Online Frankierung zu Listenpreisen (5 kg 7,69 €, 10 kg 10,49 €, 31,5 kg 23,99 €; Haftung 500 €; Transportversicherung bis 2.500 € +6,99 €). Programmatisch erzeugte Labels für Kunden (DHL Retoure als PDF/QR) setzen einen DHL-Geschäftskundenvertrag voraus (ab ca. 200 Sendungen/Jahr, mit Monatspauschale) plus Developer-Portal-App; Alternative ohne eigenen Vertrag sind Aggregatoren wie Sendcloud, die es auch als Wix-App gibt.

### Cited Findings
**DHL Privatkunden/Online Frankierung [direkt gelesen, dhl.de, 25.11.2026]** — [Preisübersicht national](https://www.dhl.de/de/privatkunden/pakete-versenden/deutschlandweit-versenden/preise-national.html)
- Päckchen S bis 2 kg (35×25×10 cm) 4,19 EUR; Päckchen M bis 2 kg (60×30×15) 5,19 EUR; Paket 2 kg (60×30×15, nur online) 6,19 EUR; **Paket 5 kg (120×60×60) 7,69 EUR; Paket 10 kg 10,49 EUR; Paket 20 kg 18,99 EUR; Paket 31,5 kg 23,99 EUR** (31,5 kg inkl. 19 % USt.; bis 20 kg umsatzsteuerfreie Endpreise). In der Tabelle steht bei allen Produkten "Sendungsverfolgung, Haftung bis 500 EUR".
- Zubuchbare Services Paket national: Abholung (nur online) +3,00 EUR (kostenlos ab vier online frankierten Paketen pro Warenkorb); **Nachnahme (nur online) +8,99 EUR; Transportversicherung bis 2.500 EUR +6,99 EUR; bis 25.000 EUR +19,99 EUR**; Sperrgut +28,99 EUR; Liefertag +0,99 EUR; Alterssichtprüfung +1,99 EUR.
- Express national (Online-Preis / Filialpreis), Zustellung nächster Tag Mo–Fr: bis 5 kg (60×30×15) 18,00 / 19,50 EUR; **bis 10 kg 30,00 / 32,50 EUR**; bis 20 kg 36,00 / 38,50 EUR; bis 31,5 kg 54,00 / 56,50 EUR. Zeitoptionen: vor 12 Uhr +6,90, vor 10:30 +21,90, vor 9 Uhr +49,90 EUR. **Samstagszustellung +11,90 EUR**; Express-Abholung +8,00 EUR; Transportversicherung Express +0,5 % des Warenwerts, mind. 5,00 EUR; Zusatzservices für Express nur bei Filialeinlieferung zubuchbar.
- Label ohne Drucker: Versandmarke online kaufen → QR-Code → Ausdruck an Packstation, in Filiale oder durch Zusteller ("Mobile Paketmarke"). Sendungen mit Service Transportversicherung können nicht über Packstation eingeliefert werden.
- Ankündigung: "Ab 1. Januar 2027 gelten neue Preise und Formate für Brief, Päckchen und Paket."

**DHL Geschäftskunden [direkt gelesen, dhl.de]**
- Geschäftskunde ab 200 Sendungen/Jahr; Vertrag je nach Volumen direkt online abschließbar; Werbepreis "ab 4,24 EUR" (1-kg-Paket, inkl. Monatspauschale-Umlage bei beispielhaft 3.000 Sendungen/Jahr); Haftung bis 500 EUR pro Paket inklusive; Abholung an vereinbarter Adresse inklusive — [Kunde werden](https://www.dhl.de/de/geschaeftskunden/paket/kunde-werden.html), [Paket](https://www.dhl.de/de/geschaeftskunden/paket/leistungen-und-services/paket.html)
- DHL Retoure – vier Bereitstellungsarten: (1) **als QR-Code** (Kunde meldet Retoure an, Label wird in Filiale/Paketshop/Packstation oder vom Zusteller gedruckt; QR max. 30 Tage gültig); (2) **als PDF zum Selbstdrucken**; (3) **als beigelegtes Label** (vorab über das Versandsystem erzeugt); (4) **als mitgebrachtes Label** (DHL holt an Kundenadresse ab und bringt das Label mit; Beauftragung über "DHL Einzelabholauftrag" im Geschäftskundenportal bis 14 Tage im Voraus). Erzeugung über Funktion "Retoure" im Post & DHL Geschäftskundenportal (Retourenportal für Endkunden) oder die Retouren-API; Retourenlabel unbegrenzt gültig (nur QR 30 Tage) — [DHL Retoure](https://www.dhl.de/de/geschaeftskunden/paket/leistungen-und-services/retoure.html)
- "Group API Developer Portal": ein Login für alle Webservices von Deutsche Post und DHL (Versandlabel erstellen, Sendungsstatus abfragen u. a.) — [Developer Portal Info](https://www.dhl.de/de/geschaeftskunden/paket/versandsoftware/group-api-developer-portal.html)
- DHL-Partnersysteme (Auswahl): Shopify-App, Shopware, Sendcloud, 8returns (Retourenportal mit DHL-Retourenlabels), V-LOG, AEB; **Wix wird in der DHL-Partnerliste nicht genannt** — [Partnersysteme](https://www.dhl.de/de/geschaeftskunden/paket/versandsoftware/partnersysteme.html)
- DHL Express "Collect & Return" (Reparaturen & Rückführungen): Abholung defekter Geräte beim Endkunden per Schnittstelle/Weblösung buchbar, Kurier bringt das Label mit, Schutzverpackung gegen Aufpreis, konsolidierte Abrechnung; erfordert DHL-Express-Kundenaccount/Vertriebskontakt — [Reparaturen & Rückführungen](https://www.dhl.de/de/geschaeftskunden/express/business-loesungen/reparaturen-und-rueckfuehrungen.html)

**DHL Geschäftskunden-Preise/APIs [Auszug]**
- Geschäftskundenpreise sind individuell; Preiserhöhung zum 01.01.2026; seit 01.07.2025 Monatspauschale für DHL Paket und DHL Retoure je nach Tarif 7,95–119,95 EUR; Peakzuschlag 0,19 EUR/Sendung im Nov./Dez. — [DHL Group Pressemitteilung](https://group.dhl.com/de/presse/pressemitteilungen/2025/dhl-paket-erhoeht-preise-fuer-geschaeftskunden.html), [Händlerbund](https://ohn.haendlerbund.de/logistik/paketdienste/preiserhoehung-dhl-geschaeftskunden-2026)
- DHL-Mustervertrag (Anlage 1): Beispiel-Staffelpreise bis 5 kg 5,63 EUR, bis 31,5 kg 11,02 EUR netto je Stück (Muster, keine verbindliche Liste) — [DHL Muster Anlage 1](https://www.dhl.de/dam/jcr:a8c3b457-442c-40da-84a3-1aee254f1c78/dhl-muster-anlage-1-vemo-vertrag-de-0824.pdf)
- Parcel DE Shipping API v2 ("Post & Parcel Germany"): benötigt EKP (Kundennummer) und 14-stellige Abrechnungsnummer (Stellen 11–12 = Produkt), Produkte u. a. V01PAK (DHL Paket), V53WPAK (International), V54EPAK (Europaket); Sandbox `api-sandbox.dhl.com/parcel/de/shipping/v2/` auch ohne Geschäftskundenvertrag nutzbar; Labelausgabe als PDF — [developer.dhl.com Shipping v2](https://developer.dhl.com/api-reference/parcel-de-shipping-post-parcel-germany-v2?language_content_entity=en), [OpenAPI-Kopie](https://github.com/kruegge82/dhl-php-rest-sdk/blob/main/parcel-de-shipping-v2_1_11.yaml)
- Parcel DE Returns API: `receiverId` aus dem Geschäftskundenportal (Retoure → Einstellungen → "Receiver ID"); `labelType` = SHIPMENT_LABEL, QR_LABEL oder BOTH; Authentifizierung zweistufig (API-Key aus dem Developer Portal + Geschäftskundenportal-Zugang); Produktivfreigabe nach Sandbox-Test durch DHL; alle Bereitstellungsarten sind Bestandteil des DHL-Geschäftskundenvertrags — [developer.dhl.com Returns](https://developer.dhl.com/api-reference/parcel-de-returns-post-parcel-germany), [DHL SDK](https://packagist.org/packages/dhl/sdk-api-parcel-de-returns)
- Es existiert zusätzlich eine "DHL Parcel DE Private Shipping"-API (Privatkunden-Frankierung) im Developer Portal — [developer.dhl.com Private Shipping](https://developer.dhl.com/api-reference/dhl-parcel-de-private-shipping-post-parcel-germany)

**Wix [Auszug]**
- "Wix Shipping" (nativ, powered by Shippo) ist in Deutschland verfügbar; Carrier für Deutschland: Deutsche Post und DPD Germany (DHL Paket nicht gelistet); Labeldruck startet aus einer unerfüllten Wix-Stores-Bestellung — [Wix Shipping](https://support.wix.com/en/article/wix-stores-printing-shipping-labels-with-wix-shipping), [About Shipping Labels](https://support.wix.com/en/article/wix-stores-about-shipping-labels)
- Sendcloud-App im Wix App Market (160+ Carrier inkl. DHL, UPS); laut Wix für Händler in Deutschland verfügbar; laut Sendcloud DHL-Versand ohne eigenen DHL-Vertrag über Sendcloud-Tarife möglich, alternativ eigener DHL-Vertrag über Geschäftskundenportal-Zugang (Systemuser) anbindbar — [Wix App Market Sendcloud](https://www.wix.com/app-market/sendcloud), [Sendcloud Wix–DHL](https://www.sendcloud.com/carrier-integrations/wix-dhl/), [Sendcloud DHL-Vertrag](https://support.sendcloud.com/hc/en-us/articles/360025834332-DHL-contract-activation-Germany)
- Shippo-App für Wix (Labels national/international) — [Wix Shippo-App](https://support.wix.com/en/article/wix-stores-printing-shipping-labels-with-the-shippo-3rd-party-app)
- DHL hat keine native Wix-Integration; Anbindung über Drittanbieter-Apps (Sendcloud, Outvio, Shiplemon, Shippo) (Sekundärquelle) — [parcelpath](https://parcelpath.com/ecommerce/wix/wix-shipping-labels/dhl-wix/)

### Inferences
- Kostenrahmen Einsendung einer Mechatronik (5–10 kg) ohne Vertrag: DHL Paket 10 kg 10,49 € + Transportversicherung bis 2.500 € 6,99 € = 17,48 € je Richtung (Listenpreis 2026); Express bis 10 kg 30,00 €, mit Samstagszustellung 41,90 €. Die Standardhaftung von 500 € liegt unter dem Wert einer Mechatronik, daher Versicherung einplanen; versicherte Pakete nicht über Packstation.
- Drei Umsetzungsstufen für "Label für den Kunden": (1) **manuell**: OZ kauft nach Formulareingang ein Label in der DHL Online Frankierung (Absender = Kunde, Empfänger = OZ) und mailt PDF/QR — sofort möglich, kein Vertrag; (2) **Aggregator**: Sendcloud (Return-Portal bzw. API) erzeugt Rücksendelabels zu Aggregator-Tarifen, ohne eigenen DHL-Vertrag; (3) **DHL direkt**: Geschäftskundenvertrag (≥ ca. 200 Sendungen/Jahr, Monatspauschale) + DHL Retoure (Retourenportal-Link oder Returns-API mit PDF/QR) — aus Wix per Velo-Backend (HTTP-Funktion, API-Key in Secrets) aufrufbar.
- Wix-Label-Apps sind an Wix-Stores-Bestellungen gebunden und für **ausgehende** Sendungen gedacht; ein Konfigurator-Formular ohne Stores-Bestellung erzeugt damit kein Kundenlabel. Entweder Reparatur als Stores-Produkt anlegen oder Label außerhalb (Sendcloud/DHL-Portal/API) erzeugen.
- ecu.de löst die Einsendung per DHL-Express-Abholung (10 € netto, 1.500 € versichert) — vergleichbar mit DHL Paket + Abholung (+3,00 €) + Versicherung, aber schneller.

### Gaps
- developer.dhl.com war nicht direkt lesbar (403); API-Details stammen aus Suchauszügen und SDK-Dokumentation. Produktcode für DHL Retoure in der Shipping-API, aktuelle Sandbox-Matrix und Zulassungsprozess nicht verifiziert.
- Verbindliche Geschäftskundenpreise 2026 (5/10/31,5 kg) und Preis je DHL-Retoure: nur individuell über DHL; keine öffentliche Liste.
- MyDHL API (DHL Express) für Abhol-/Importlabels: nicht recherchiert über die dhl.de-Express-Seite hinaus; erfordert Express-Kundennummer (nicht belegt).
- Ob DHL unter 200 Sendungen/Jahr einen Geschäftskundenvertrag abschließt: DHL nennt "etwa 200 Sendungen oder mehr"; Kulanz nicht belegt.
- Wix-App-Market-Verfügbarkeit/Preise von Sendcloud, Shippo, Outvio für Deutschland im November 2026 nicht direkt geprüft (wix.com nicht erreichbar); ob diese Apps Retouren-/Einsendelabels ohne Stores-Bestellung erlauben, ist nicht belegt.
- Neue DHL-Privatkundenpreise ab 01.01.2027 sind angekündigt, Beträge nicht erfasst.
