# Prüfbericht: Steuergeräte-Reparatur-Konfigurator (OZ Performance GmbH)

**Urteil: nicht freigegeben**

Geprüft am 25.11.2026: `konfigurator/index.html` (1.772 Zeilen), `konfigurator/README.md`, `konfigurator/vorschau/`. Die Dateien wurden nicht verändert. Geprüft wurde mit eigenen Playwright-Skripten in Chromium (Firefox und WebKit sind nicht installiert).

| Schwere | Anzahl |
|---|---|
| kritisch | 3 |
| wichtig | 11 |
| klein | 20 |

Die drei kritischen Punkte in einem Satz: Über die Fortschrittsleiste lässt sich die Prüfung der Schritte umgehen (Auftrag wird ohne AGB-Zustimmung und mit ungültiger E-Mail als „übermittelt“ gemeldet), nach einer Änderung in Schritt 1 stehen falsche Fehlercodes, Symptome und Teilenummern in Zusammenfassung, Arbeitskarte und Datensatz, und ein Emoji an einer bestimmten Textstelle legt den Konfigurator im Tab dauerhaft lahm.

Die Grundlagen sind in Ordnung: kein Skript-Einschleusen möglich, keine Fremdanfragen, Fehlerfälle beim Senden werden ehrlich gemeldet, Tastaturbedienung und Kontraste stimmen, die iframe-Einbettung aus der README funktioniert.

---

## Kritisch

### K1 – Fortschrittsleiste umgeht die Pflichtprüfungen; Auftrag geht ohne Zustimmung raus

- **Nachstellen:** Auftrag bis zur Zusammenfassung ausfüllen. „Zurück“ zu Schritt 5. Haken bei AGB und Widerruf entfernen, E-Mail auf `kaputt` ändern, Nachname leeren. In der Fortschrittsleiste auf „6. Zusammenfassung“ klicken (nicht auf „Weiter“). Mit eingetragenem `submit.endpoint` „Auftrag senden“ drücken.
- **Ist:** Die Zusammenfassung erscheint mit E-Mail „kaputt“ und ohne Namen. Der Server erhält `zustimmungen.agb.erteilt: false`, `kontakt.email: "kaputt"`, `kontakt.nachname: ""`. Angezeigt wird „Auftrag OZ-… wurde übermittelt“. Ohne Endpunkt werden E-Mail- und WhatsApp-Weg genauso angeboten. Gleiches Muster: In Schritt 3 nachträglich „Einbau in Bochum“ anhaken und per Fortschrittsleiste zu Schritt 6 springen → Terminanfrage ohne Wunschtermin (`termin.wunsch1: ""`), Versandangaben weg. Ein manipulierter oder unvollständiger sessionStorage-Stand mit `schritt: 6` führt ebenfalls direkt zur Sendeschaltfläche.
- **Soll:** Schritt 6 ist nur erreichbar und sendbar, wenn die Schritte 1–5 mit dem aktuellen Stand gültig sind.
- **Korrektur:** In `gehe(nr)` (Zeile 1719) beim Vorwärtsspringen alle Schritte von `Z.schritt` bis `nr-1` mit `PRUEFER[i]()` prüfen und `DANACH[i]()` ausführen; beim ersten Fehler dort anhalten und die Fehlerliste zeigen. Zusätzlich in `setzen()` (Zeile 842) `Z.maxSchritt` auf den Schritt des geänderten Felds zurücksetzen, damit spätere Schritte in der Leiste gesperrt sind. In `schritt6()` und `senden()` vor dem Anzeigen bzw. Absenden alle `PRUEFER` noch einmal laufen lassen (auch als Schutz nach `laden()`).

### K2 – Veraltete Angaben nach Änderung eines frühen Schritts

- **Nachstellen (a):** Einstieg „Fehlercode“, `P1735`, DQ381 wählen, in Schritt 2 das Symptom „Fehler an den Kupplungs-Positionssensoren …“ anhaken, bis Schritt 6. Dann „Ändern“ bei Gerät → „Getriebe auswählen“ → Mercedes-Benz → per Fortschrittsleiste zu Schritt 6.
- **Ist (a):** Auftrag für „Mercedes 7G-Tronic (722.9)“ mit Fehlercode P1735 und dem DQ381-Symptom, in Zusammenfassung, Arbeitskarte, E-Mail-Text und JSON. JSON: `geraet.einstieg: "katalog"`, aber `gesuchterFehlercode: "P1735"`.
- **Nachstellen (b):** Einstieg „Teilenummer“ `0GC325025D`, DQ381, bis Schritt 6. Zurück zu Schritt 1, „Getriebe auswählen“ → Mercedes, diesmal mit „Weiter“.
- **Ist (b):** Teilenummer `0GC325025D` bleibt beim Mercedes-Gerät stehen. Löscht der Kunde das Feld „Getriebe- / Teilenummer“ in Schritt 2 bewusst, erscheint die Nummer trotzdem wieder, weil `abschnitte()` auf `Z.geraet.teilenummer` zurückfällt (Zeile 942, ebenso Zeile 1033).
- **Nachstellen (c):** Rückweg „Selbstabholung“, Zahlung „Bar oder Karte bei Abholung“. Später in Schritt 4 auf „DHL Paket“ ändern und per Leiste zu Schritt 6.
- **Ist (c):** Zahlungswunsch „Bar oder Karte bei Abholung in Bochum“ bei DHL-Rückversand.
- **Nachstellen (d):** Abweichende Lieferadresse eintragen, danach Rückweg auf „Selbstabholung“ ändern (mit „Weiter“ durchgehen).
- **Ist (d):** Die Lieferadresse steht weiter in Zusammenfassung und Arbeitskarte.
- **Soll:** Keine Angabe, die zur aktuellen Auswahl nicht passt.
- **Korrektur:** Eine Funktion `bereinigen()` schreiben und in `setzen()` bei Änderung von `geraet.id`, `geraet.weg`, `leistung.einbau`, `versand.rueck`, `kontakt.typ` sowie zu Beginn von `schritt6()`/`datensatz()` aufrufen: Symptome auf `symptomListe()` filtern (steht heute nur in `nach1`, Zeile 1213); den aus Schritt 1 übernommenen Code aus `fahrzeug.codes` entfernen, wenn Gerät oder Einstieg wechselt, und `geraet.code`/`geraet.teilenummer` leeren, wenn `weg` nicht mehr passt; `fahrzeug.getriebeNr` leeren, wenn sie aus Schritt 1 stammt und das Gerät gewechselt wurde; `kontakt.zahlung` gegen `zahlungsOptionen()` prüfen (Zeile 991 nimmt `aktive(K.zahlungsarten)` statt `zahlungsOptionen()`). In Zeile 942 und 1033 den Rückfall `|| Z.geraet.teilenummer` streichen. In Zeile 987 die Bedingung um `&& Z.versand.rueck !== "abholung"` ergänzen. K1 beheben, damit `nach1/nach3/nach4` nicht übersprungen werden.

