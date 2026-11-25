# Steuergeräte-Reparatur-Konfigurator – OZ Performance GmbH

Ein Einsende-Assistent für die Website: Der Kunde wählt sein Getriebesteuergerät bzw. seine Mechatronik, beschreibt Fahrzeug und Fehler, legt Versand und Zahlungswunsch fest, druckt eine Arbeitskarte für das Paket und schickt den Auftrag ab.

**Stand:** Entwurf, lokal getestet, noch nicht auf der Website eingebunden. An der Live-Website und in Wix wurde nichts geändert.

## 1. Was ist enthalten

| Datei | Zweck |
|---|---|
| `index.html` | Der komplette Konfigurator in einer Datei (Gestaltung, Konfiguration, Programm). Lädt nichts von außen: keine Schriften, keine Skripte, kein Tracking. |
| `README.md` | Diese Anleitung. |
| `vorschau/` | Bildschirmfotos und eine Muster-Arbeitskarte als PDF (mit erfundenen Daten „Max Mustermann“). |

Ablauf für den Kunden (6 Schritte):

1. **Gerät finden** – per Getriebeliste, Teilenummer oder Fehlercode (z. B. P1735 → Vorschlag DQ381 / DQ500).
2. **Fahrzeug & Fehler** – Marke, Modell, Baujahr, FIN, Kilometerstand, Fehlercodes, Symptome, Beschreibung. Dazu der Hinweis, was eingesandt werden soll und was nicht.
3. **Leistung & Optionen** – Express-Bearbeitung, Einbau in Bochum, Kostenfreigabe.
4. **Versand** – Hinweg und Rückweg. Bei „Einbau in Bochum“ stattdessen eine **Terminanfrage**.
5. **Kontakt & Zahlung** – Privat oder Werkstatt, Adresse, Zahlungswunsch, Einwilligungen.
6. **Zusammenfassung** – Auftragsnummer, Arbeitskarte drucken, Auftrag senden.

Die Eingaben bleiben im Browser-Tab erhalten (sessionStorage), bis der Tab geschlossen oder „Eingaben löschen“ gewählt wird.

## 2. Preise, Geräte und Texte ändern

Alles Geschäftliche steht in `index.html` im Block **`<script id="ozk-konfiguration">`** (in der Datei nach „KONFIGURATION“ suchen). Die Datei lässt sich mit jedem Texteditor öffnen. Die Regeln stehen oben im Block, kurz:

- Preise sind Zahlen **netto**, mit Punkt statt Komma, ohne Anführungszeichen: `preisNetto: 400,`
- `null` heißt „noch kein Preis“. Der Kunde sieht dann einen Hinweistext statt eines Betrags.
- `true` / `false` schaltet eine Option ein oder aus.

| Was | Wo im Block | Anzeige bei `null` |
|---|---|---|
| Reparaturpreis je Gerät | `geraete` → `preisNetto` | „Preis nach Eingangsprüfung – Sie erhalten vorab einen Kostenvoranschlag“ |
| Bearbeitungszeit je Gerät | `geraete` → `bearbeitungstage` (Text) | Zeile wird nicht angezeigt |
| Express-Aufpreis | `express.aufpreisNetto` | „auf Anfrage“ |
| Einbau in Bochum | `einbau.preisNetto` | „wird im Kostenvoranschlag ausgewiesen“ |
| Rückversand-Arten | `versand.rueckweg` → `preisNetto` | „Preis wird im Kostenvoranschlag ausgewiesen“ |
| Höherversicherung | `versand.versicherung.preisNetto` | wie oben |
| Garantie | `allgemein.garantieMonate` | keine Aussage zur Garantie |
| Prüfpauschale | `allgemein.pruefpauschaleNetto` | wird nicht erwähnt |

Sobald eine Zahl eingetragen ist, rechnet der Konfigurator die Mehrwertsteuer selbst: aus `preisNetto: 400` wird „ab 476,00 € inkl. MwSt. (400,00 € netto)“. Sind alle Positionen eines Auftrags bepreist, erscheint zusätzlich eine Summe.

