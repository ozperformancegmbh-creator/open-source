# Technik-Faktenbasis: VW P1735 / DSG-Fehlercodes und Getriebespülung (Stand November 2026)

**Methodischer Hinweis (wichtig für die Einordnung aller Angaben):** In dieser Sitzung war der direkte Seitenabruf (WebFetch) für alle getesteten Hosts gesperrt (u. a. wiki.ross-tech.com, aftermarket.zf.com, motor-talk.de, autoservicepraxis.de, ecu.de, az-teile.de, kfz-dietrich.com, ecutesting.com). Alle Befunde stammen daher aus Suchergebnis-Auszügen (Snippets/Zusammenfassungen), nicht aus vollständig gelesenen Seiten. Kein einziges Hersteller-Originaldokument (VW-TPI, ODIS-Text, Mercedes-Wartungsblatt, ZF-Serviceinformation im Volltext) konnte geöffnet werden. Konfidenz-Skala: **hoch** = mehrere unabhängige Quellen übereinstimmend; **mittel** = mehrere Quellen, aber alle interessengeleitet (Reparaturanbieter) oder nur Snippet; **niedrig** = Einzelquelle/Forum/Blog. Vor Veröffentlichung sollten die mit "prüfen" markierten Punkte von OZ Performance selbst gegen ODIS/ISTA/XENTRY bzw. ZF-Unterlagen verifiziert werden – das ist zugleich die beste Quelle für eigene, zitierfähige Aussagen.

Mehrere Treffer stammen von kfz-dietrich.com (sehr viele, schematisch aufgebaute Blogartikel mit auffällig präzisen, nirgends belegten Zahlen wie "±0,3 bar Toleranzgrenze"). Diese Quelle wird hier nur als Hinweis geführt, nicht als Beleg.

---

## 1. Was bedeutet P1735 im VW-Konzern – und unterscheidet sich die Bedeutung je Getriebe/Hersteller?

### Takeaway
Im VW-Konzern ist P1735 (ODIS-Schreibweise P173500, VAG-Nummer 10666) praktisch durchgängig als "Positionsgeber/Geber 1 für Kupplung(sposition) – elektrischer Fehler" belegt und tritt fast ausschließlich beim nassen 7-Gang-DSG DQ381 (0GC) und beim DQ500 (0BH/0BT) auf; P1736 (P173600 / 10668) ist das Pendant für Kupplung 2. Die im Briefing vermuteten Deutungen "18143", "Kupplungssteller" oder "Toleranzgrenze erreicht" ließen sich für P1735 NICHT belegen; bei anderen Herstellern bedeutet P1735 etwas völlig anderes.