### K3 – Emoji an der Kürzungsgrenze bringt den Konfigurator zum Absturz, ohne Ausweg

- **Nachstellen:** Fehlerbeschreibung = 239 beliebige Zeichen, direkt danach ein Emoji (z. B. 😀), danach weiterer Text. Bis Schritt 5 ausfüllen, „Weiter zur Zusammenfassung“.
- **Ist:** JavaScript-Fehler `URIError: URI malformed`. Der Schrittbereich bleibt leer, die Seitenleiste mit „Eingaben löschen“ wird nicht mehr gezeichnet. Nach dem Neuladen derselbe Zustand, weil `schritt: 6` gespeichert ist. Der Kunde kommt nur durch Schließen des Tabs heraus und verliert alle Eingaben. Ursache: `wert.slice(0, 240)` (Zeile 1010) zerschneidet ein Zeichenpaar, `encodeURIComponent` (Zeile 1527/1528) wirft. Betrifft jedes Feld über 240 Zeichen (Beschreibung, Reparaturversuche). Selten, aber vollständiger Ausfall.
- **Soll:** Zusammenfassung erscheint immer.
- **Korrektur:** Zeile 1010: nach Zeichen statt nach Code-Einheiten kürzen, `wert = Array.from(wert).slice(0, 240).join("")`. Zusätzlich `encodeURIComponent` in `sendeBereich()` in `try/catch` fassen und in `schrittZeichnen()` (Zeile 1685) den Aufruf `BAUER[Z.schritt]()` absichern, damit bei einem Fehler Seitenleiste und „Eingaben löschen“ erhalten bleiben.

---

## Wichtig

### W1 – Vorbereitete E-Mail / WhatsApp-Nachricht wird zu lang (Auslieferungszustand)

- **Nachstellen:** Länge von `#ozk-mailto` messen.
- **Ist:** Minimalauftrag 1.334 Zeichen, Auftrag mit langer Beschreibung und Reparaturversuchen 2.677 Zeichen, alle Felder ausgeschöpft 10.217 Zeichen (WhatsApp 10.051). Umlaute und Emoji zählen kodiert drei- bis zwölffach. Viele Kombinationen aus Browser und Mailprogramm (vor allem unter Windows) schneiden `mailto:`-Adressen um etwa 2.000 Zeichen ab oder öffnen nichts. Der Kunde merkt das nicht; der Auftrag kommt verstümmelt oder gar nicht an. Ohne `endpoint` ist das der einzige Übermittlungsweg.
- **Soll:** Der Fallback bleibt sicher unter etwa 1.800 kodierten Zeichen oder verweist klar auf „Text kopieren“.
- **Korrektur:** In `auftragsText(true)` (Zeile 1000) ein Gesamtbudget einführen: Länge von `encodeURIComponent(text)` messen und schrittweise kürzen (Freitexte auf 120 Zeichen, Symptome weglassen, Bestätigungszeile kürzen). Wenn das Budget nicht reicht: nur Auftragsnummer, Name, Kontakt, Gerät senden und den Hinweis „vollständiger Text unten zum Kopieren“ einfügen. In der README als Grund nennen, warum der Livegang einen Endpunkt braucht.

### W2 – Mehrwertsteuer wird bei x,50-Beträgen falsch gerundet

- **Nachstellen:** Testkopie mit `preisNetto: 59.5`.
- **Ist:** Anzeige „70,80 € inkl. MwSt.“; richtig sind 70,81 € (59,50 × 1,19 = 70,805). Weitere Beispiele: 2,50 → 2,97 statt 2,98; 12,50 stimmt zufällig; 104,50 → 124,35 statt 124,36. Von 2.000 Nettowerten in 50-Cent-Schritten bis 1.000 € sind 251 um einen Cent zu niedrig. Ursache: Gleitkomma in `brutto()` (Zeile 776).
- **Korrektur:** In Cent rechnen: `function brutto(n){ var c = Math.round(n * 100); return Math.round(c * (100 + mwstProzent) / 100) / 100; }` mit ganzzahligem `mwstProzent`.