**Im Auslieferungszustand sind alle Reparatur- und Versandpreise `null`.** Es wird dem Kunden also kein Betrag gezeigt, den Sie nicht selbst festgelegt haben. Die DHL-Listenpreise stehen nur als Kommentar zur Orientierung in der Datei.

**Neues Gerät anlegen:** einen vorhandenen Block in `geraete` kopieren, `id` neu vergeben (klein, ohne Leerzeichen), Texte anpassen. **Neuen Fehlercode zuordnen:** in `fehlercodes` ergänzen; nur Codes eintragen, deren Zuordnung fachlich sicher ist.

Ebenfalls dort: Firmendaten, Öffnungszeiten, Zahlungsarten, Länder, Verpackungstipps, Packliste, die Texte „So läuft es ab“ und die häufigen Fragen.

## 3. Auf die Website bringen

Die Website ist ein von Wix verwaltetes Astro-Projekt. Es gibt drei Wege, die sich kombinieren lassen.

### Weg A: als iframe einbetten (schnellster Weg)

1. `index.html` in das Astro-Projekt legen, z. B. als `public/konfigurator/index.html`. Sie ist dann unter `/konfigurator/` erreichbar.
2. Auf der gewünschten Seite einfügen:

```html
<iframe id="oz-konfigurator" src="/konfigurator/?theme=dunkel&kopf=0"
        title="Steuergerät zur Reparatur einsenden"
        style="width:100%;border:0;height:1400px" loading="lazy"></iframe>
<script is:inline>
  // Passt die Höhe des iframes an den Inhalt an und springt beim Schrittwechsel nach oben.
  window.addEventListener("message", function (e) {
    if (e.origin !== window.location.origin) return;
    var d = e.data, f = document.getElementById("oz-konfigurator");
    if (!d || d.quelle !== "oz-konfigurator" || !f) return;
    if (d.typ === "hoehe") f.style.height = d.hoehe + "px";
    if (d.typ === "nach-oben" && f.getBoundingClientRect().top < 0) f.scrollIntoView({ block: "start" });
  });
</script>
```

Parameter in der Adresse: `theme=dunkel` oder `theme=hell` (ohne Angabe richtet sich das Schema nach dem Gerät des Besuchers), `kopf=0` blendet Überschrift und „So läuft es ab“ aus, wenn die Seite das schon selbst zeigt.

### Weg B: als eigene Astro-Seite oder Komponente

Die Datei besteht aus drei klar markierten Blöcken, die sich direkt übernehmen lassen. Alle Styles sind unter `.ozk` gekapselt und kollidieren nicht mit dem Website-CSS.

```astro
---
// src/pages/steuergeraet-einsenden.astro
import SiteLayout from "../layouts/SiteLayout.astro";
---
<SiteLayout title="Steuergerät zur Reparatur einsenden | OZ Performance Bochum">
  <div class="ozk" id="ozk-wurzel" data-theme="dunkel"> … Inhalt des div aus index.html … </div>
</SiteLayout>

<style is:global> … Inhalt von <style id="ozk-styles"> … </style>
<script is:inline> … Inhalt von <script id="ozk-konfiguration"> … </script>
<script is:inline> … Inhalt von <script id="ozk-programm"> … </script>
```

Hinweise für die Entwicklung:

- `is:inline` verhindert, dass Astro die Skripte bündelt; die Reihenfolge (erst Konfiguration, dann Programm) muss erhalten bleiben. Die Konfiguration kann auch als eigene Datei `public/konfigurator/config.js` ausgelagert und per `<script is:inline src="…">` vor dem Programm geladen werden.
- Die Klasse `ozk-seite` am `<body>` wird in Astro nicht gebraucht. `min-height:100vh` an `.ozk` bei Bedarf entfernen.
- Der Druck funktioniert auch eingebettet: Das Programm hängt die Arbeitskarte als `#ozk-druckbogen` direkt an `<body>` und blendet beim Drucken alle anderen direkten Kinder von `<body>` aus.
- Die neue Seite sollte in die Sitemap. Laut Website-Audit fehlen dort derzeit viele Unterseiten.
- Die Schriften der Website (Archivo, Inter) werden bewusst nicht geladen. Liegen sie später selbst gehostet vor, genügt es, `--ozk-schrift` im Style-Block zu ändern.