### Cited Findings
- VW-Fehlertext laut Reparaturanbieter: "P1735 (10666) Positionsgeber Kupplung …" für DQ381/DQ500; der Anbieter ordnet den Fehler einem elektrischen Defekt im Druck-/Wegsensor der Getriebemechatronik zu, nicht einem mechanischen Kupplungssensor (Konfidenz: mittel) — [ecu.de](https://ecu.de/druck-wegsensor-dq381-dq500-312.htm)
- Schreibweise mit Fehlerart-Suffix: "P173500 (10666) – Geber 1 für Kupplungsposition: Elektrischer Fehler (Kupplung K1)" und "P173600 (10668) – Geber 2 für Kupplungsposition: Elektrischer Fehler (Kupplung K2)", zugeordnet DQ381/DQ500 (Konfidenz: niedrig als Einzelquelle, aber deckungsgleich mit den übrigen) — [kfz-dietrich.com](https://kfz-dietrich.com/blog/vw-audi-dsg-mechatronik-defekt-dq200-dq250-dq381-diagnose/)
- Motor-Talk-Thread mit genau diesem Fehlerbild trägt den Titel "DSG Getriebefehler 10668 – Positionsgeber für Kupplung 2" (bestätigt die VAG-Nummer 10668 = P1736 aus einem realen Fall) (Konfidenz: mittel) — [motor-talk.de](https://www.motor-talk.de/forum/dsg-getriebefehler-10668-positionsgeber-fuer-kupplung-2-t7614389.html)
- Englische Fassung: "P1735 – Position Sensor For Clutch 1 Electrical Malfunction; P1736 – Position Sensor For Clutch 2 Electrical Malfunction", DQ381 (Konfidenz: mittel) — [ecutesting.com](https://www.ecutesting.com/common-faults/volkswagen/dq381-mechatronic-causing-tiguan-dsg-gearbox-problems/)
- Weitere Anbieter führen dieselbe Codegruppe für DQ381/DQ500: P1735, P1736, 10666, 10668, häufig zusammen mit P0607, P175D, P175E, P176E, P176F — [dias-automotive-engineering.com](https://dias-automotive-engineering.com/dq500-dq381-mechatronik-reparatur-fehler-p1735-p1736-10666-10668-beheben/); [compramas-shop.de](https://compramas-shop.de/blogs/getriebesteuergerat-fehler-diagnose-und-reparatur/dq381-getriebesteuergerat-defekt-reparatur-bei-p1735-p1736-p175d-p175e-p176e-und-p176f); [motronik-service.de](https://motronik-service.de/vw/vw-getriebesteuergeraet/dsg-7-gang-dq381-dq500-mechatronik/p1735-p1736-positionsgeber-kupplung-1-2-elektrischer-fehler/)
- Ross-Tech-Wiki: Für "18143/P1735" wurde keine Wiki-Seite gefunden. Die Wiki nutzt das Format "18148/P1740/005952" für benachbarte Codes; rechnerisch läge P1735 im alten 5-stelligen VAG-Schema bei 18143, belegt ist das nicht — [wiki.ross-tech.com (Beispiel 18148/P1740)](https://wiki.ross-tech.com/wiki/index.php/18148/P1740/005952)
- Angehängte Ziffern, die manche Auslesegeräte hinter dem Code zeigen, sind Fehlertyp/Statusbyte und gehören nicht zum Code selbst (Konfidenz: niedrig, Einzelquelle) — [az-teile.de](https://www.az-teile.de/dsg-fehlercodes-dq200-dq250-dq500-erklaert/)
- "Toleranzgrenze" ist als DSG-Fehlertext belegt, aber unter einem ANDEREN Code: Praxisfall Skoda Octavia mit DQ200, nach Kupplungstausch Eintrag "P177B Toleranzgrenze" für Kupplung K1 — [autoservicepraxis.de (FabuCar-Fall, PDF)](https://www.autoservicepraxis.de/downloadfile/3792057/90007_2026_30_04_I_042_n40_FabuCar-Fall_172519_print.pdf)
- Opel Easytronic: P1735 bedeutet dort, dass die Getriebeparameter nicht korrekt angelernt wurden; laut Quelle häufig bei Corsa C/D und Meriva A (Konfidenz: niedrig, Anbieter) — [repairfirst.de](https://repairfirst.de/pages/fehlercodes/getriebe0130-p1735-easytronic)
- GM (4T65E/4T60E): Bezug auf 2-3-Schaltventil; Nissan (Sentra/Altima): "First Gear Switch Circuit Malfunction"; Honda: hängendes Schaltmagnetventil/Hydrauliksteuerung (Konfidenz: niedrig, generische OBD-Sammelseite) — [go-parts.com](https://www.go-parts.com/garage/obd-p1735)
- Hyundai: Bezug auf "Speed Sensor Reference"-Stromkreis (hoch) (Konfidenz: niedrig) — [engine-codes.com](https://www.engine-codes.com/p1735.html)
- Generische Ratgeberseite zu P1735 als herstellerspezifischem Code — [club.autodoc.de](https://club.autodoc.de/obd-codes/p1735)

### Inferences
- P1xxx-Codes sind per SAE-Definition herstellerspezifisch; die Seite sollte das gleich im ersten Absatz sagen ("P1735 bei VW/Audi/Seat/Skoda/Cupra = Geber 1 Kupplungsposition, DQ381/DQ500 – bei Opel, GM, Nissan, Honda, Hyundai etwas anderes"). Das ist ein klarer Genauigkeitsvorsprung gegenüber generischen OBD-Seiten.
- Das Wort "Positionsgeber" ist irreführend: Bei den nassen Getrieben DQ381/DQ500 gibt es keinen Kupplungswegsensor wie beim trockenen DQ200; mehrere Anbieter verorten den Fehler bei den Kupplungs-Drucksensoren auf der Mechatronik. Genau diese Erklärung ("warum heißt es Positionsgeber, obwohl ein Drucksensor getauscht wird?") fehlt auf den meisten Seiten und ist eine Chance.
- Für DQ200 (0AM/0CW) und DQ250 (02E) wurde P1735 in keinem Treffer als typischer Code genannt. Die Seite sollte nicht behaupten, P1735 sei ein DQ200-Fehler.
- Empfehlung: beide Schreibweisen (P1735, P173500) und beide VAG-Nummern (10666, 10668) auf der Seite nennen – Nutzer suchen nach dem, was ihr Tester anzeigt.

### Gaps
- Offizieller ODIS-/VCDS-Wortlaut im Original nicht verifiziert (Ross-Tech-Wiki und VW-Unterlagen nicht abrufbar). OZ Performance sollte einen eigenen ODIS-Screenshot/Protokollauszug beisteuern. **prüfen**
- Ob 18143 tatsächlich als alte VAG-Nummer zu P1735 existiert und welchen Text sie bei älteren Getrieben (z. B. 01M/09G/02E) trägt: nicht belegt.
- Mercedes und Ford: keine Belege für eine P1735-Belegung gefunden.
- Kein VW-TPI mit Nummer zu P1735/P1736 gefunden.

---

## 2. P1735: Symptome, Ursachen, betroffene Modelle, Diagnose, Reparatur, Kosten, Weiterfahren, Rückrufe/Kulanz

### Takeaway
P1735/P1736 gilt übereinstimmend als Hardwarefehler der Mechatronik (driftende Kupplungs-Drucksensoren bzw. Elektronikdefekt), der ein Teilgetriebe abschaltet; ein Softwareupdate behebt ihn laut Anbietern nicht. Belegte Preise gibt es nur für Elektronik-/Sensorreparaturen (ca. 299–339 € netto/brutto je nach Anbieter); für Kupplungstausch, Komplettmechatronik und Händlerpreise fehlen belastbare Quellen. Ein offizieller Rückruf zu P1735 wurde nicht gefunden.

### Cited Findings
**Symptome**
- Bei gespeichertem P1735 geht die Funktion der ungeraden Gänge 1, 3, 5, 7 verloren (Teilgetriebe 1); entsprechend P1736 = gerade Gänge (Konfidenz: mittel) — [ecutesting.com](https://www.ecutesting.com/common-faults/volkswagen/dq381-mechatronic-causing-tiguan-dsg-gearbox-problems/)
- Fahrzeug "fährt verzögert an, schaltet ruckartig, geht ab und zu in den Notlauf"; Abschaltung einer Kupplung, sodass nur ein Teil der Gänge verfügbar ist, "fast immer wegen P1735 oder P1736" (Konfidenz: mittel) — [kfz-reparatur24.de](https://kfz-reparatur24.de/leistungen/p1735-p1736-dsg-reparatur/); [az-teile.de](https://www.az-teile.de/dsg-getriebe-defekt-symptome-ursachen/)

**Ursachen (Quellen uneinig über das genaue Bauteil)**
- Variante A – Drucksensoren: elektrischer Defekt der Drucksensoren in der Mechatronik; genannter Sensortyp SMP132-532; Empfehlung, beide Sensoren zu tauschen — [ecu.de](https://ecu.de/druck-wegsensor-dq381-dq500-312.htm); [transmission-online.shop](https://www.transmission-online.shop/shop/Steuergerat-Reparatur-Positionsgeber-fur-Kupplung-1und-2-DSG-7-Gang-DQ381-DQ500-p734916336)
- Forenbeobachtung dazu: "Die Drucksensorwerte driften ins Minus und bei einem Offset von ca. −0,75 bar meldet DSG einen Fehler" (Konfidenz: niedrig, einzelner Forenbeitrag, aber plausibler Mechanismus) — [motor-talk.de](https://www.motor-talk.de/forum/dsg-dq381-mechatronik-reparatur-t7490016.html)
- Variante B – Steuergerät: interne Defekte des Getriebesteuergeräts, nicht die Kupplung selbst; genannt werden beschädigte Leiterbahnen, kalte Lötstellen, Kabelbruch/Kurzschluss im Kabelbaum — [motronik-service.de](https://motronik-service.de/vw/vw-getriebesteuergeraet/dsg-7-gang-dq381-dq500-mechatronik/p1735-p1736-positionsgeber-kupplung-1-2-elektrischer-fehler/); [dsg-getriebe-reparatur.de](https://www.dsg-getriebe-reparatur.de/)
- Drucksensortausch am DQ381 ist als eigenständige Reparatur dokumentiert — [langwieser-performance.at](https://www.langwieser-performance.at/2024/04/10/drucksensor-tausch-dq381-7-gang-dsg/)
- Das DQ381/DQ500-Steuergerät ist (Stand 31.10.2026) als neues Bosch-Originalteil im freien Handel erhältlich; der Anbieter rät ausdrücklich, vor einem Tausch eine Fehlerdiagnose durchzuführen, da auch andere Ursachen möglich sind — [langwieser-performance.at](https://www.langwieser-performance.at/2026/10/31/dq381-dq500-dsg-steuergeraet-jetzt-als-neues-bosch-originalteil-erhaeltlich/)
- Fehler sei hardwarebedingt, ein Softwareupdate helfe nicht; bei massiven mechanischen Schäden (Kupplungsverschleiß, Metallabrieb im Hydrauliksystem) reiche eine reine Steuergerätereparatur nicht (Konfidenz: mittel, Anbieteraussagen) — [repairfirst.de](https://repairfirst.de/pages/fehlercodes/getriebe0129-p1735-dq381); [compramas-shop.de](https://compramas-shop.de/blogs/getriebesteuergerat-fehler-diagnose-und-reparatur/dq381-getriebesteuergerat-defekt-reparatur-bei-p1735-p1736-p175d-p175e-p176e-und-p176f)

**Betroffene Modelle**
- Genannt: VW Golf 7, Tiguan, Passat; Audi A3, Q3, TT; Seat Leon, Ateca; Skoda Octavia, Kodiaq – jeweils mit DQ381 oder DQ500 — [kfz-reparatur24.de](https://kfz-reparatur24.de/leistungen/p1735-p1736-dsg-reparatur/)
- Skoda Kodiaq und VW Tiguan als eigene Fehlerbild-Seiten — [ecutesting.com (Kodiaq)](https://www.ecutesting.com/common-faults/skoda/skoda-kodiaq-dq381-mechatronic-fault/)
- Neuere Modelle (Tiguan, Passat B9, Golf 8) werden ebenfalls genannt — [repairfirst.de](https://repairfirst.de/collections/dq381-reparatur-austausch)
- Audi-Praxisfall DQ381/0GC — [herzdrive.com](https://herzdrive.com/unsere-arbeiten/audi-dsg-dq381-0gc-reparatur/)

**Kosten (nur diese Werte sind belegt)**
- Steuergerätereparatur: 299 € bei einem Anbieter — [kfz-reparatur24.de](https://kfz-reparatur24.de/leistungen/p1735-p1736-dsg-reparatur/)
- DQ381-Mechatronikreparatur "ab 339 €" zzgl. MwSt., 2 Jahre Garantie — [repairfirst.de](https://repairfirst.de/collections/dq381-reparatur-austausch)
- Angebot regionaler Reparatur (Hanau) für P1735/P1736/10666/10668/P0607 — [kleinanzeigen.de](https://www.kleinanzeigen.de/s-anzeige/p1735-p1736-dsg-reparatur-dq381-dq500-kupplungspositionsgeber/2246618536-280-4283)

**Weiterfahren**
- Weiterfahren im Notlauf ist kurzfristig möglich, aber nicht empfehlenswert, weil nur eine Kupplung arbeitet und der Verschleiß steigt (Konfidenz: mittel, Anbieter) — [repairfirst.de](https://repairfirst.de/pages/fehlercodes/getriebe0129-p1735-dq381)

**Kulanz / Rückrufe**
- Motor-Talk-Fall: Kulanzantrag bei VW abgelehnt (Fahrzeug zu alt, zu viele Kilometer); danach Mechatronik repariert, beide Positionssensoren getauscht (Konfidenz: niedrig, Einzelfall) — [motor-talk.de](https://www.motor-talk.de/forum/dsg-getriebefehler-10668-positionsgeber-fuer-kupplung-2-t7614389.html)
- DQ200 (nicht P1735!): Skoda-/VW-Serviceaktion 34H5 ist ein Software-Update des Getriebesteuergeräts, Freigabedatum laut Forum 12.01.2017, betroffen 7-Gang-DSG DQ200 etwa Baujahre 2013–2015; Zweck laut Forum: Maximaldruck im Hydrauliksystem senken, um Risse/Undichtigkeiten am Druckspeicher zu vermeiden; Dauer 30–60 min (Konfidenz: niedrig–mittel, nur Forenangaben) — [skodacommunity.de](https://www.skodacommunity.de/threads/rueckrufaktion-fuer-octavia-3-7-gang-dsg-aktion-34h5.112329/)
- Auto Bild titelte zu den DQ200-Problemen: "Kein offizieller Rückruf von Volkswagen" (Deutschland) — [autobild.de](https://www.autobild.de/artikel/vw-probleme-mit-dsg-4559939.html)
- Handelsblatt zum DSG-Rückruf (China/Asien): "Das Problem ist der Schwefel" (Ölthema, Umstellung synthetisch → mineralisch) — [handelsblatt.com](https://www.handelsblatt.com/mobilitaet/motor/dsg-rueckruf-bei-vw-das-problem-ist-der-schwefel/9076570.html)
- Sekundärquelle: Ölaktion (synthetisches gegen mineralisches Öl), Februar 2014, freiwillig, "kein offizieller Rückruf", ca. 257.000 Fahrzeuge in Deutschland; für Italien wird eine Druckspeicher-Kampagne für DQ200 10/2008–11/2014 genannt, für Deutschland unklar (Konfidenz: niedrig) — [carwiki.de](https://carwiki.de/vw-dsg-probleme/)

### Inferences
- Sinnvolle Diagnose-Reihenfolge für die Seite (aus den Quellen abgeleitet, als Werkstatt-Vorgehen zu formulieren und von OZ zu bestätigen): (1) Fehlerspeicher vollständig mit Umgebungsdaten auslesen, P1735 vs. P1736 und Begleitcodes (P0607, P175D/E, P176E/F) notieren; (2) Messwerte der Kupplungs-Drucksensoren K1/K2 im Stand drucklos prüfen (Offset; laut Forum Fehler bei ca. −0,75 bar); (3) Stecker/Kabelbaum/Spannungsversorgung der Mechatronik prüfen; (4) Ölzustand/Abrieb prüfen, um mechanischen Schaden auszuschließen; (5) erst dann Sensor- bzw. Mechatronikreparatur; (6) anschließend Grundeinstellung/Adaption.
- Kostenkommunikation: Da nur Elektronik-Einsendepreise (ca. 300–400 €) belegt sind, sollte OZ eigene Festpreise inkl. Aus-/Einbau, Öl und Grundeinstellung nennen – das wäre der erste belastbare Komplettpreis im deutschen Web und sehr zitierfähig.
- Die im Briefing genannte "DQ200-Druckspeicher-Rückrufaktion 2019+" konnte nicht bestätigt werden; belegt ist lediglich die Serviceaktion 34H5 (Software, 2017). Auf der Seite nicht als "Rückruf 2019" darstellen.

### Gaps
- Baujahr-Fenster und betroffene Teilenummern-Stände der DQ381-Mechatronik: nicht belegt.
- Preise für Komplettmechatronik neu (Händler), Kupplungstausch DQ381/DQ500, Händler-Stundensätze: keine Quelle gefunden. **prüfen / eigene Preise einsetzen**
- VW-TPI oder Kulanzregelung speziell zu P1735/P1736: nichts gefunden.
- Konkrete Messwertblock-/Grundeinstellungs-Nummern (ODIS-geführte Funktion, VCDS-Kanäle) für DQ381: nicht belegt.
- Weltweite Zahlen zur DQ200-Ölaktion 2013/14 (aus dem Gedächtnis: ca. 1,6 Mio. Fahrzeuge weltweit, 384.000 in China) konnten in dieser Sitzung nicht mit Quelle belegt werden – nur nach Prüfung des Handelsblatt-/Auto-Bild-Artikels verwenden.
- KBA-Rückrufdatenbank wurde nicht abgefragt.

---

## 3. Benachbarte Fehlercodes mit Potenzial für eigene Seiten (DSG/S-Tronic, ZF 6HP/8HP, Mercedes 722.9/9G)

### Takeaway
Am besten belegt und am häufigsten genannt sind beim DSG das Paar P17BF/P189C (DQ200-Hydraulikdruck/Druckspeicher), P0841, P173A–P173D, P1736, P0607 und P175D; bei Mercedes 722.9 die Drehzahlsensor-Codes 0717/0718/0722/0723. Die Bedeutungsangaben stammen fast nur von Reparaturanbietern und widersprechen sich teilweise – jede Codeseite braucht den Original-ODIS/XENTRY/ISTA-Text aus der eigenen Werkstatt.

### Cited Findings
**VW-Konzern DSG / S-Tronic**
- P1736 (P173600 / 10668): Geber 2 für Kupplungsposition, elektrischer Fehler, DQ381/DQ500 — [motor-talk.de](https://www.motor-talk.de/forum/dsg-getriebefehler-10668-positionsgeber-fuer-kupplung-2-t7614389.html)
- P17BF: "Überlastschutz Hydraulikpumpensystem" / Hydraulikpumpe erreicht Abschaltdruck nicht; DQ200; tritt typischerweise mit P189C auf — [actronics-gmbh.de](https://www.actronics-gmbh.de/neuigkeit/diagnosehilfe/vag-fehlercodes-p17bf-p189c); [actronics.co.uk](https://www.actronics.co.uk/dq200-dsg-p17bf-p189c-fault-codes-tcu-repair)
- P189C: unzureichender Druckaufbau / "Funktionseinschränkung durch Druckabfall" (DQ200); abweichende Deutungen in anderen Quellen ("Keine Kommunikation mit dem TCM", "Kupplungsdruck K2 unplausibel") – Quellen uneinig — [actronics-gmbh.de](https://www.actronics-gmbh.de/acinsights/tcu-dsg7-dq200); [az-teile.de](https://www.az-teile.de/dsg-fehlercodes-dq200-dq250-dq500-erklaert/)
- Merksatz aus Anbieterquelle: "Beim DQ200 führen P17BF und P189C fast immer zum Druckspeicher"; Dauerlauf der Hydraulikpumpe + beide Codes = undichter Druckspeicher; bei gerissenem Gewinde Reparatursatz mit verstärktem Gehäuse (Teilenummer 0AM325587E/F) — [az-teile.de](https://www.az-teile.de/dq200-mechatronik-reparieren-oder-tauschen/); [getriebeshop24.de](https://getriebeshop24.de/blogs/news/druckspeicher-fur-dsg-getriebe-erklart-probleme-und-losungen)
- Hydraulikdruckverlust DQ200: Risse im Aluminium-Druckgussgehäuse oder defekter Dichtring — [mosertronik.com](https://mosertronik.com/en/dsg-mechatronics-repair-austria/)
- P0841: Getriebeöl-Drucksensor, Signal unplausibel (Mehrheit); eine Liste nennt abweichend "Steuermodul defekt" — [az-teile.de](https://www.az-teile.de/dsg-fehlercodes-dq200-dq250-dq500-erklaert/)
- Typische DQ250-Codes laut Anbieter: P17BF, P189C, P0841, P0871, P0717 — [kfz-dietrich.com](https://kfz-dietrich.com/blog/dq250-mechatronik-probleme-symptome-diagnose-reparatur/)
- P173A–P173D: Gangpositionssensoren (Wegsensoren Gangsteller) 1–4, Signal unplausibel, DQ200; häufige Ursache Metallabrieb an Sensoren/Magneten; eine andere Seite ordnet P173A/B abweichend der "Kupplungsregelung" zu — [langwieser-performance.at](https://www.langwieser-performance.at/2023/01/24/wegsensor-problem-signal-unplausibel-dq200-7-gang-dsg-unser-neues-video-zu-diesen-thema/); [getriebeprofi-rostock.de](https://getriebeprofi-rostock.de/dsg/)
- P072C: "Gang nicht einlegbar" (elektronische oder hydraulische Ansteuerungsstörung) (Konfidenz: niedrig, Einzelquelle) — [getriebeprofi-rostock.de](https://getriebeprofi-rostock.de/dsg/)
- P17E1: Gangsteller 2, mechanischer Fehler; laut Teileseite DQ501 (Konfidenz: niedrig) — [az-teile.de](https://www.az-teile.de/dsg-fehlercodes-dq200-dq250-dq500-erklaert/)
- P177B: "Toleranzgrenze" Kupplung K1 (DQ200, nach Kupplungstausch gesetzt) — [autoservicepraxis.de](https://www.autoservicepraxis.de/downloadfile/3792057/90007_2026_30_04_I_042_n40_FabuCar-Fall_172519_print.pdf)
- P175D: eigener DSG-Mechatronikfehler (DQ381) mit eigener Fehlerbildseite — [ecutesting.com](https://www.ecutesting.com/common-faults/volkswagen/vw-p175d-dsg-fault/)
- P0805: DQ381/DQ380-Mechatronik-Steuergerätefehler — [actronics.co.uk](https://www.actronics.co.uk/p0805-vw-audi-dsg-fault)
- 01315 (VAG): DQ200-Steuergerät (Kommunikation Getriebesteuergerät) — [actronics.co.uk](https://www.actronics.co.uk/vag-fault-code-01315-dq200)
- 19143/P2711: existiert als Ross-Tech-Wiki-Eintrag (DSG-relevant; Wortlaut nicht abrufbar) — [wiki.ross-tech.com](https://wiki.ross-tech.com/wiki/index.php/19143/P2711/010001)
- 18148/P1740: Ross-Tech-Eintrag zur Kupplungstemperatur-Überwachung — [wiki.ross-tech.com](https://wiki.ross-tech.com/wiki/index.php/18148/P1740/005952)
- DQ500-Fallthread: nach fehlgeschlagener Grundeinstellung nur noch ungerade Gänge, Codes P074A, P18BA, P0607 — [tx-board.de](https://tx-board.de/threads/dq500-nach-fehlgeschlagener-grundeinstellung-nur-noch-ungerade-gaenge-p074a-p18ba-p0607.173840/)
- Ross-Tech-Übersichtsseiten je Getriebe (02E/0D9, 0B5 S-Tronic) — [wiki.ross-tech.com 02E](https://wiki.ross-tech.com/wiki/index.php/6-Speed_Direct_Shift_Gearbox_(DSG/0D9)); [wiki.ross-tech.com 0B5](https://wiki.ross-tech.com/wiki/index.php/7-Speed_S-Tronic_Direct-Shift_Gearbox_(DSG/0B5))

**ZF 6HP / 8HP (BMW, Audi u. a.)**
- P0741: Wandlerüberbrückungskupplung – Leistung/dauerhaft offen; typisch für 6HP und 8HP; Symptom Vibration bei ca. 60–80 km/h im Lock-up (Konfidenz: mittel) — [trnw.net](https://trnw.net/z-search/ZF8HP45.php); [bmw-diagnose.kfz-dietrich.com](https://bmw-diagnose.kfz-dietrich.com/automatik/)
- P0730 (und gangbezogen P0731–P0738): falsche Übersetzung / interner Schlupf — [jgmecatech.fr](https://jgmecatech.fr/boites-auto/la-boite-8hp-zf/)

**Mercedes 722.9 (7G-Tronic)**
- Häufigste Codes: 0717, 0718 (Drehzahlsensor Y3/8n1: kein Signal bzw. Sensor defekt), 0720 (Abtriebsdrehzahlsensor), 0722, 0723 sowie mehrere 22xx-/27xx-Codes; Getriebe geht häufig in den Notlauf; Ursache sitzt auf der Leiterplatte des Steuergeräts (EHS/VGS) — [actronics-gmbh.de](https://www.actronics-gmbh.de/getriebesteuergerat/continental-7g-tronic-722-9-first-second-and-third-generation)
- Weitere 722.9-Codes in englischer Übersicht: P0700, P0748, P0778, P2810, P2759, U0101 — [fcpeuro.com](https://www.fcpeuro.com/blog/the-definitive-guide-to-the-mercedes-722-9-7g-tronic-transmission)

### Inferences
- Priorisierung für nächste Codeseiten (nach Belegdichte und Suchnähe): 1) P1736; 2) P17BF; 3) P189C; 4) P0841; 5) P173A–D als Sammelseite; 6) P0607 (DSG-Steuergerät); 7) P175D/P175E/P176E/P176F (DQ381-Sammelseite); 8) P177B/"Toleranzgrenze erreicht"; 9) P072C; 10) Mercedes 0717/0718 (Y3/8n1, Y3/8n2); 11) ZF P0741 Wandlerkupplung; 12) ZF P0730-Familie; 13) 01315.
- Wegen der widersprüchlichen Anbieterangaben (P189C, P0841, P173A) ist ein "So lautet der Text in ODIS – so interpretieren ihn andere Seiten falsch"-Abschnitt ein starkes Differenzierungsmerkmal.

### Gaps
- Keine Belege gefunden für: P173B (einzeln), P1895, P0746, P17D8, P177F, P2711-Wortlaut, P0715 im DSG-Kontext. Nicht mit erfundenen Bedeutungen füllen.
- BMW-eigene Hex-Codes für ZF 6HP/8HP (z. B. Übersetzungsüberwachung, Kupplung E) und Audi-ZF-Codes: keine Treffer.
- Mercedes Y3/8n2 (Code 0718-Zuordnung unsicher: Quelle ordnet 0717 UND 0718 Y3/8n1 zu), 722.6-typische Fehler (Leitblech, Steckergehäuse) und 9G-Tronic (725.0) Fehlercodes: keine Belege gefunden.
- Suchvolumen-Daten je Code liegen nicht vor (kein Keyword-Tool genutzt); "am häufigsten gesucht" ist hier über Häufigkeit der Anbieterseiten angenähert.

---

## 4. Reale Nutzerfragen zu P1735 (Foren)

### Takeaway
Wörtliche Forenfragen konnten wegen der Abrufsperre nicht gesammelt werden; belegt sind nur Thread-Titel. Die Zielzahl von 15–25 wörtlichen Formulierungen wurde NICHT erreicht – die untenstehende zweite Liste sind aus den Quelleninhalten abgeleitete Fragen und ausdrücklich keine Zitate.

### Cited Findings
- Thread-Titel (wörtlich): "DSG Getriebefehler 10668 – Positionsgeber für Kupplung 2" — [motor-talk.de](https://www.motor-talk.de/forum/dsg-getriebefehler-10668-positionsgeber-fuer-kupplung-2-t7614389.html)
- Thread-Titel (wörtlich): "DSG DQ381 Mechatronik Reparatur" — [motor-talk.de](https://www.motor-talk.de/forum/dsg-dq381-mechatronik-reparatur-t7490016.html)
- Thread-Titel (wörtlich): "DQ500 nach fehlgeschlagener Grundeinstellung nur noch ungerade Gänge (P074A, P18BA, P0607)" — [tx-board.de](https://tx-board.de/threads/dq500-nach-fehlgeschlagener-grundeinstellung-nur-noch-ungerade-gaenge-p074a-p18ba-p0607.173840/)
- Thread-Titel (wörtlich): "'Rückrufaktion' für Octavia 3 7-Gang DSG – Aktion 34H5" — [skodacommunity.de](https://www.skodacommunity.de/threads/rueckrufaktion-fuer-octavia-3-7-gang-dsg-aktion-34h5.112329/)
- Thread-Titel (wörtlich): "Softwareupdate für DSG" — [skodacommunity.de](https://www.skodacommunity.de/threads/softwareupdate-fuer-dsg.112672/)
- Thread-Titel (wörtlich): "Rückruf Stronic Getriebe DQ200" — [motor-talk.de](https://www.motor-talk.de/forum/rueckruf-stronic-getriebe-dq200-t4750784.html?page=3)
- FabuCar-Beitragstitel (Werkstattfrage, wörtlich, Orthografie so im Original): "... und Gang rutschen durch (Audi A...)" — [fabucar.de](https://app.fabucar.de/beitraege/9e8abecd-e049-4df7-ad4e-eb1b58d5c501/--und--gang-rutschen-durch--audi-a-)

### Inferences
Abgeleitete Fragen (NICHT wörtlich; aus den in Abschnitt 1–3 belegten Themen formuliert, als FAQ-Kandidaten):
1. Was bedeutet der Fehler P1735 bei VW?
2. Was ist der Unterschied zwischen P1735 und P1736?
3. Was bedeutet 10666 bzw. 10668 im Fehlerspeicher?
4. Was heißt "Geber 1 für Kupplungsposition – elektrischer Fehler"?
5. Kann ich mit P1735 weiterfahren?
6. Warum fährt mein DSG nur noch in den geraden / ungeraden Gängen?
7. Ist bei P1735 die Kupplung defekt oder die Mechatronik?
8. Muss die ganze Mechatronik getauscht werden oder reicht ein Sensor?
9. Was kostet die Reparatur von P1735 beim DQ381?
10. Hilft ein Softwareupdate oder das Löschen des Fehlers?
11. Kommt der Fehler nach dem Löschen wieder?
12. Gibt es Kulanz von VW bei P1735/P1736?
13. Welche Modelle sind von P1735 betroffen (Golf 7/8, Tiguan, Passat, Kodiaq, Octavia)?
14. Tritt P1735 auch beim DQ200 oder DQ250 auf?
15. Muss nach der Reparatur eine Grundeinstellung gemacht werden?
16. Kann ich das Steuergerät einschicken, ohne das Getriebe auszubauen?
17. Ist ein gebrauchtes Steuergerät eine Alternative (Anlernen/Codierung)?
18. Hat P1735 etwas mit dem Getriebeölwechsel zu tun?
19. Warum zeigt mein OBD-Tester für P1735 einen anderen Text als VCDS/ODIS?
20. Gibt es einen Rückruf für das DQ381?

### Gaps
- Wörtliche Nutzerfragen aus Motor-Talk, Reddit, Golf-/Tiguan-/Kodiaq-Foren: nicht erhebbar (Hosts nicht erreichbar). Für die Seite sollten die Threads oben manuell gelesen oder Kundenanfragen von OZ Performance ausgewertet werden.
- Google "Weitere Fragen" (PAA) zu "P1735": nicht abrufbar.

---

## 5. Getriebespülung: Methoden, Austauschgrad, Ablauf, Dauer, Ölmengen

### Takeaway
Ein einfacher Ölwechsel (Ablassen/Auffüllen) erneuert beim Wandlerautomaten grob 40–60 % des Öls, eine dynamische Spülung mit Gerät laut Anbietern "bis zu 90 %" bis "95–97 %" – die hohen Werte sind Anbieter-/Forenangaben ohne unabhängige Messung. Typischer Aufwand: 10–15 l Frischöl (ca. 3–4 l über Füllmenge laut Krafthand), 2–4 Stunden.

### Cited Findings
- Beim konventionellen Getriebeölwechsel verbleibt "stets noch etwa die Hälfte des Altöls im Getriebe" — [autobild.de](https://www.autobild.de/artikel/getriebeoelwechsel-16583253.html)
- Shop-Blog: beim einfachen Ablassen bleiben 40–60 % Altöl in Wandler und Kanälen — [blog.ws-autoteile.com](https://blog.ws-autoteile.com/auto-reparieren-diy/getriebespuelung/)
- "Eine solche Spülung entfernt bis zu 90 % des Altöls" — [web.de Magazin](https://web.de/magazine/auto/getriebeoel-wechseln-spuelung-pruefen-anzeichen-32659952)
- Tim-Eckart-Methode: Anbieterangabe ca. 97 % Austausch; 12–14 l Frischöl bei 9–10 l Gesamtfüllung (Forenvorstellung) — [e90-forum.de](https://www.e90-forum.de/forum/thread/33270-automatik-getriebe%C3%B6lsp%C3%BClung-tim-eckart-methode-kurze-vorstellung-inkl-erfahrungs/)
- Forenschätzung: rund 95 %, Ablagerungen im Ventilkörper würden aber nicht vollständig entfernt — [dodge-forum.eu](https://www.dodge-forum.eu/threads/wer-hat-sein-getriebe-nach-tim-eckart-methode-sp%C3%BClen-lassen.61645/)
- TE-Ablauf (5–6 Schritte): Reiniger einfüllen, kurze Fahrt/Warmlauf, Altöl ablassen, mit Frischöl im laufenden Betrieb spülen, befüllen, Ölstand elektronisch per Diagnosegerät prüfen — [tuningblog.eu](https://www.tuningblog.eu/tipps_tuev-dekra-u-co/tim-eckhart-methode-417968/); [att24.de](https://att24.de/getriebespuelung-tim-eckart-methode/)
- Mengen/Dauer: 10–15 l statt ca. 5 l beim normalen Wechsel; 2–4 Stunden statt ca. 30 Minuten — [att24.de](https://att24.de/getriebespuelung-tim-eckart-methode/)
- Im Schnitt 12 l Frischöl plus ca. 500 ml Spezialreiniger; beim normalen Wechsel werden nur 4–4,5 l abgelassen — [pannenhilfe-lehrte.de](https://www.pannenhilfe-lehrte.de/getriebesp%C3%BClungen/)
- Krafthand ("Die zehn wichtigsten Arbeitsschritte beim Getriebespülen"): Spülwirkung idealerweise mit etwa 3–4 l über der Getriebefüllmenge — [krafthand.de](https://www.krafthand.de/artikel/die-zehn-wichtigsten-arbeitsschritte-beim-getriebespuelen-38270/)
- Liqui Moly Gear Tronic: offizielle Kurzanleitungen für zwei Betriebsarten – Anschluss über Ölkühlerleitung ("Kühler-Modus") und über Messstabrohr ("Messstab-Modus"); Füllmenge nach Herstellerangabe einstellen, auf nächsten Literwert aufrunden, Ölstand danach prüfen — [liqui-moly.com (Kühler-Modus, PDF)](https://www.liqui-moly.com/fileadmin/user_upload/Downloads/Technische_Informationen/Oel/7917_Kurzanleitung_Geartronic_Kuehler-Modus.pdf); [liqui-moly.com (Messstab-Modus, PDF)](https://www.liqui-moly.com/fileadmin/user_upload/Downloads/Technische_Informationen/Oel/7917_Kurzanleitung_Geartronic_Messstab-Modus.pdf)
- Gear Tronic II: erkennt Flussrichtung automatisch, Füllmengen/Ölspezifikationen aus Datenbank, Additivdosierung integriert (Werkstattangaben) — [kfzservice-gerobl.at](https://www.kfzservice-gerobl.at/getriebesp%C3%BClungen/)
- Liqui Moly Automatikgetriebe-Reiniger: laut Hersteller für CVT-, DSG- und Wandlergetriebe; 300 ml reichen für 6–9 l Öl — [liqui-moly.com](https://www.liqui-moly.com/en/automatic-transmission-cleaner-p000013.html)
- Liqui Moly Verbraucherseite zum Automatikgetriebeölservice — [liqui-moly.com](https://www.liqui-moly.com/de/ch/fahrer/automatikgetriebeoelservice.html)
- Hauptnachteile der Spülung laut Quellen: höherer Ölverbrauch und Zeitaufwand — [att24.de](https://att24.de/getriebespuelung-tim-eckart-methode/)
- Forenstimme: Spülung werde heute oft gemacht, "weil es für die Werkstatt einfacher und sauberer ist" — [touran-24.de](https://www.touran-24.de/thread/32799-dsg-%C3%B6l-wechsel-interval/)

### Inferences
- Für die Seite sauber trennen: (a) Ölwechsel statisch (Ablassen/Wanne/Filter, ca. 40–60 %), (b) mehrfacher Ölwechsel, (c) dynamische Spülung über Kühlerkreislauf mit Gerät (Anbieterangaben 90–97 %). Die Prozentwerte stets als "laut Geräte-/Methodenanbieter" kennzeichnen; eine unabhängige Messreihe wurde nicht gefunden.
- Der Austauschgrad hängt vom Getriebetyp ab: Beim nassen DSG ohne Wandler läuft beim Ablassen ein deutlich größerer Anteil heraus als beim Wandlerautomaten – deshalb ist der Zusatznutzen einer Spülung beim DSG kleiner (siehe Abschnitt 7).

### Gaps
- Mahle-Spülgeräte (ATX-Serie): keine technischen Angaben gefunden.
- ZF-Volltext zum offiziellen 8HP-Ölwechselverfahren (ZF-Dokument Stand 11.2024, nur Überschrift sichtbar): [ZF-PDF](https://aftermarket.zf.com/app/controller/ti/download/Binary/8e37fbbb-a254-11ef-a30a-00505690da53.pdf) – nicht lesbar. **prüfen (OZ hat als ZF Service Point Zugriff)**
- Unabhängige Messung des Austauschgrads (ADAC/GTÜ/Fachpresse-Test): nicht gefunden.

---

## 6. Herstellerpositionen zu Ölwechselintervallen (ZF, VW DSG, Mercedes, BMW)

### Takeaway
ZF kommuniziert zwei Zahlen, die auf der Seite nebeneinander erklärt werden müssen: "Lebensdaueröl, Wechsel nur im Reparaturfall – empfohlen nach 150.000 km" (Produktdatenblatt/Ratgeberzitate) und "je nach Fahrweise alle 80.000–120.000 km bzw. spätestens nach 8 Jahren" (ZF-Serviceinformation zum Ölwechselkit 8HP). Bei VW gilt: DQ250 alle 60.000 km, DQ381 120.000 km (teils mit 5-Jahres-Grenze genannt), DQ200 kein planmäßiger Wechsel; für Mercedes fanden sich nur Sekundärquellen.

### Cited Findings
**ZF**
- ZF-Produktdatenblatt LifeguardFluid: Ölwechsel in der Regel nur im Reparaturfall erforderlich; als Empfehlung Ölwechsel nach 150.000 km (Dokumentstand 2017) — [ZF Aftermarket PDS LifeguardFluid 6](https://aftermarket.zf.com/lubricants-datasheets/lifeguardfluid-6/pds_zf_lifeguardfluid_6_de_20171110.pdf)
- ZF-Serviceinformation "Ölwechselkit für ZF-Automatgetriebe 8HP" (als Anhang bei Motor-Talk, ca. 2019): Ölwechsel alle 80.000 bis 120.000 km bzw. spätestens nach acht Jahren; nur vorgeschriebenes ZF-LifeguardFluid verwenden; Warnung vor Additiven (Konfidenz: mittel – ZF-Dokument, aber nur über Forenanhang und Snippet gesehen) — [motor-talk.de Anhang](https://www.motor-talk.de/forum/aktion/Attachment.html?attachmentId=777606)
- Forenwiedergabe: ZF-Empfehlung 120.000 km bzw. 8 Jahre, bei viel Autobahn/hoher Last 80.000 km — [oil-club.de](https://oil-club.de/index.php?thread%2F4347-zf-automatikgetriebe-8-gang%2F=)
- Ratgeberzitat: ZF Aftermarket nennt für Pkw-Automatikgetriebe 150.000 km und rät bei hoher Last zu kürzeren Intervallen — [kombi.de](https://www.kombi.de/getriebeoel-wechseln)
- ZF laut Autoservicepraxis: "Bei entsprechendem Nutzungsprofil sollte das Getriebeöl regelmäßig geprüft werden. Bei Bedarf ist eine Getriebeölspülung empfehlenswert." — [autoservicepraxis.de](https://www.autoservicepraxis.de/nachrichten/autobranche/getriebeoele-lebensverlaengernde-massnahmen-2534592)
- ZF-Aftermarket-Seite "Transmission oil change (PC)" als Primärquelle (nicht lesbar) — [aftermarket.zf.com](https://aftermarket.zf.com/sg/aftermarket-portal/for-workshops/useful-tips/transmission-oil-change-pc/)
- Zubehörkatalog nennt für 6HP 80.000 km Wechselintervall (kein ZF-Dokument) — [autoteiledirekt.de](https://www.autoteiledirekt.de/vaico-7078013.html)

**VW-Konzern DSG**
- DQ250 (6-Gang nass): Öl und Filter alle 60.000 km; DQ381 (7-Gang nass): 120.000 km; DQ200 (7-Gang trocken): laut Hersteller kein Getriebeölwechsel vorgesehen, Experten raten dennoch zu ca. 100.000 km (Konfidenz: hoch für DQ250/DQ200, mittel für DQ381) — [auto-motor-und-sport.de](https://www.auto-motor-und-sport.de/tech-zukunft/dsg-oelwechsel-erklaert-intervalle-fuer-dq200-dq250-dq381/)
- DQ381 "alle 120.000 km oder 5 Jahre"; DQ250 teils "60.000 km oder 4 Jahre" (Sekundärquellen) — [automobilsalon-bellemann.de](https://automobilsalon-bellemann.de/news/dsg-oelwechsel-intervall-kosten-getriebespuelung/)
- Widerspruch: ein Ratgeber nennt für DQ381 60.000 km — [welchesoel.de](https://welchesoel.de/welches-ol-fur-dsg-getriebe/)
- DQ500: 60.000 km (Einzelquelle); britische Übersicht 40.000 Meilen — [hixa.eu](https://hixa.eu/blog/dsg-oil-change-guide)
- DQ200 hat zwei getrennte Ölkreisläufe (Getriebeöl und Hydrauliköl der Mechatronik) mit unterschiedlichen Ölen — [hixa.eu](https://hixa.eu/blog/dsg-oil-specifications)

**Mercedes**
- 722.9: Werksintervall laut Sekundärquelle "je nach Code bis 125.000 km / 5 Jahre"; Werkstattempfehlungen 60.000–80.000 km (Konfidenz: niedrig) — [motorzentrale.de](https://www.motorzentrale.de/magazin/7g-tronic-722-9-getriebespuelung-wann-ist-sie-sinnvoll/); [kfz-dietrich.com](https://kfz-dietrich.com/blog/getriebe-biz-automatik-oelwechsel-intervalle/)
- Ölfreigaben 722.9: frühe 7G-Tronic MB 236.14 (rot), 7G-Tronic Plus ab ca. Mitte 2010 MB 236.15 (blau), nicht verwechseln/mischen — [getriebewerkstatt.com](https://getriebewerkstatt.com/news-25.html)
- Pauschale Sekundärangabe 7G/9G: 60.000–100.000 km oder 4–6 Jahre — [kfzpick.de](https://kfzpick.de/aktuelles/was-kostet-getriebeolwechsel-bei-mercedes-automatik/)

**BMW / "Lifetime" / ADAC**
- Bericht zum Thema Lifetime-Füllung: ADAC widerspricht der Lebensdauerfüllung und empfiehlt je nach Modell einen Wechsel nach etwa 100.000 km; ZF: nach 150.000 km sinnvoll — [netzwelt.de](https://www.netzwelt.de/news/258541-lifetime-getriebeoel-moderne-autos-versiegelte-getriebe-haben-haken-liegt.html)
- Sekundärangabe: ADAC empfiehlt für Wandlerautomaten etwa alle 100.000 km einen Ölwechsel inklusive Spülung (ADAC-Originalseite nicht gefunden) — [kombi.de](https://www.kombi.de/getriebeoel-wechseln)

### Inferences
- Formulierungsvorschlag, der beide ZF-Zahlen korrekt abbildet: "ZF befüllt mit Lebensdaueröl, empfiehlt aber im Aftermarket je nach Belastung einen Ölwechsel nach 80.000–120.000 km bzw. spätestens nach 8 Jahren; in Datenblättern nennt ZF spätestens 150.000 km." Welche Fassung aktuell gilt, muss OZ Performance anhand der aktuellen ZF-Serviceinformation bestätigen (als ZF Service Point Primärzugang).
- BMW-"Lifetime": Der Fahrzeughersteller sieht keinen Wechsel vor, der Getriebehersteller empfiehlt einen – diese Gegenüberstellung ist der zentrale, gut belegbare Punkt.

### Gaps
- Offizielle Mercedes-Wartungsvorgaben (Wartungsblätter) für 722.6, 722.9, 725.0 inkl. einmalig/wiederkehrend und km-/Jahreswerte: nicht belegt. Die oft zitierten Werte (722.6 einmalig 60.000 km; 722.9 je nach Baujahr 50.000 bzw. 125.000 km; 725.0 125.000 km) konnten in dieser Sitzung NICHT mit Quelle bestätigt werden. **prüfen**
- BMW-Originalaussage zur Lebensdauerfüllung: keine Primärquelle.
- VW-Originalwartungstabelle (DQ381-Intervall je Modelljahr, DQ500, DQ400e-Hybrid, Audi 0B5/DL382): nicht belegt.
- ADAC-Originalseite und GTÜ-Position: nicht gefunden.

---

## 7. Ist eine Spülung sinnvoll oder schädlich? Wann nicht spülen, welche Getriebe, Additive, Filter/Ölwanne, Dichthülse

### Takeaway
Die Fachpresse behandelt die Spülung als umstritten ("Pro & Contra", Autoservicepraxis 2023): ZF hält sie "bei Bedarf" für empfehlenswert, warnt aber vor Additiven; der Einsatz von Reinigern ist der eigentliche Streitpunkt. Ein Beleg, dass eine fachgerechte Spülung ein gesundes Getriebe zerstört, wurde nicht gefunden – gewarnt wird vor Spülungen bei vorhandenem Metallabrieb/mechanischem Defekt und (von DSG-Spezialisten) vor aggressivem Spülen beim DSG.

### Cited Findings
- Autoservicepraxis hat ein "Pro & Contra Getriebeölspülung" veröffentlicht (Ausgabe 11/2023) — [autoservicepraxis.de (PDF)](https://live.autoservicepraxis.de/downloadfile/3449492/90007_2023_27_11_I_026-027_n16_Pro_Contra_Getriebolspulung_484380_print.pdf)
- Autoservicepraxis zu Additiven: Der Einsatz von Reinigungszusätzen wird kontrovers diskutiert; ein dort zitierter Betrieb verzichtet darauf und setzt bei hartnäckigen Fällen auf wiederholtes Spülen mit Frischöl — [autoservicepraxis.de](https://www.autoservicepraxis.de/nachrichten/kfz-werkstatt/lebensverlaengernde-massnahme-3449497)
- ZF-Serviceinformation 8HP-Ölwechselkit warnt vor der Verwendung von Additiven — [motor-talk.de Anhang](https://www.motor-talk.de/forum/aktion/Attachment.html?attachmentId=777606)
- ZF: Öl bei entsprechendem Nutzungsprofil regelmäßig prüfen, "bei Bedarf ist eine Getriebeölspülung empfehlenswert" — [autoservicepraxis.de](https://www.autoservicepraxis.de/nachrichten/autobranche/getriebeoele-lebensverlaengernde-massnahmen-2534592)
- Kontraindikationen laut Shop-Blog: Metallabrieb, mechanischer Defekt oder über 180.000 km ungewechselt (Schwelle = Einzelquelle) — [blog.ws-autoteile.com](https://blog.ws-autoteile.com/auto-reparieren-diy/getriebespuelung/)
- "Eine Spülung ersetzt keine Reparatur", wenn das Getriebe bereits einen Defekt hat — [getriebezentrum-rhein-main.de](https://getriebezentrum-rhein-main.de/ratgeber/getriebespuelung-versus-oelwechsel-wo-liegt-der-unterschied/)
- "Eine Garantie gegen bereits vorhandene mechanische Schäden ist sie jedoch nicht" — [optimum-fahrzeugtechnik.de](https://optimum-fahrzeugtechnik.de/blog/getriebespuelung-oder-oelwechsel)
- Forenängste (Mythos-Quelle): gelöste Partikel/Späne könnten an Stellen landen, wo sie Schaden anrichten — [motor-talk.de](https://www.motor-talk.de/forum/getriebespuelung-ja-oder-nein-t5822283.html)
- DSG-Spezialist: Für ein DSG sei die Spülung der falsche Weg; empfohlen wird fachgerechter Ölwechsel mit Filter; bei hoher Laufleistung mit nie gewechseltem Öl könne eine aggressive Spülung gelöste Ablagerungen in die Mechatronik schwemmen (Einzelquelle) — [hixa.eu](https://hixa.eu/blog/dsg-flush-guide)
- Gegenposition: Werkstätten bieten Spülung ausdrücklich auch für DSG und CVT an ("macht auch einen Sinn"), Liqui Moly gibt seinen Reiniger für CVT/DSG/Wandler frei — [bo-kfz.de](https://www.bo-kfz.de/getriebespuelung/); [liqui-moly.com](https://www.liqui-moly.com/en/automatic-transmission-cleaner-p000013.html)
- Empfohlen bei höherer Laufleistung (ab 100.000 km), bei Schaltproblemen oder stark verunreinigtem Öl; bei Fahrzeugen mit Servicehistorie lässt sich dabei der Getriebezustand beurteilen — [carwiki.de](https://carwiki.de/getriebespuelung); [mobile.de Magazin](https://www.mobile.de/magazin/artikel/getriebe-oel-wechseln-verschleiss-vorbeugen-2514)
- Hohe Laufleistung: Forenthreads diskutieren Spülung bei 200.000+ km kontrovers; ein Nutzer rät bei unauffälligem Getriebe "maximal das Öl wechseln" — [motor-talk.de](https://www.motor-talk.de/forum/getrieboelspuelung-nach-tim-eckart-bei-hoher-laufleistung-noch-sinnvoll-t5087068.html); [f10-forum.de](https://www.f10-forum.de/forum/thread/7432-getriebesp%C3%BClung-bei-hoher-laufleistung/)
- ZF 8HP: Ölwanne mit integriertem Filter wird beim Service mitgetauscht (Angebotsumfang "Original-ZF-Ölwanne und integrierter Filter") — [autoservice-marbach.de](https://www.autoservice-marbach.de/getriebespuelung-stuttgart-ludwigsburg/)
- DQ200: Hersteller sieht keinen Ölwechsel vor; getrennte Kreisläufe (siehe Abschnitt 6) — [auto-motor-und-sport.de](https://www.auto-motor-und-sport.de/tech-zukunft/dsg-oelwechsel-erklaert-intervalle-fuer-dq200-dq250-dq381/)
- Symptome, bei denen Quellen eine Spülung eher empfehlen: ruckelnde Schaltvorgänge/Schaltprobleme; Mercedes 7G-Tronic Wandlerthema als Spülanlass (Werkstattblog) — [motorzentrale.de](https://www.motorzentrale.de/magazin/getriebespuelung-vorteile-und-nachteile-unter-der-lupe/); [kfz-dietrich.com](https://kfz-dietrich.com/blog/mercedes-7g-tronic-getriebespuelung-w211-w212/)
- ZF 8HP: Adaptions-Reset hilft bei Belagverschleiß oder Mechatronikdefekt oft nur kurz (Werkstattblog) — [kfz-dietrich.com](https://kfz-dietrich.com/blog/bmw-zf8hp-automatik-notprogramm-diagnose/)

### Inferences
- Tragfähige, belegbare Linie für die Seite: (1) Spülung ist Wartung, keine Reparatur; (2) vor jeder Spülung Befund (Fehlerspeicher, Ölprobe/Abrieb, Probefahrt); (3) nicht spülen bzw. erst reparieren bei Metallspänen, verbranntem Öl mit Durchrutschen, mechanischem Defekt; (4) Additive: ZF warnt, Fachpresse nennt es kontrovers – OZ sollte als ZF Service Point seine eigene Praxis (mit/ohne Reiniger) transparent begründen; (5) der Mythos "Spülung zerstört altes Getriebe" entsteht typischerweise, weil bereits geschädigte Getriebe als letzter Versuch gespült werden – dafür gibt es keinen direkten Beleg, nur die Forendiskussion; als Einordnung, nicht als Tatsache formulieren.
- Getriebetyp-Matrix (aus Quellen ableitbar, von OZ zu bestätigen): Wandlerautomat (ZF 6HP/8HP, 722.x, Aisin) = klassischer Spülkandidat; nasses DSG (DQ250/DQ381/DQ500, DL501) = Ölwechsel mit Filter üblich, Spülung möglich aber umstritten; trockenes DQ200 = kein Spülkreislauf über Kühler im klassischen Sinn, nur Wechsel von Getriebeöl und ggf. Mechatronik-Hydrauliköl; CVT/Multitronic = laut Werkstätten/Liqui Moly möglich, mit höherem Aufwand.
- Symptome, die eine Spülung NICHT heilt (aus den "ersetzt keine Reparatur"-Aussagen abgeleitet): Durchrutschen durch verschlissene Lamellen, Mechatronik-/Sensordefekte (z. B. P1735), Druckspeicherdefekte (P17BF/P189C), mechanische Geräusche.

### Gaps
- Inhalt des Autoservicepraxis-Pro/Contra (wer vertritt welche Position, Zitate): PDF nicht lesbar.
- ADAC-, GTÜ- und Auto-Bild-Originalaussagen speziell zur Spülung (nicht nur zum Ölwechsel): nicht gefunden.
- ZF-Aussagen zur Mechatronik-Dichthülse (Steckerhülse 6HP/8HP) und zum Tausch der Kunststoffölwanne als Pflichtumfang: keine Quelle gefunden – als OZ-Praxiswissen ergänzen.
- Belege zu "Wandlerrupfen durch Spülung behoben" (Erfolgsquote): nur Werkstattblogs, keine Daten.
- Multitronic (Audi 01J/0AW) und DQ200 spezifisch: keine belastbare Quelle zur Spülbarkeit.

---

## 8. Preise für Getriebespülung in Deutschland (2026)

### Takeaway
Belegte Angebotspreise freier Spezialisten liegen 2026 bei etwa 350–820 € je nach Getriebe (ZF 8HP typ. 620–820 € inkl. Öl, Ölwanne/Filter, Adaption; 7G-Tronic 490–590 €; DSG-Ölwechsel mit Filter ca. 450 €). Ratgeber-Spannen (100–700 €) sind teils über drei Jahre alt; aktuelle Händler-/Kettenpreise wurden nicht gefunden.

### Cited Findings
- BMW ZF 8HP beim Spezialisten: 650–820 € je nach Variante, inkl. Öl, neuer Ölwanne mit Filter und Adaption (Seite ca. Herbst 2026) — [motorschmiede.com](https://motorschmiede.com/bmw-getriebespuelung/zf-8hp/)
- Autoservice Marbach (Raum Stuttgart): 7G-Tronic 490 €, BMW ZF 8HP 630 €, Audi ZF 8HP55 620 €; inkl. Original-ZF-Öl, Original-ZF-Ölwanne mit integriertem Filter — [autoservice-marbach.de](https://www.autoservice-marbach.de/getriebespuelung-stuttgart-ludwigsburg/)
- Wildemann Getriebetechnik (ZF Service Point): Spülung ZF 6HP/8HP "ab 350 €"; VW-DSG-Ölwechsel mit Filter/Spülung 450 € — [w-w-auto.de](https://w-w-auto.de/zf-automatikgetriebe-spuelung/)
- Mercedes 7G-Tronic 590 € inkl. MwSt., inkl. Öl, Filterkit und Differentialölwechsel — [getriebespuelung-stuttgart.de](https://getriebespuelung-stuttgart.de/)
- DSG-Gesamtkosten VW/Audi 600–900 €: ca. 8 l DSG-Öl 180–240 €, Filter 150–250 €, Arbeitszeit 270–410 €; ZF-Spezialöl bis zu 40 €/l (Quelle ca. 2025) — [auto-naim.de](https://www.auto-naim.de/blog/automatikgetriebe-wartung-wann-sinnvoll-was-kostet-sie)
- Ältere Markenspannen (ca. 2023): VW/Skoda/Seat Spülung 350–500 €, kombiniert mit DSG-Ölwechsel 500–700 €; Audi ca. 600 €; BMW (ZF-Wandler) 500–600 €; Ford 450–600 € — [carwiki.de](https://carwiki.de/getriebespuelung)
- Ratgeber-Spannen: einfacher Ölwechsel ca. 100 €, Spülung 100–500 €; Ölwechsel plus Spülung 330–600 € — [bussgeldkatalog.org](https://www.bussgeldkatalog.org/getriebeoel-wechseln/); [autozeitung.de](https://www.autozeitung.de/getriebeoelwechsel-203175.html)
- Werkstattangabe 300–700 € je nach Fahrzeug — [autoservice-sengbusch.de](https://autoservice-sengbusch.de/ratgeber/getriebeoelwechsel-oder-getriebeoelspuelung)
- Preistreiber: Wandler- und CVT-Getriebe teurer als DSG wegen Mehraufwand und höherer Ölmenge; bei Allrad teils Demontage der vorderen Kardanwelle nötig — [bo-kfz.de](https://www.bo-kfz.de/getriebespuelung/); [autohaus-viole.de](https://www.autohaus-viole.de/getriebe.htm)
- Vergleichsportal für Getriebeölwechsel-Preise — [fairgarage.com](https://www.fairgarage.com/de-de/getriebeoelwechsel-kosten)
- Motor-Talk-Thread zu Mercedes-Händlerpreisen 722.9 (alt, Zweifel an Rechnung) — [motor-talk.de](https://www.motor-talk.de/forum/spuelung-oelwechsel-7g-tronic-typ-722-9-preise-bei-mb-zweifel-an-der-rg-t2224787.html)

### Inferences
- Realistische Preistabelle 2026 für freie Spezialisten (aus den Angeboten verdichtet): ZF 6HP ca. 350–650 €; ZF 8HP ca. 620–820 €; Mercedes 7G-Tronic ca. 490–600 €; nasses DSG (Ölwechsel mit Filter/Spülung) ca. 450–700 €, in Einzelquellen bis 900 €. Immer angeben, was enthalten ist: Ölmenge und -spezifikation, Ölwanne/Filter, Dichtungen/Schrauben, Reiniger ja/nein, Adaption/Reset, MwSt.
- "Was ist im Preis enthalten?" ist die wichtigste Vergleichsfrage – Billigangebote ohne Ölwanne/Filter sind nicht vergleichbar. Eine transparente Leistungsliste ist ein Zitier-Asset.

### Gaps
- Preise von Ketten (ATU, Bosch Car Service, Vergölst) und Vertragshändlern 2026: nicht gefunden.
- Preise für 9G-Tronic, 722.6, CVT/Multitronic, DQ200: nicht belegt.
- Regionale Preise Ruhrgebiet/Bochum: nicht erhoben.

---

## 9. Reale Nutzerfragen zur Getriebespülung

### Takeaway
Wörtlich belegt sind nur Thread- und Seitentitel (unten zitiert); "Weitere Fragen"-Boxen von Google und Foreninhalte waren nicht abrufbar. Die Zielzahl von 20–30 wörtlichen Fragen wurde NICHT erreicht; die zweite Liste ist abgeleitet und so zu kennzeichnen.

### Cited Findings
Wörtliche Titel/Fragen:
- "Getriebespülung JA oder NEIN?" (BMW 3er E46) — [motor-talk.de](https://www.motor-talk.de/forum/getriebespuelung-ja-oder-nein-t5822283.html)
- "Getriebölspülung nach Tim Eckart bei hoher Laufleistung noch sinnvoll?" — [motor-talk.de](https://www.motor-talk.de/forum/getrieboelspuelung-nach-tim-eckart-bei-hoher-laufleistung-noch-sinnvoll-t5087068.html)
- "Getriebespülung bei hoher Laufleistung" (BMW F10/F11) — [f10-forum.de](https://www.f10-forum.de/forum/thread/7432-getriebesp%C3%BClung-bei-hoher-laufleistung/)
- "Automatikgetriebe ZF 8HP hohe Laufleistung ohne Getriebeölwechsel, Erfahrungen" — [motor-talk.de](https://www.motor-talk.de/forum/automatikgetriebe-zf-8hp-hohe-laufleistung-ohne-getriebeoelwechsel-erfahrungen-t6533858.html)
- "ZF8HP Ölwechsel selber durchführen" — [motor-talk.de](https://www.motor-talk.de/forum/zf8hp-oelwechsel-selber-durchfuehren-t5287015.html)
- "Getriebespülung – Wo und Wie?" — [2ertalk.de](https://www.2ertalk.de/threads/6672/)
- "Wer hat sein Getriebe nach Tim Eckart Methode spülen lassen?" — [dodge-forum.eu](https://www.dodge-forum.eu/threads/wer-hat-sein-getriebe-nach-tim-eckart-methode-sp%C3%BClen-lassen.61645/)
- "Automatikgetriebe spülen – welche Möglichkeiten? – Tim-Eckart-Methode" — [oil-club.de](https://oil-club.de/index.php?thread%2F4664-automatikgetriebe-sp%C3%BClen-welche-m%C3%B6glichkeiten-tim-eckart-methode%2F=&pageNo=10)
- "Getriebespülung Unterschiede / Tim Eckart – Liqui Moly Gear Tronic / Motul Evo /// allgemeine Fragen zur Spülung" — [andre-citroen-club.de](https://www.andre-citroen-club.de/forums/topic/133476-getriebesp%C3%BClung-unterschiede-tim-eckart-liqui-moly-gear-tronic-motulevo-allgemeine-fragen-zur-sp%C3%BClung/)
- "Getriebespülung nach Tim Eckart Methode in Raum Frankfurt/Main gesucht" (Muster: lokale Anbietersuche) — [motor-talk.de](https://www.motor-talk.de/forum/getriebespuelung-nach-tim-eckart-methode-in-raum-frankfurt-main-gesucht-t3327526.html)
- "Spülung/Ölwechsel 7G-TRONIC (Typ 722.9) Preise bei MB / Zweifel an der Rg" — [motor-talk.de](https://www.motor-talk.de/forum/spuelung-oelwechsel-7g-tronic-typ-722-9-preise-bei-mb-zweifel-an-der-rg-t2224787.html)
- "DSG ÖL Wechsel interval ?" — [touran-24.de](https://www.touran-24.de/thread/32799-dsg-%C3%B6l-wechsel-interval/)
- "Getriebespülung beim DSG oder Ölwechsel?" (Ratgebertitel) — [hixa.eu](https://hixa.eu/blog/dsg-flush-guide)
- "Getriebeölspülung: Wann ist sie wirklich sinnvoll?" — [getriebe.biz](https://getriebe.biz/ratgeber/getriebeoelspuelung-sinnvoll-oder-nicht/)
- "7G-Tronic (722.9) Getriebespülung: Wann ist sie sinnvoll?" — [motorzentrale.de](https://www.motorzentrale.de/magazin/7g-tronic-722-9-getriebespuelung-wann-ist-sie-sinnvoll/)
- "Getriebespülung versus Ölwechsel – wo liegt der Unterschied?" — [getriebezentrum-rhein-main.de](https://getriebezentrum-rhein-main.de/ratgeber/getriebespuelung-versus-oelwechsel-wo-liegt-der-unterschied/)
- Anbieter-FAQ "FAQ Getriebespülung" (Fragenkatalog, nicht lesbar) — [boostdynamics.ch](https://www.boostdynamics.ch/faq-getriebesp%C3%BClung)

### Inferences
Abgeleitete FAQ-Kandidaten (NICHT wörtlich):
1. Was ist der Unterschied zwischen Getriebespülung und Getriebeölwechsel?
2. Wie viel Altöl wird bei einer Spülung wirklich getauscht?
3. Was kostet eine Getriebespülung (ZF 8HP, 7G-Tronic, DSG)?
4. Was ist im Preis enthalten – Ölwanne, Filter, Adaption?
5. Wie lange dauert eine Getriebespülung?
6. Ist eine Getriebespülung bei 200.000 km noch sinnvoll oder gefährlich?
7. Kann eine Getriebespülung das Getriebe kaputt machen?
8. Wann sollte man NICHT spülen?
9. Hilft eine Spülung gegen Schaltrucken / Wandlerrupfen / verzögertes Einlegen?
10. Was ist die Tim-Eckart-Methode und ist sie besser als Liqui Moly Gear Tronic?
11. Wird mit Reiniger gespült – und ist das schädlich?
12. Was sagt ZF zur Getriebespülung?
13. Mein Hersteller sagt "Lifetime-Öl" – brauche ich trotzdem einen Wechsel?
14. Wie oft sollte man das Automatikgetriebeöl wechseln (ZF 6HP/8HP, 7G/9G-Tronic)?
15. Kann man ein DSG spülen? Gilt das auch für das 7-Gang-DQ200?
16. Kann man ein CVT / eine Multitronic spülen?
17. Muss nach der Spülung die Adaption zurückgesetzt werden?
18. Verliere ich durch eine Spülung in der freien Werkstatt die Garantie?
19. Welches Öl wird verwendet (ZF LifeguardFluid, MB 236.14/236.15)?
20. Warum ist die Spülung beim Allrad teurer?
21. Reicht ein doppelter Ölwechsel statt einer Spülung?
22. Kann ich die Getriebespülung selbst machen?
23. Woran erkenne ich, dass mein Getriebeöl gewechselt werden muss?
24. Nach der Spülung schaltet das Getriebe schlechter – ist das normal?
25. Wo finde ich einen Spezialisten für Getriebespülung in meiner Nähe?

### Gaps
- Google-PAA-Fragen und wörtliche Forenfragen im Fließtext: nicht abrufbar; vor Veröffentlichung per SERP-Check (deutsche IP) ergänzen.
- Reddit (r/de, r/automobil) und GTÜ/ADAC-Leserfragen: nicht erhoben.