### W3 – Summe weicht um einen Cent von den angezeigten Einzelpreisen ab

- **Nachstellen:** Testkopie: DQ381 400, Express 80, DHL Paket 6.46, Versicherung 5.87. Express und Versicherung wählen.
- **Ist:** Zeilen 476,00 + 95,20 + 7,69 + 6,99 = 585,88 €; „Voraussichtliche Summe ab 585,87 €“ (Seitenleiste, Tabelle, Arbeitskarte, E-Mail-Text, JSON `summeBrutto`). Gegenüber Verbrauchern sieht das wie ein Rechenfehler aus.
- **Korrektur:** In `preisSumme()` (Zeile 928) zusätzlich die Summe der Zeilen-Bruttowerte bilden und diese als Endbetrag zeigen; Netto und MwSt. daraus ableiten. Alternativ Bruttopreise in der Konfiguration zulassen (`preisBrutto`), was auch das Eintragen der DHL-Endpreise vereinfacht: 10,49 € lässt sich mit zwei Nachkommastellen netto nicht treffen (8.82 → 10,50; 8.81 → 10,48).

### W4 – Werkstatt- und Auslandskunden sehen dieselbe Brutto-Darstellung

- **Nachstellen:** Testkopie mit Preisen; Schritt 5 „Werkstatt / Gewerbe“, Land Österreich, USt-IdNr. `ATU12345678`.
- **Ist:** „ab 476,00 € inkl. MwSt. (400,00 € netto)“ und „inkl. 19 % MwSt.“ unverändert. Für EU-Unternehmen mit USt-IdNr. ist deutsche Umsatzsteuer in der Regel nicht auszuweisen; für die Schweiz gelten eigene Regeln. Inländische Werkstätten erwarten Netto zuerst. Die Preisangaben in den Schritten 1–4 erscheinen ohnehin, bevor die Kundenart bekannt ist.
- **Korrektur:** In `preisText()` (Zeile 782) und `preisTabelle()` (Zeile 1494) nach `Z.kontakt.typ` und `Z.kontakt.land` unterscheiden: Werkstatt Inland „400,00 € netto (476,00 € inkl. MwSt.)“; Ausland keinen Bruttobetrag, sondern „400,00 € netto; Umsatzsteuer nach Prüfung im Kostenvoranschlag“. Steuerliche Behandlung vom Steuerberater bestätigen lassen und in die offenen Punkte der README aufnehmen.

### W5 – Weg „nicht gelistet“ (Anfrage) widerspricht sich selbst

- **Nachstellen:** „Anderes Gerät“ wählen, durchklicken.
- **Ist:**
  - Schritt 6: „Drucken Sie die Arbeitskarte aus … und legen Sie sie dem Paket bei“, obwohl Schritt 2 und 4 sagen „erst einsenden, nachdem wir Ihre Anfrage bestätigt haben“.
  - Arbeitskarte: „Bitte ausgedruckt und unterschrieben in das Paket legen“, Adressaufkleber, und die Packliste enthält den Hinweissatz „Bitte senden Sie das Gerät erst ein …“ als Ankreuzkästchen.
  - Hinweis über der Sendeschaltfläche: „übermitteln Sie uns Ihren Reparaturauftrag“.
  - Für eine unverbindliche Anfrage wird die Erklärung „Leistungsbeginn vor Ablauf der Widerrufsfrist“ verlangt und eine „Reparatur ohne Rückfrage bis Höchstbetrag“ angeboten.
  - Grammatik: „Der Anfrage ist erst bei uns, wenn …“ (Zeile 1537). Fehlermeldung beim Senden: „Der Auftrag konnte nicht übermittelt werden“. Seitenleiste: „Auftragsnummer“.
- **Korrektur:** Zeile 1537: Artikel mitführen („Die Anfrage“ / „Der Auftrag“). In `schritt6()` (Zeile 1518) bei `istAnfrage()` den Druckabschnitt durch „Die Arbeitskarte erhalten Sie nach unserer Bestätigung“ ersetzen oder als „Anfrage-Übersicht“ ohne Packliste und Aufkleber drucken (`druckbogenFuellen`, Zeilen 1600, 1606, 1612). In `zustimmungsArten()` (Zeile 997) `widerruf` bei Anfragen weglassen. In `schritt3()` die Freigabegrenze bei Anfragen ausblenden. Eigenen `abschlussHinweisAnfrage` in der Konfiguration vorsehen.

### W6 – Preisübersicht ragt bei 320 px aus der Karte

- **Nachstellen:** Viewport 320 px, Schritt 6, Preise `null`.
- **Ist:** Die Tabelle ist 38 px breiter als der Bildschirm. „Eingangsprüfung“, „Kostenvoranschlag“ und „ausgewiesen“ laufen über den Kartenrand und werden abgeschnitten; die Seite scrollt waagerecht. Bei 360, 768 und 1280 px kein Überlauf.
- **Korrektur:** `.ozk-preise` (Zeile 215): `table-layout: fixed;` und für `th, td` `overflow-wrap: anywhere; hyphens: auto;`. Besser unter 480 px die Zeilen untereinander stellen (`display: block` für `th` und `td`, Betrag linksbündig).

### W7 – Arbeitskarte: Unterschrift landet allein auf Seite 2