### Weg C: von Angebotsseiten verlinken

Direktlinks wählen das Gerät vor oder starten mit einem Fehlercode:

- `/konfigurator/?geraet=dq381` – mögliche Werte: `dq200`, `dq250`, `dq381`, `dq500`, `dl501`, `multitronic`, `zf6hp`, `zf8hp`, `mb7229`, `anderes`
- `/konfigurator/?code=P1735`

Beispiel für die Seite `/angebote/getriebesteuergeraet-reparatur-dq381-dq500`: Schaltfläche „Steuergerät einsenden“ → `/konfigurator/?geraet=dq381`. Umgekehrt verlinkt der Konfigurator bei DQ200, DQ381 und DQ500 auf die passende Angebotsseite (`angebotUrl` im Katalog).

## 4. Auftragsübermittlung anbinden

### Zustand ohne Anbindung (Auslieferung)

`submit.endpoint` ist `null`. In Schritt 6 erhält der Kunde zwei Schaltflächen: **per E-Mail senden** (öffnet sein Mailprogramm mit vorbereitetem Text an info@ozperformance.de) und **per WhatsApp senden**. Dazu ein Feld zum Kopieren des Textes. Der Konfigurator behauptet in diesem Fall nie, der Auftrag sei übermittelt; er weist darauf hin, dass der Kunde die Nachricht selbst absenden muss. Das funktioniert sofort, ist aber fehleranfällig (kein Mailprogramm eingerichtet, Kunde sendet nicht ab). Der vorbereitete Text ist bewusst gekürzt; vollständig stehen die Angaben auf der Arbeitskarte.

### Mit Server-Anbindung (empfohlen)

In der Konfiguration eintragen: `endpoint: "https://…"`. Der Konfigurator sendet dann per `POST` ein JSON (`Content-Type: application/json`) und zeigt „übermittelt“ **nur** bei einer Antwort mit Status 200–299. Bei Fehler oder Zeitüberschreitung erscheint eine Fehlermeldung und die E-Mail-/WhatsApp-Wege werden als Ersatz angeboten.

Aufbau des Datensatzes (gekürzt):

```json
{
  "auftragsnummer": "OZ-261125-K7QX",
  "erstelltAm": "2026-11-25T10:15:00.000Z",
  "art": "reparaturauftrag",
  "geraet": { "id": "dq381", "name": "DSG 7-Gang DQ381", "teilenummer": "…", "gesuchterFehlercode": "P1735" },
  "fahrzeug": { "marke": "…", "modell": "…", "baujahr": "2019", "fin": "…", "codes": ["P1735"], "symptome": ["…"], "beschreibung": "…" },
  "leistung": { "express": false, "einbau": false, "freigabeArt": "limit", "freigabeBis": "500" },
  "versand": { "hin": "selbst", "rueck": "standard", "versicherung": true, "warenwert": "1500" },
  "termin": null,
  "kontakt": { "typ": "privat", "vorname": "…", "email": "…", "zahlung": "ueberweisung" },
  "zustimmungen": { "agb": { "erteilt": true, "text": "…" } },
  "preise": { "positionen": [ { "name": "…", "netto": null, "anzeige": "Preis nach Eingangsprüfung" } ], "summeBrutto": null },
  "zusammenfassungText": "Reparaturauftrag OZ-261125-K7QX …"
}
```

`zusammenfassungText` enthält den kompletten Auftrag als lesbaren Text und kann unverändert in eine E-Mail übernommen werden.

Drei Möglichkeiten für die Gegenstelle:

1. **Webhook eines Automatisierungsdienstes** (z. B. Make, Zapier, n8n): Webhook-Adresse als `endpoint` eintragen; der Dienst schickt eine E-Mail an die Werkstatt, eine Bestätigung an den Kunden und legt eine Zeile in einer Tabelle an. Schnell eingerichtet; Auftragsverarbeitungsvertrag (AVV) mit dem Anbieter und Serverstandort klären.
2. **Eigener Endpunkt im Astro-/Wix-Projekt** (sauberste Lösung): eine Server-Route, z. B. `src/pages/api/reparaturauftrag.ts`, die den Datensatz prüft, in einer Wix-CMS-Sammlung „Reparaturaufträge“ speichert und Benachrichtigungen auslöst. Grundgerüst:

   ```ts
   import type { APIRoute } from "astro";
   export const prerender = false;
   export const POST: APIRoute = async ({ request }) => {
     const auftrag = await request.json();
     if (!auftrag?.auftragsnummer || !auftrag?.kontakt?.email) return new Response("ungültig", { status: 400 });
     // 1. serverseitig prüfen (Pflichtfelder, Längen), Auftragsnummer auf Eindeutigkeit prüfen oder neu vergeben
     // 2. speichern (z. B. Wix-CMS-Sammlung über das Wix SDK)
     // 3. E-Mail an die Werkstatt und Bestätigung an den Kunden auslösen
     return new Response(JSON.stringify({ ok: true }), { status: 200, headers: { "Content-Type": "application/json" } });
   };
   ```

   Die genauen SDK-Aufrufe hängen vom Projektaufbau ab und sind hier nicht ausprogrammiert.
3. **Formular-/E-Mail-Dienst**, der JSON per POST annimmt und als E-Mail weiterleitet. Auch hier AVV und Serverstandort prüfen.

Für alle Varianten gilt:

- Liegt der Endpunkt auf einer anderen Domain als der Konfigurator, muss er **CORS** erlauben (`Access-Control-Allow-Origin` für die Website, Methode `POST`, Header `Content-Type`).
- Die Auftragsnummer entsteht im Browser (Datum + 4 Zufallszeichen). Das ist praktisch eindeutig, aber nicht garantiert. Der Server sollte Dubletten abfangen.
- Alle Prüfungen im Browser sind Komfort. Der Server muss die Daten selbst noch einmal prüfen. Ein einfaches Honigtopf-Feld gegen Formular-Bots ist eingebaut; ein Missbrauchsschutz am Server (Begrenzung der Anfragen) ist trotzdem sinnvoll.
- In `index.html` stehen niemals Zugangsdaten oder geheime Schlüssel. Jeder Besucher kann die Datei lesen.

## 5. DHL: Wie kommt das Paket zum Kunden und zurück?

### Stufe 1 – ohne DHL-Vertrag (Auslieferungszustand)

- **Hinweg:** Der Kunde wählt „Ich versende selbst“. Er sieht Versandadresse und Verpackungstipps und gelangt per Schaltfläche zur **DHL Online Frankierung** (`https://www.dhl.de/de/privatkunden/pakete-versenden/online-frankieren.html`, am 25.11.2026 erreichbar). Dort kauft er die Paketmarke selbst. Der Adressaufkleber auf der Arbeitskarte ist ausdrücklich **keine** Paketmarke.
- **Rückweg:** Sie frankieren selbst (Online Frankierung oder Filiale) und berechnen die Versandkosten. Die Preise dafür tragen Sie in `versand.rueckweg` ein.
- Orientierung, öffentliche DHL-Listenpreise für Privatkunden 2026: Paket bis 5 kg 7,69 €, bis 10 kg 10,49 €, bis 31,5 kg 23,99 €; Express national online bis 10 kg 30,00 €; Samstagszustellung +11,90 €; Transportversicherung bis 2.500 € +6,99 €. Standardhaftung 500 € je Paket, das liegt unter dem Wert vieler Mechatroniken. Für 2027 sind neue Preise angekündigt. Bitte vor dem Eintragen auf dhl.de prüfen.
- Möglich ohne Vertrag, aber Handarbeit: Sie kaufen nach Auftragseingang selbst eine Marke in der Online Frankierung (Absender Kunde, Empfänger OZ) und mailen sie dem Kunden.