- **Nachstellen:** Minimalauftrag (nur Pflichtfelder), `page.pdf` mit Druckmedium.
- **Ist:** Zwei Seiten. Seite 1 endet mit „Vermerke der Werkstatt“; Unterschriftszeile und Adressaufkleber stehen allein oben auf Seite 2. Das Muster-PDF in `vorschau/` zeigt dasselbe. Kunden unterschreiben dann ein fast leeres Blatt oder legen nur Seite 1 bei. Beim langen Auftrag (2.000 Zeichen Beschreibung) bleibt Seite 1 zu zwei Dritteln leer, weil der Abschnitt „Fahrzeug und Fehler“ wegen `break-inside: avoid` komplett auf Seite 2 springt (drei Seiten statt zwei). Abgeschnitten wird nichts, Bedienelemente erscheinen nicht, Adressblock und Unterschriftszeile sind vorhanden.
- **Korrektur:** Minimalfall auf eine Seite bringen: „Bestätigt im Konfigurator“ und „Vermerke der Werkstatt“ nebeneinander, Abstände in `.ozk-druck section` (Zeile 277) und `.ozk-druck-unterschrift` (Zeile 289) verringern. Unterschrift und Aufkleber in einen gemeinsamen Block mit `break-inside: avoid` setzen und Seitenzahl „Seite 1 von 2“ sowie Auftragsnummer auf jeder Seite ausgeben. Für `.ozk-druck-breit` mit Freitext `break-inside: auto` erlauben.

### W8 – README und Konfigurationskommentar nennen „ab 400 €“, die Website nennt „ab 1.200 €“

- **Nachstellen:** `https://www.ozperformance.de/angebote/getriebesteuergeraet-reparatur-dq381-dq500` abrufen (25.11.2026, Status 200).
- **Ist:** Die Seite nennt „BOSCH-Steuergerät ab 1.200 €“ und „Die Komplettlösung inklusive Ölwechsel beginnt bei 1.200 €“. „400“ kommt im Text nicht vor. README Abschnitt 6 und der Kommentar in Zeile 586 behaupten „Die Website nennt für DQ381/DQ500 in der Werkstatt ‚ab 400 €‘“. Das Preisbeispiel `preisNetto: 400` zieht sich durch README und Konfiguration. Wer dem Hinweis folgt, trägt einen Preis ein, der der eigenen Website widerspricht.
- **Korrektur:** Aussage in README (Abschnitt 6, erster Punkt) und Zeile 586–587 berichtigen oder mit Quelle und Datum belegen. Beispielzahlen neutral wählen und als erfunden kennzeichnen.

### W9 – Fachaussagen und Leistungsumfang gehen über das Belegte hinaus

- **Ist:**
  - Belegt ist nur die Zuordnung Code → Getriebe. Der Konfigurator behauptet darüber hinaus als Tatsache: „Diese Codes betreffen die Kupplungs-Positionssensoren“ (Zeile 688, auch als Symptom in Zeile 584 und 597), „hängen typischerweise mit dem Hydraulikdruck der Mechatronik im DSG DQ200 zusammen“ (Zeile 690), „betreffen typischerweise die internen Sensoren der Steuereinheit“ (Zeile 692). Die eigene Website spricht beim DQ381/DQ500 vom „Druck- und Positionsgeber“ bzw. „Positions- bzw. Drucksensor“, nicht von Kupplungs-Positionssensoren. Die Recherchenotizen vermerken, dass die Bedeutungsangaben fast nur von Reparaturanbietern stammen und sich widersprechen (P189C, P0841).
  - Der Katalog bietet DQ250, DL501, Multitronic, ZF 6HP, ZF 8HP und 722.9 als reparierbare Geräte an, mit Einbauort, Symptomen und Einsendeumfang. Ob OZ diese Steuergeräte im Einsendegeschäft repariert, ist nicht belegt. Die README führt das als offenen Punkt, der Kunde sieht es aber als Angebot.
  - Teilenummern-Suche: Kennungen ab vier Zeichen treffen auch mitten in der Nummer. `TEST7229X` und jede Nummer mit der Ziffernfolge 7229 (z. B. `1K0 907 229`) ergibt „Die Nummer passt zu folgendem Gerätetyp: Mercedes 7G-Tronic“. Der Präfix „6HP“/„8HP“ ist eine Getriebebezeichnung, keine Teilenummer.
  - „DHL-Pakete sind … bis 500 € abgesichert“ steht auch dann da, wenn „DHL Express“ als Rückweg gewählt ist; Express hat eigene Haftungsregeln.
  - Plausibel und unauffällig: 0AM/0CW = DQ200 trocken, 02E = DQ250 nass, 0GC = DQ381, 0BH/0BT = DQ500, 0B5 = DL501 längs, 01J/0AW = Multitronic, Mechatronik in der Ölwanne bei ZF 6HP/8HP, FIN im Fahrzeugschein unter E.
- **Korrektur:** Hinweistexte auf die belegte Aussage kürzen: „Dieser Code wird häufig bei DQ381 und DQ500 gemeldet.“ Symptomzeile 584/597 in „Fehlercodes P1735, P1736 oder P0805“ ändern. Nicht bestätigte Geräte bis zur Freigabe durch den Inhaber aus `geraete` nehmen (dafür ein Feld `aktiv` einführen und in `geraeteKarten`, `nummerTreffer`, `codeTreffer` beachten). In `nummerTreffer()` (Zeile 898) nur Treffer am Anfang zulassen und den Text auf „könnte passen“ abschwächen. Versicherungstext neutral fassen oder nur bei DHL Paket zeigen.

### W10 – Vorschau-Material für den Kunden enthält Testreste

- **Ist:** `vorschau/arbeitskarte_muster.pdf` zeigt als Fehlerbeschreibung „Fiktiver Testfall `<img src=x onerror="window.__xss=1"> <script>window.__xss=2</script>` Ganganzeige blinkt.“ und „Ölwechsel durchgeführt (Testdaten).“. Die E-Mail-Adresse bricht mitten im Wort um („…@example.co / m“), der Aufkleber trennt die Auftragsnummer („OZ- / 261125-DWAJ“). `vorschau/07_termin_einbau_desktop_1280.png` zeigt das Datum im US-Format („11/30/2026“, „mm/dd/yyyy“).
- **Korrektur:** Muster-PDF mit sauberen Beispieldaten neu erzeugen. Screenshots mit `locale: "de-DE"` aufnehmen. Auftragsnummer auf dem Aufkleber mit `white-space: nowrap` schützen (Zeile 1614).

### W11 – Datensatz (JSON) enthält widersprüchliche Reste

- **Nachstellen:** Freigabegrenze 500 eintragen, zurück auf „immer Kostenvoranschlag“. Versicherung mit Warenwert 1500 wählen, dann Rückweg „Selbstabholung“. Werkstatt mit Firma und USt-IdNr. eintragen, dann zurück auf „Privatkunde“. „Fehlerspeicher ausgelesen: ja“, Gerät „VCDS“, dann „nein“. Senden.
- **Ist:** `leistung: {freigabeArt:"kv", freigabeBis:"500"}`, `versand: {rueck:"abholung", versicherung:true, warenwert:"1500"}`, `kontakt: {typ:"privat", firma:"Alt GmbH", ustid:"DE123456789"}`, `fahrzeug: {ausgelesen:"nein", diagnosegeraet:"VCDS"}`, bei Abholung `abwAdresse:true` samt Lieferadresse. `zusammenfassungText` ist dagegen sauber. Ein Server, der die Felder auswertet, versichert dann eine Abholung oder gibt 500 € frei.
- **Korrektur:** In `datensatz()` (Zeile 1028) nicht `Z.fahrzeug`, `Z.leistung`, `Z.versand`, `Z.kontakt` roh übergeben, sondern bereinigte Kopien: abhängige Felder leeren, wenn die Bedingung nicht gilt (dieselben Bedingungen wie in `abschnitte()`).

---

## Klein