### Stufe 2 – Versand-Tool (z. B. Sendcloud)

Dienste wie Sendcloud erzeugen Versand- und Rücksendelabels über eigene Tarife, laut Anbieter auch ohne eigenen DHL-Vertrag; ein eigener Vertrag lässt sich dort später hinterlegen. Ablauf: Ihr Server (siehe Abschnitt 4) ruft nach Auftragseingang die Schnittstelle des Tools auf und mailt dem Kunden das Label, oder Sie erzeugen es von Hand in der Oberfläche des Tools. Die Label-Apps im Wix App Market hängen an Wix-Stores-Bestellungen und sind für ausgehende Sendungen gedacht; ob sie Einsende-Labels ohne Bestellung können, ist nicht geprüft. Aktuelle Preise und Verfügbarkeit bitte beim Anbieter ansehen.

### Stufe 3 – DHL-Geschäftskundenvertrag

- Laut DHL ab etwa 200 Sendungen pro Jahr, mit Monatspauschale und individuellen Preisen.
- **DHL Retoure**: Der Kunde bekommt ein Rücksendelabel als PDF oder als QR-Code (Druck in der Filiale). Erzeugung im Geschäftskundenportal (Retourenportal-Link) oder automatisch über die **Returns API** (benötigt die Receiver-ID aus dem Portal).
- **Shipping API (Parcel DE Shipping)** für den Rückversand: benötigt Ihre **EKP** (Kundennummer) und die 14-stellige **Abrechnungsnummer**, dazu einen API-Schlüssel aus dem DHL-Entwicklerportal und Ihren Geschäftskunden-Zugang. Vor dem Produktivbetrieb ist ein Test in der Sandbox und eine Freigabe durch DHL vorgesehen. Die API-Angaben stammen aus Sekundärquellen (das Entwicklerportal war bei der Recherche nicht abrufbar) und sind vor der Umsetzung dort zu prüfen.

> **Wichtig:** Label-Erzeugung findet **immer auf dem Server** statt. EKP, Abrechnungsnummer, API-Schlüssel und Passwörter gehören in die geschützten Einstellungen des Servers (z. B. Wix Secrets oder Umgebungsvariablen) und **niemals** in `index.html` oder anderen Code, der im Browser läuft. Der Konfigurator enthält deshalb bewusst keine DHL-Anbindung, sondern meldet nur den Wunsch des Kunden.

### Label-Option im Konfigurator einschalten

Sobald Stufe 2 oder 3 steht: in der Konfiguration `labelService.aktiv: true` setzen und `labelService.preisNetto` eintragen. Im Schritt „Versand“ erscheint dann zusätzlich „Versandlabel von OZ Performance per E-Mail“. Der Konfigurator erzeugt selbst kein Label; das erledigt Ihr Server oder Sie von Hand, nachdem der Auftrag eingegangen ist.

## 6. Offene Punkte vor dem Livegang

**Preise und Leistung**

- [ ] Reparaturpreise je Gerät festlegen (`preisNetto`) oder bewusst bei „Preis nach Eingangsprüfung“ bleiben. Hinweis: Die Website nennt für DQ381/DQ500 in der Werkstatt „ab 400 €“. Gilt das auch für eingesandte Geräte?
- [ ] Bearbeitungszeiten (`bearbeitungstage`), Garantie (`garantieMonate`) und Prüfpauschale (`pruefpauschaleNetto`) entscheiden. Solange `null`, macht der Konfigurator dazu keine Aussage.
- [ ] Express-Aufpreis und Preis für Einbau und Grundeinstellung festlegen, oder die Optionen mit `aktiv: false` ausblenden.
- [ ] Rückversandpreise und Höherversicherung eintragen. Rückversand ins Ausland klären (derzeit nur Hinweis „im Kostenvoranschlag“).
- [ ] Katalog fachlich prüfen: Beschreibungen, Symptome und vor allem **„einsenden“ / „nicht einsenden“** je Gerät sind Vorschläge (z. B. ZF 6HP/8HP: Mechatronik komplett oder nur Steuergerät?).
- [ ] Fehlercode-Zuordnung prüfen und bei Bedarf erweitern.
- [ ] Zahlungsarten an das tatsächliche Angebot anpassen (Überweisung, PayPal, bar/Karte vor Ort, Rechnung für Werkstätten sind Annahmen).
- [ ] Texte „So läuft es ab“ und die häufigen Fragen lesen und freigeben. Sie beschreiben Ihren Ablauf, unter anderem: Reparatur erst nach Freigabe bzw. innerhalb der Freigabegrenze, Zahlung nach Rechnung.