1. **Fortschrittsleiste mobil:** Unter 760 px sind die Schritt-Schaltflächen 44 × 5 px groß (nur der Balken). Korrektur: `min-height: 24px` und Balken per `::before` zentrieren oder die Schaltflächen mobil nicht anklickbar machen (Zeile 114).
2. **Kleine Tippflächen bei 360 px:** „Ändern“ 54 × 32, Chip-„×“ 30 × 30, „Eingaben löschen“ 32 hoch, Rechtstext-Links 16 hoch, Telefon/WhatsApp/E-Mail-Links 19 hoch, „Text kopieren“ 40 hoch, einzelne Symptom-Zeilen 39 hoch. Korrektur: `.ozk-btn-text` und `.ozk-chip button` auf `min-height/min-width: 44px`, Links in Listen mit `padding-block: 12px`.
3. **Platzhalter-Kontrast hell:** 3,71 : 1 (Soll 4,5). Korrektur: `opacity: .75` in Zeile 140 entfernen (dann 6,7 : 1).
4. **Fehlercode-Feld ohne sichtbare Rückmeldung:** Ungültige Eingabe (`??`) bleibt stehen, die Meldung geht nur an Screenreader und wird beim „Weiter“ still verworfen. Freitext wird zerlegt: „fehler getriebe“ ergibt die Codes `FEHLER` und `GETRIEBE`. Korrektur: Meldung sichtbar in `#f-codes-hilfe` schreiben; Muster verschärfen (mindestens eine Ziffer), Zeile 1221.
5. **Termin:** Ausweichtermin an einem Sonntag wird angenommen (06.12.2026), ebenso Feiertage (25.12.2026), obwohl die Website „So und gesetzliche Feiertage geschlossen“ nennt. Korrektur: Sonntagsprüfung auch für `wunsch2` (Zeile 1397); Feiertagshinweis als Text.
6. **Zahlenfelder:** `type="number"` nimmt je nach Browsersprache kein Komma an; „499,90“ wurde im Test zu 49990. Beim Warenwert fehlt die Obergrenze in `pruefe4` (Zeile 1404). Korrektur: `type="text"` mit `inputmode="decimal"` und eigener Prüfung.
7. **FIN mit Leerzeichen:** `maxlength=17` schneidet eine mit Leerzeichen eingefügte FIN ab („wvw zzz 1kz aw 00“). Korrektur: `max: 24` und Leerzeichen bei der Eingabe entfernen (Zeile 1257).
8. **Preis 0 und Sonderwerte:** `preisNetto: 0` beim Gerät ergibt „ohne Aufpreis“ und „Voraussichtliche Summe ab 0,00 €“. `"1.234"` als Text wird als 1,23 € gelesen. Negative Werte werden still zu „kein Preis“. Korrektur: beim Start eine Konfigurationsprüfung mit Konsolenwarnung; bei 0 „kostenlos“ nur für Zusatzpositionen.
9. **Wortwahl:** „Rückversand: Selbstabholung in Bochum“ in der Preisübersicht; bei Einbau heißt die Überschrift „Arbeitskarte drucken“, die Schaltfläche „Arbeitskarte / Begleitschein drucken“ (Zeile 1520). Sonst keine Rechtschreib- oder Grammatikfehler gefunden, Sie-Form durchgehend.
10. **Drucken vor Schritt 6:** Strg+P in Schritt 2–5 erzeugt eine echt aussehende Arbeitskarte ohne Auftragsnummer („–“), mit leerem Absender und Unterschriftszeile. Korrektur: in `druckbogenFuellen()` (Zeile 1592) den Hinweistext zeigen, solange `Z.schritt < 6`.
11. **Honigtopf:** Das Feld wird aus dem Datensatz gelöscht (Zeile 1036), der Server kann es also nicht prüfen; Bots, die direkt an den Endpunkt senden, hält es nicht auf. Füllt eine Autofill-Erweiterung das unsichtbare Feld, scheitert jedes Senden dauerhaft mit „Die automatische Prüfung hat die Übermittlung abgelehnt“. Korrektur: Feld als `_hp` mitsenden und serverseitig prüfen oder README-Aussage abschwächen; Wert beim Zeichnen von Schritt 5 leeren.
12. **Doppelte Aufträge möglich:** Nach „übermittelt“ lassen sich Angaben ändern und derselbe Auftrag mit gleicher Nummer erneut senden. Bei Zeitüberschreitung kann der Server den Auftrag trotzdem erhalten haben; der Kunde sendet dann noch einmal oder per E-Mail. Korrektur: Fehlermeldung bei Zeitüberschreitung ergänzen („möglicherweise angekommen – bitte nicht doppelt senden, sondern anrufen“), nach Änderung eine neue Nummer oder einen Zähler vergeben; Dublettenprüfung am Server steht schon in der README.
13. **Erfolg nur nach Statuscode:** Eine Antwort `200` mit `{"ok":false}` gilt als übermittelt. Viele Webhook-Dienste antworten immer mit 200. Korrektur: optional `ok === true` im Antworttext verlangen; in README erwähnen.
14. **FAQ „Was passiert mit meinen Eingaben?“:** „bleiben bis zum Absenden nur in diesem Browser-Tab“ – sie bleiben auch nach dem Absenden bis zum Schließen des Tabs im sessionStorage. Korrektur: Text anpassen oder nach Erfolg anbieten, die Daten zu löschen.
15. **Eigenständige Seite ohne Pflichtlinks:** `/konfigurator/` ist nach Weg A direkt aufrufbar und indexierbar, hat aber im Fuß nur den Link zur Startseite, kein Impressum und keinen Datenschutzlink. Korrektur: beide Links in `kopfUndRahmen()` (Zeile 1631) ergänzen; für die iframe-Quelle `<meta name="robots" content="noindex">` vorsehen.
16. **Schriftgröße:** `.ozk { font-size: 16px }` (Zeile 70) ignoriert die Schriftgrößen-Einstellung des Browsers; Beschriftungen in `rem` wachsen mit, Fließtext und Eingabefelder nicht. Korrektur: `font-size: 1rem`.
17. **Fehlerliste und Schritt-Überschrift ohne sichtbaren Fokus** (programmatischer Fokus, `outline: none`, Zeile 79). Zulässig, aber für sehende Tastaturnutzer wäre ein dezenter Rahmen an der Fehlerliste hilfreich.
18. **Langer Text ohne Leerzeichen:** Bei 80 Zeichen ohne Umbruch in Firma/Name kollabiert die Empfängerspalte des Adressaufklebers auf ein Wort pro Zeile. Korrektur: `.ozk-druck-schnitt { grid-template-columns: minmax(0,1fr) minmax(0,1fr) }` und `overflow-wrap: anywhere` für `.ozk-druck-von`.
19. **Zahlungshinweis:** „Sie zahlen erst, nachdem Sie von uns eine Rechnung erhalten haben“ (Zeile 1451) ist eine feste Zusage ohne Konfigurationsschalter. Steht als Annahme in der README; besser als Text in die Konfiguration verlagern.
20. **Formulierungen nahe an Wettbewerbertext:** Zwei Wendungen decken sich mit den ecu.de-Auszügen in den Recherchenotizen („… ausgebaut oder die Batterie abgeklemmt wird“, „nach dem Einbau eine Grundeinstellung mit [einem] Diagnosetester“). Der Aufbau (Gerätesuche, Begleitschein, Packliste) ist branchenüblich. Sonst keine Übereinstimmungen über sechs Wörter. Korrektur: beide Sätze umformulieren.

---

## README: Abgleich mit dem Code

**Stimmt:** Alle genannten Konfigurationsschlüssel existieren (`geraete[].preisNetto`, `bearbeitungstage`, `express.aufpreisNetto`, `einbau.preisNetto`, `versand.rueckweg`, `versand.versicherung.preisNetto`, `allgemein.garantieMonate`, `allgemein.pruefpauschaleNetto`, `allgemein.farbschema`, `submit.endpoint`, `submit.buttonText`, `submit.abschlussHinweis`, `labelService.aktiv`, `labelService.preisNetto`, `angebotUrl`, `fehlercodes`). Die Ersatztexte bei `null` stimmen. `aktiv: false` blendet Express, Einbau und Versicherung aus; `labelService.aktiv: true` zeigt die Label-Option. Direktlinks `?geraet=` und `?code=` funktionieren, alle zehn Geräte-IDs existieren. Der JSON-Aufbau entspricht dem Beispiel (zusätzlich vorhanden: `quelle`, `geraet.kennung`, `geraet.einstieg`, `preise.mwstProzent`, `brutto`, `summeNetto`). „übermittelt“ erscheint nur bei 2xx. sessionStorage-Aussage stimmt; localStorage, Cookies und IndexedDB bleiben leer. Der DHL-Abschnitt ist technisch stimmig, verlangt Zugangsdaten ausdrücklich nur auf dem Server; in `index.html` stehen keine Schlüssel. Der DHL-Link antwortet mit 200.

**iframe-Schnipsel (Weg A) getestet:** Mit einer kleinen Host-Seite über HTTP bei 1280 und 375 px. Die Höhe passt sich in allen sechs Schritten, bei geöffneten FAQ und geöffnetem Kopierfeld an, kein innerer Scrollbalken. `theme=dunkel` und `kopf=0` wirken. Bei Fehlern scrollt die Host-Seite zum iframe-Anfang. Der Druck läuft im iframe-Fenster. Keine Fremdanfragen.

**Abweichungen:**

- R1 (wichtig, siehe W8): „ab 400 €“ auf der Website ist nicht belegt.
- R2 (klein): Weg B zeigt `data-theme="dunkel"` am `div`. `start()` überschreibt das Attribut mit `allgemein.farbschema` („auto“), Zeile 1754. Korrektur: Hinweis in der README, dass das Schema über die Konfiguration gesetzt wird, oder das Attribut im HTML als Vorgabe respektieren.
- R3 (klein): In Weg B stehen `<style>` und `<script>` hinter `</SiteLayout>`. Sauberer ist es, sie in den Slot des Layouts zu setzen. Nicht getestet (kein Astro vorhanden).
- R4 (klein): Öffnet man die Host-Seite von der Festplatte (`file://`), bleibt die iframe-Höhe bei 1400 px, weil die Herkunftsprüfung dort nicht greift. Betrifft nur die lokale Vorschau; einen Satz dazu ergänzen.
- R5 (klein): „Der vorbereitete Text ist bewusst gekürzt“ – die Längenprobleme aus W1 fehlen.
- R6 (klein): DHL-Listenpreise 2026 und die Angaben zu Sendcloud, Returns API und Vertragsschwellen konnte ich nicht nachprüfen; sie sind in der README als zu prüfen gekennzeichnet.

**Liste der offenen Punkte – es fehlen:**

- Steuerliche Darstellung für Werkstätten und Auslandskunden (W4).
- Längengrenze des E-Mail-/WhatsApp-Wegs als Grund für den Endpunkt (W1).
- Bestätigung der Öffnungszeiten und Feiertagsregel für die Terminanfrage. Die Website nennt aktuell Mo–Fr 9–18, Sa 9–13, das deckt sich mit der Konfiguration; die Recherchenotizen zeigen aber ältere abweichende Angaben in Verzeichnissen.
- Impressum- und Datenschutzlink sowie `noindex` für die eigenständige Konfigurator-Seite (Klein 15).
- Umgang mit Anfragen für nicht gelistete Geräte (W5).
- Serverseitige Prüfung der Zustimmungen (K1) und des Honigtopfs (Klein 11).
- Freigabe der Fachtexte zu Fehlercodes durch den Meister (W9) – bisher nur „Zuordnung prüfen“.

---

## Geprüft und in Ordnung

**Funktion**
- Fehlercode P1735 (auch `p1735`, `P173500`, `p 17-35`) schlägt DQ381 und DQ500 vor; P1736/P0805 ebenso; P17BF/P189C/P0841 → DQ200; 0717–0723 → 722.9; unbekannter Code zeigt alle Geräte mit neutralem Hinweis. Der Code wird in Schritt 2 übernommen.
- Teilenummern für alle neun Gerätetypen werden erkannt, die Nummer wird in Schritt 2 übernommen.
- Manuelle Auswahl, „nicht gelistet“, Einbau mit Terminanfrage (Sonntag wird beim Wunschtermin abgelehnt, Vergangenheit ebenso), Privat- und Werkstattkunde (Rechnung nur für Werkstatt, Barzahlung nur vor Ort, Widerrufserklärung nur für Privat).
- Zurück/Weiter behält alle Eingaben; Neuladen stellt Schritt, Daten und Auftragsnummer wieder her; „Eingaben löschen“ mit Rückfrage leert alles. Defekter sessionStorage-Inhalt führt zu einem sauberen Neustart. Gesperrter Speicher (sandboxed iframe) läuft ohne Fehler.
- Pflichtfeldprüfungen bei „Weiter“: Baujahr 1980–2027, FIN-Länge und -Zeichen, PLZ, E-Mail, Telefon, USt-IdNr., Freigabegrenze 1–20.000.

**Preise und Wortlaut**
- Mit `null`-Preisen erscheint nirgends ein Eurobetrag (außer der vom Kunden gesetzten Freigabegrenze und dem Warenwert). Texte: „Preis nach Eingangsprüfung“, „auf Anfrage“, „wird im Kostenvoranschlag ausgewiesen“, „Gesamtpreis laut Kostenvoranschlag“.
- Ohne `garantieMonate`, `bearbeitungstage`, `pruefpauschaleNetto` erscheint keine Aussage zu Garantie, Dauer oder Prüfkosten. Mit Werten erscheinen sie korrekt (Garantie auch als FAQ-Eintrag).
- Mit Preisen: 400 → „ab 476,00 € inkl. MwSt. (400,00 € netto)“, deutsches Zahlenformat mit Tausenderpunkt, „ab“ nur bei Ab-Preisen und an der Summe, Summe nur wenn alle Positionen bepreist sind, Express/Versicherung/Rückversand/Einbau gehen richtig in die Summe ein (bis auf W2/W3). Kein falsches „zzgl.“.