**Recht (Anwalt)**

- [ ] Alle vier Einwilligungstexte sind Platzhalter und mit „[Text vom Anwalt prüfen lassen]“ markiert. Der Vermerk ist für Kunden sichtbar, bis die Texte ersetzt sind.
- [ ] AGB um das Einsendegeschäft ergänzen: Haftung für nicht aufgeführte Teile, Vorgehen bei nicht reparierbaren Geräten, Fremdeingriffe, Versandrisiko, Aufbewahrung und Rücksendung.
- [ ] Widerrufsbelehrung für Fernabsatz-Dienstleistungen und Erklärung zum vorzeitigen Leistungsbeginn prüfen lassen.
- [ ] Klären, ob das Absenden ein **verbindlicher Auftrag** oder eine **unverbindliche Anfrage** sein soll. Davon hängen Beschriftung der Schaltfläche („Button-Lösung“ bei zahlungspflichtigen Verbraucherverträgen im Internet), Hinweistext (`submit.buttonText`, `submit.abschlussHinweis`) und die nötige Bestätigungs-E-Mail ab.
- [ ] Preisangaben: Verbrauchern werden Bruttopreise gezeigt (Netto in Klammern). Pflichtangaben zu Versandkosten prüfen lassen.

**Datenschutz (DSGVO)**

- [ ] Datenschutzhinweise um den Konfigurator ergänzen: welche Daten, Zweck (Auftragsabwicklung), Rechtsgrundlage, Speicherdauer, Empfänger (Paketdienst, ggf. Webhook-/Versand-Dienst, WhatsApp).
- [ ] Festlegen, **wo Aufträge gespeichert werden** (Postfach, Wix-CMS, Tabelle), wer Zugriff hat und wann gelöscht wird.
- [ ] AVV mit jedem eingesetzten Dienstleister (Hosting/Wix, Automatisierungsdienst, Versand-Tool).
- [ ] WhatsApp als Übermittlungsweg bewusst entscheiden; sonst den WhatsApp-Weg entfernen lassen.
- [ ] Zwischenspeicher im Browser: Die Eingaben liegen im sessionStorage des Tabs (technisch notwendig, keine Cookies, kein Tracking). In den Datenschutzhinweisen erwähnen. Auf gemeinsam genutzten Rechnern bleiben sie bis zum Schließen des Tabs lesbar.

**Technik**

- [ ] Übermittlungsweg wählen und anbinden (Abschnitt 4), inklusive Bestätigungs-E-Mail an den Kunden.
- [ ] DHL-Stufe wählen (Abschnitt 5).
- [ ] Einbindung (Weg A oder B), Verlinkung von den Angebotsseiten, Aufnahme in Sitemap und Navigation.
- [ ] Farbschema festlegen (`allgemein.farbschema`; die Website ist dunkel).
- [ ] Nach der Einbindung auf echten Geräten testen: iPhone/Safari, Android/Chrome, Firefox, Ausdruck der Arbeitskarte. Bisher wurde nur in Chromium automatisiert getestet.
- [ ] Datei-Upload (Foto vom Typenschild, Fehlerprotokoll) ist nicht enthalten, weil er einen Server braucht. Bei Bedarf zusammen mit der Server-Anbindung ergänzen.