**Robustheit und Sicherheit**
- HTML und Skript in jedem Feld (auch Teilenummer, Codes, Referenz, URL-Parameter) werden als Text angezeigt; kein Skript läuft, keine fremden Elemente in Zusammenfassung oder Druckbogen. Anführungszeichen, Umlaute, ß, Emoji, Zeilenumbrüche bleiben im JSON unverändert.
- `mailto:` und `wa.me` sind korrekt kodiert (genau zwei Parameter, keine rohen Sonderzeichen, dekodierbar).
- Endpunkt 400, 404, 429, 500, Zeitüberschreitung, Umleitungsschleife, offline: jeweils Fehlermeldung mit `role="alert"`, Fokus auf der Meldung, „Erneut senden“ und E-Mail/WhatsApp als Ersatz, nie „übermittelt“. Erneutes Senden nach Offline funktioniert.
- Doppelklick und dreifacher Klick senden genau eine Anfrage. Anfrage ohne Cookies (`credentials: "omit"`), `Content-Type: application/json`.
- Vor dem Klick auf „Senden“ geht keine Anfrage hinaus. Keine externen Anfragen (Schriften, Bilder, Analyse) in allen Abläufen; funktioniert von der Festplatte.
- Honigtopf blockiert das Senden und ist nicht per Tab erreichbar.

**Barrierefreiheit und Bedienung**
- Kompletter Durchlauf nur mit Tastatur: sinnvolle Tab-Reihenfolge, Pfeiltasten in Radiogruppen funktionieren trotz Neuzeichnen, Fokus bleibt auf dem bedienten Element, Enter im Textfeld löst „Weiter“ aus, Enter im Textbereich nicht, Fokus springt nach Schrittwechsel auf die Überschrift und bei Fehlern auf die Fehlerliste, Fehlerlinks führen zum Feld.
- Jedes Bedienelement hat einen Namen; Radiogruppen haben `fieldset`/`legend`; `aria-describedby` zeigt auf vorhandene Hilfe- und Fehlertexte; `aria-invalid` wird gesetzt; keine doppelten IDs; Überschriftenfolge ohne Sprünge; Statusmeldungen über `role="status"`.
- Fokusring an allen Tab-Stopps sichtbar (6,4 : 1 hell, 8,9 : 1 dunkel).
- Kontrast hell / dunkel: Haupttext 18,6 / 15,7; Hinweistext 6,7 / 7,4 (auf Fläche 2: 6,1 / 6,9); weiße Schrift auf rotem Knopf 5,25 (Hover 6,24); Links 6,9 / 7,4; Fehlertext 6,9 / 8,1 (auf Fehlerfläche 6,1 / 7,8); Feldrand 3,2 / 3,5. Alles über den AA-Schwellen.
- Kein waagerechter Überlauf bei 360, 768, 1280 px und bei 200 % Zoom (640 px breit). Bei 320 px nur die Preisübersicht (W6).
- `prefers-reduced-motion`: Übergänge sind dann abgeschaltet; kein weiches Scrollen.

**Druck**
- Im Druckmedium ist nur `#ozk-druckbogen` sichtbar, auch im dunklen Schema schwarz auf weiß, Format A4. Kopf mit Firmendaten, Auftragsnummer, Datum, alle Abschnitte, Preise, Bestätigungen, Packliste mit Kästchen, Werkstattvermerke, Unterschriftszeile mit Namen, Aufkleber mit Empfänger samt Zusatz und Absender (Firma bei Werkstatt, Land bei Ausland). Bei Einbau entfallen Packliste und Aufkleber. 2.000 Zeichen Beschreibung und 1.000 Zeichen Reparaturversuche werden vollständig gedruckt.

**Inhalt**
- Firmendaten stimmen mit Impressum und Kontaktseite überein (OZ Performance GmbH, Coloniastraße 21, 44892 Bochum, 0234 54453755, info@ozperformance.de, Öffnungszeiten). Links zu AGB, Datenschutz, Widerruf und beiden Angebotsseiten antworten mit 200.
- Alle vier Rechtstexte und der Abschlusshinweis tragen sichtbar „[Text vom Anwalt prüfen lassen]“.

## Nicht prüfbar

- Firefox, Safari/WebKit, echte Mobilgeräte, echter Druckdialog und Papierausdruck (nur Chromium-PDF).
- Verhalten echter Mailprogramme und von WhatsApp bei langen Texten; `wa.me` war aus der Testumgebung nicht erreichbar, die WhatsApp-Nummer ist nur gegen die Recherchenotizen abgeglichen.
- Screenreader (NVDA, VoiceOver) – nur Struktur und Attribute geprüft.
- Astro-/Wix-Einbindung nach Weg B und die Server-Route aus der README.
- DHL-Listenpreise 2026, Sendcloud- und DHL-API-Angaben.
- Rechtliche Bewertung (Button-Lösung, Widerruf, Preisangaben, Umsatzsteuer Ausland).
- Ob OZ Performance die im Katalog genannten Geräte tatsächlich im Einsendegeschäft repariert.

## Testmaterial

Skripte und Ergebnisse liegen unter `/tmp/claude-0/-home-user-open-source/636b991d-d1e6-53a1-a80d-5c89433afd35/scratchpad/pruefer/` (`t1_paths.js` bis `t9_misc.js`, `lib.js`; PDFs und Screenshots in `out/`). Der Ordner ist flüchtig.
