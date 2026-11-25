# Website audit ozperformance.de (SEO and AI-search readiness, state 25 Nov 2026)

Method: live crawl with curl on 25 Nov 2026 (desktop Chrome UA plus GPTBot/ClaudeBot/PerplexityBot/OAI-SearchBot/Googlebot/bingbot UAs), seeded from the XML sitemaps and following every internal link (67 URLs fetched). Read-only Wix API look-ups (site context, Search Console connection). Nothing on the site was changed. "Verified" = observed directly in the HTTP response/HTML. Word counts are visible words in the body without header/footer/nav ("main words"); they include the repeated review block and CTA boilerplate (roughly 150-250 words per page).

Headline correction to the briefing: the site is no longer a classic Wix editor site. It was rebuilt as a Wix-managed headless project on Astro (Wix site created 21 Oct 2026, last update 14 Nov 2026). It is much larger and better structured than assumed (9 service pages, 16 fixed-price offer pages, 8 Ratgeber articles, 6 city pages, shop), but the relaunch broke the old URLs and the sitemap omits two thirds of the pages.

## 1. Which pages exist? (full inventory)

### Takeaway
67 URLs respond, of which 62 are indexable 200 pages; only 24 URLs are in the XML sitemap, and that sitemap contains the 404 page, two 301 URLs and one noindex page while omitting all 43 deep content pages (services, offers, Ratgeber, city pages, products). Old URLs known to search engines (/getriebeinstandsetzung/, /softwareoptimierung/, /leistungen/getriebeinstandsetzung) now return 404 with no redirect.

### Cited Findings

Sitemap and platform
- /sitemap.xml is a Wix-generated sitemap index with two children: pages-sitemap.xml (21 URLs, lastmod 2026-11-25) and store-categories-sitemap.xml (3 URLs, lastmod 2026-11-13). There is no product sitemap and no entry for any /leistungen/*, /angebote/*, /ratgeber/*, /standorte/* or /products/* URL — [sitemap.xml](https://www.ozperformance.de/sitemap.xml), [pages-sitemap.xml](https://www.ozperformance.de/pages-sitemap.xml), [store-categories-sitemap.xml](https://www.ozperformance.de/store-categories-sitemap.xml)
- pages-sitemap.xml lists https://www.ozperformance.de/404 (HTTP 404, noindex), /preise (301 to /leistungen), /preisrechner (301 to /termin) and /termin/verwalten (noindex) — [pages-sitemap.xml](https://www.ozperformance.de/pages-sitemap.xml)
- Root cause is visible in the Wix page registry: the dynamic routes /angebote/[slug], /leistungen/[slug], /ratgeber/[slug], /standorte/[slug], /preise/[slug], /termin/[slug], /service-page/[slug] are registered without item metadata; only /category/[slug] and /products/[slug] carry a Wix Stores identifier — [/_wix/pages.json](https://www.ozperformance.de/_wix/pages.json). Wix documents that pages-sitemap.xml is "built from your page registry ... covers your main pages and any item-page routes you registered with wixMetadata" — [Wix: About Sitemaps in the Astro Integration](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/feature-guides/seo/about-sitemaps-in-the-astro-integration)
- Wix site context: status Published, Premium plan, custom domain, editor type "Editorless", created 21 Oct 2026, updated 14 Nov 2026, language de, apps: Promote SEO, Wix Bookings, Wix Forms, Wix Invoices, Wix Payments, Wix Stores (catalog V3). No Wix Blog app installed — Wix connector GetSiteContext (site id fed338a2-82ed-4feb-b6c7-6490fb000bd4), no public URL
- HTML is served from Astro (assets under /_astro/, astro-island components), not from the Wix editor renderer — [homepage source](https://www.ozperformance.de/)

Inventory (T = title tag, D = meta description, W = main words; all canonicals are self-referencing; LD = JSON-LD types besides the site-wide AutoRepair block)

Core pages
| URL | Status | T | H1 | W | LD | Topic |
|---|---|---|---|---|---|---|
| / | 200 | OZ Performance Bochum – Getriebe-Reparatur, DSG & Mechatronik (61) | Ihr Getriebe-Spezialist in Bochum | 698 | WebSite, FAQPage (6 Q) | Brand + Getriebe Bochum; D: "Getriebe-Werkstatt in Bochum: Getriebe-Reparatur, DSG- und Mechatronik-Reparatur, Automatikgetriebe-Spülung. ZF Service Point, kostenlose Erstdiagnose." |
| /leistungen | 200 | Leistungen & Preise – Getriebe, DSG, Mechatronik Bochum \| OZ Performance (72) | Getriebetechnik vom Spezialisten | 261 | – | Service hub, 9 cards |
| /angebote | 200 | Getriebespülung, DSG & Mechatronik Bochum \| OZ Performance (58) | Konkrete Leistungen mit Festpreis | 229 | – | Offer hub, 16 cards |
| /ratgeber | 200 | Getriebe-Ratgeber: DSG, Ölwechsel & Kosten \| OZ Performance | Wissen rund ums Getriebe | 526 | – | Ratgeber hub, 8 articles |
| /standorte | 200 | Getriebe-Reparatur im Ruhrgebiet & Bochum \| OZ Performance | Ihre Getriebe-Werkstatt im Ruhrgebiet | 136 | – | City hub |
| /termin | 200 | Preis & Termin – Getriebe, DSG, Software Bochum \| OZ Performance | Preis & Termin · OZ Performance GmbH Bochum | 189 | – | Price calculator / booking (D is 210 chars) |
| /kontakt | 200 | Kontakt & Termin \| OZ Performance | Termin anfragen | 180 | – | Contact form, hours, map |
| /ueber-uns | 200 | Über uns \| OZ Performance | Getriebetechnik mit Haltung | 289 | – | About (no people named) |
| /galerie | 200 | Galerie \| OZ Performance | Einblicke in unsere Werkstatt | 128 | – | 28 photos |
| /videos | 200 | Videos \| OZ Performance | Werkstatt in Bewegung | 158 | – | Video embeds (no VideoObject) |
| /shop | 200 | Shop – Getriebeteile & Reparatur per Versand \| OZ Performance | Teile & Reparatur per Versand | 141 | – | Shop hub |
| /karriere | 200 | Karriere bei OZ Performance Bochum – Kfz-Mechatroniker, Meister, Bürokraft (74) | Wir suchen Verstärkung | 480 | – (no JobPosting) | 5 vacancies |
| /partner | 200 | Partner werden – Fileservice & Franchise \| OZ Performance GmbH Bochum | Werden Sie Partner der OZ Performance GmbH | 132 | – | B2B fileservice / franchise |
| /impressum, /datenschutz, /agb, /widerruf | 200 | "Impressum \| OZ Performance" etc. | – | 144 / 1181 / 2701 / 440 | – | Legal; all four share the homepage meta description |
| /termin/verwalten | 200 noindex | Termin ändern \| OZ Performance | – | 77 | – | Utility |
| /404 | 404 noindex | Seite nicht gefunden \| OZ Performance | Diese Seite gibt es nicht | 59 | – | Error page |
| /preise, /preisrechner | 301 | – | – | – | – | Redirect to /leistungen and /termin |

Service pages /leistungen/* (each: Service + BreadcrumbList, FAQPage except two)
| URL | T | H1 | W | Notes |
|---|---|---|---|---|
| /leistungen/mechatronik-reparatur | Mechatronik-Reparatur Bochum: DSG & Automatik \| OZ Performance | Mechatronik-Reparatur | 1838 | Deepest page; price tables per gearbox, fault-code lists, 13 FAQ |
| /leistungen/automatikgetriebe-spuelung | Automatikgetriebe-Spülung Bochum \| OZ Performance | Getriebespülung & Wartung | 1554 | Price tables per make/gearbox |
| /leistungen/getriebe-instandsetzung | Getriebe-Reparatur Bochum: Automatik & DSG \| OZ Performance | Getriebe-Instandsetzung | 1136 | |
| /leistungen/software-optimierung | Software-Optimierung Bochum: Kennfeld \| OZ Performance | Software-Optimierung | 964 | Only page containing the word "Chiptuning" (once) |
| /leistungen/meister-wartung | KFZ-Wartung & Inspektion Bochum \| OZ Performance | Meister-Wartung | 812 | Price table is BMW timing chains; card says "ab 1.899 €" |
| /leistungen/diagnose-technik | Getriebe-Diagnose Bochum: Fehlerspeicher \| OZ Performance | Diagnose & Technik | 670 | |
| /leistungen/dsg-reparatur | DSG-Reparatur Bochum: Kupplung & Mechatronik \| OZ Performance | DSG-Reparatur | 495 | Thin for the main DSG money page |
| /leistungen/zf-service-point | ZF Service Point Bochum: ZF-Getriebe Wartung \| OZ Performance | ZF Service Point | 320 | Thin; no FAQ; no certificate/proof |
| /leistungen/performance-upgrades | Getriebe Performance-Upgrades Bochum \| OZ Performance | Performance-Upgrades | 302 | Thin; no FAQ |

Offer pages /angebote/* (each 547-653 words, identical template: intro, bullet list, reviews, 3 FAQ, 4-step process, location block; LD Service + Offer + BreadcrumbList + FAQPage)
- dq381-dq500-drucksensor-reparatur (T "DQ381/DQ500 Drucksensor Reparatur Bochum", D names P1735, P1736, "ab 400 €"), getriebesteuergeraet-reparatur-dq381-dq500 (D: P1736, P1735, P0805), dq200-druckspeicher-reparatur (D: P17BF, P189C), dq200-0am-mechatronik-schieberkasten (D: P17BF, P189C, P1895, P0841, P1604), 0am-kupplungswechsel-dq200, audi-stronic-0b5-dl501-kupplungswechsel, mercedes-9g-steuergeraetreparatur (T includes "725.0"; D: P073E, P07B7, P0840), automatikgetriebespuelung-mercedes-9g-tronic, automatikgetriebespuelung-zf (ab 299 €), automatikgetriebespuelung-bmw-8hp-zf (ab 450 €), bmw-steuerkettenwechsel-n47-b47, bmw-steuerkettenwechsel-n57-b57, bmw-oelservice, bmw-schluesseldienst, dpf-agr-sorglospaket, adblue-reparatur — [offer hub](https://www.ozperformance.de/angebote)

Ratgeber /ratgeber/* (8 articles, 609-672 words each, Article + BreadcrumbList + FAQPage with 3 Q, all datePublished 2026-10-28)
- was-ist-dsg-doppelkupplungsgetriebe, dsg-getriebe-probleme-symptome, dsg-kupplung-wann-wechseln-kosten, auto-ruckelt-beim-anfahren, getriebe-notlauf-was-tun, getriebeoel-wechseln-intervall-kosten, getriebespuelung-oder-oelwechsel, steuerkette-wechseln-symptome-intervall — [Ratgeber hub](https://www.ozperformance.de/ratgeber)

City pages /standorte/* (446-480 words, near-identical template, Service + BreadcrumbList + FAQPage with 2 Q)
- bochum, dortmund, essen, herne, gelsenkirchen, witten; H1 pattern "Getriebe-Reparatur & DSG-Spezialist in {Stadt}". No page for Hattingen or Castrop-Rauxel although both are in areaServed (/standorte/hattingen returns 404) — [city hub](https://www.ozperformance.de/standorte)

Shop (Wix Stores)
- /category/reparatur-per-versand, /category/ersatzteile, /category/all-products (84-118 words; "All Products" is an English default title) and 4 products under /products/* (118-170 words, Product schema): getriebesteuergerät-reparatur-per-versand, getriebesteuergerät-klonen-per-versand, dq381-dq500-drucksensor-reparatur-per-versand, dq200-0am-mechatronik-schieberkasten-neuteil. Two product slugs contain the umlaut "ä" (percent-encoded in URLs) — [shop](https://www.ozperformance.de/shop)

Old vs new URLs
- Search engines still hold pre-relaunch URLs: "Getriebeinstandsetzung - OZ Performnce - Software & Getriebetechnik" at ozperformance.de/getriebeinstandsetzung/, ozperformance.de/leistungen/getriebeinstandsetzung, and "OZ Performance UG Getriebe & Motortechnik - Preise" at ozperformance.de/preise (web search result listing, 25 Nov 2026; the old pages themselves are no longer retrievable)
- Live status today: /getriebeinstandsetzung 404, /leistungen/getriebeinstandsetzung 404, /softwareoptimierung 404 (the trailing-slash form 301s to the slashless form, which then 404s), /chiptuning 404, /getriebespuelung 404, /dsg-reparatur 404, /blog 404, /faq 404; only /preise (301 to /leistungen) and /preisrechner (301 to /termin) are redirected — e.g. [/softwareoptimierung](https://www.ozperformance.de/softwareoptimierung), [/getriebeinstandsetzung](https://www.ozperformance.de/getriebeinstandsetzung)
- /angebote and /kontakt (named in the briefing) exist and return 200 — [/angebote](https://www.ozperformance.de/angebote), [/kontakt](https://www.ozperformance.de/kontakt)

Second domains
- getriebespuelung-bochum.de is a separate small PHP/nginx site (not Wix): title "Getriebespülung Bochum | Automatikgetriebe spülen lassen", H1 "Getriebespülung in Bochum für Automatik, DSG und ZF", 574 words, own sitemap with 8 URLs (/getriebespuelung-bmw, -mercedes, /dsg-getriebespuelung, -dortmund, -essen, impressum, datenschutz). Same address and phones (0234 54453755, WhatsApp 0176 45858800) but brand name "Getriebespülung Bochum", JSON-LD AutoRepair name "Getriebespülung Bochum", email info@getriebespuelung-bochum.de, "ZF Servicepoint" spelling, hours "Sa nach Vereinbarung". It does not link to ozperformance.de and never names OZ Performance on the homepage — [getriebespuelung-bochum.de](https://getriebespuelung-bochum.de/), [its sitemap](https://getriebespuelung-bochum.de/sitemap.xml)
- getriebe-bochum.com 301s to www.getriebe-bochum.com, which returns a Wix "PAGE NOT FOUND (if this is your website, you need to publish it)" 404. A search engine still lists it as "OZ Performance GmbH" — [www.getriebe-bochum.com](https://www.getriebe-bochum.com/)

### Inferences
- The 43 deep pages are discoverable only through internal links, so indexing of exactly the pages that target money and long-tail queries depends on crawl discovery rather than on the sitemap. Fix is in the Astro project (register item routes with wixMetadata or serve an own sitemap), not in the Wix dashboard.
- The missing redirects mean the old site's rankings, backlinks and any AI citations of old URLs currently land on 404. This is probably the single most damaging current defect.
- getriebespuelung-bochum.de competes with ozperformance.de for "Getriebespülung Bochum" with the same NAP under another brand name; getriebe-bochum.com is a dead asset that should be redirected or published.

### Gaps
- The pre-relaunch site could not be retrieved (no archive access), so the complete list of old URLs needing redirects is unknown; a Search Console export or Wayback crawl is required.
- Routes /preise/[slug], /termin/[slug] and /service-page/[slug] exist in the registry but no live URLs under them were found by the crawl; their content was not checked.
- Pages reachable only through JavaScript interaction (price calculator steps) were not rendered in a browser.

## 2. Content on fault codes, Getriebespülung, DSG, Mechatronik, ZF, Mercedes, Chiptuning; blog/Ratgeber

### Takeaway
Fault codes are mentioned (P1735 on 3 pages, P17BF/P189C on 5) but only as lists and one- to two-sentence FAQ answers inside offer pages; there is no dedicated fault-code page, no "VW P1735" page and no fault-code Ratgeber. Getriebespülung and Mechatronik are covered in real depth; DSG, ZF Service Point and Chiptuning are thin relative to their importance.

### Cited Findings
- P1735 appears 17 times on 3 pages: the two DQ381/DQ500 offer pages and the Mechatronik service page. The best answer on the site is the FAQ "Was bedeutet Fehler P1735 oder P1736 beim DSG DQ381 / DQ500?": "elektrischen Fehler am Positionsgeber Kupplung 1 (P1735) oder Kupplung 2 (P1736). Meist ist nicht die Kupplung defekt, sondern ein Drucksensor..." — [/leistungen/mechatronik-reparatur](https://www.ozperformance.de/leistungen/mechatronik-reparatur); offer page states price "ab 400 €", symptoms (Notlauf, Ruckeln, Gänge fallen aus) and BOSCH position sensor repair — [/angebote/dq381-dq500-drucksensor-reparatur](https://www.ozperformance.de/angebote/dq381-dq500-drucksensor-reparatur)
- No page has P1735 in title or H1, none mentions VW model names (Golf 8, Tiguan, Passat, T6.1 etc.), VAG codes 10666/10668 or the 6-digit form P173500 that competitors rank for; "VW P1735" as a phrase does not occur. /ratgeber/p1735 returns 404 — [crawl of all pages, e.g. offer page](https://www.ozperformance.de/angebote/getriebesteuergeraet-reparatur-dq381-dq500)
- P17BF and P189C: on /angebote/dq200-druckspeicher-reparatur, /angebote/dq200-0am-mechatronik-schieberkasten, the Mechatronik page, one product and the AGB. Further code lists on the Mechatronik page: DQ200 P1604, U0101, P0562, P0841, P177F, P173E, P173F, P174A, P174D; Mercedes 725.0 P07B700, P073E00, P07B571, P07B623/624, P07B634/635, P07E400, P07EF00; DQ381 P0805, P0605 — [/leistungen/mechatronik-reparatur](https://www.ozperformance.de/leistungen/mechatronik-reparatur)
- Getriebespülung: service page 1,554 words with per-gearbox price tables, plus 3 offer pages (ZF ab 299 €, BMW 8HP ab 450 €, Mercedes 9G-Tronic), plus Ratgeber "Getriebespülung oder Ölwechsel?" and "Getriebeöl wechseln: Intervall & Kosten"; homepage claims "1.500+ Getriebespülungen pro Jahr" — [/leistungen/automatikgetriebe-spuelung](https://www.ozperformance.de/leistungen/automatikgetriebe-spuelung), [homepage](https://www.ozperformance.de/)
- DSG: service page only 495 words; depth sits in offers (DQ200 clutch, Druckspeicher, Schieberkasten, DQ381/DQ500, Audi 0B5) and 3 Ratgeber articles — [/leistungen/dsg-reparatur](https://www.ozperformance.de/leistungen/dsg-reparatur)
- ZF: "8HP" on 11 pages, "6HP" on 3; ZF Service Point page has 320 words, no FAQ, no certificate number, no link to a ZF partner locator; "ZF [pro]Tech Partner" appears only as a photo caption on /ueber-uns — [/leistungen/zf-service-point](https://www.ozperformance.de/leistungen/zf-service-point), [/ueber-uns](https://www.ozperformance.de/ueber-uns)
- Mercedes: 9G/725.0 well covered (2 offers plus tables); "7G" on 4 pages and "722.9" once only — [/angebote/mercedes-9g-steuergeraetreparatur](https://www.ozperformance.de/angebote/mercedes-9g-steuergeraetreparatur)
- Chiptuning: the word occurs exactly once on the whole site; the page is positioned as "Software-Optimierung"/"Kennfeldoptimierung" (964 words, "Stage 1" on 4 pages). No vehicle- or engine-specific tuning pages, no dyno results — [/leistungen/software-optimierung](https://www.ozperformance.de/leistungen/software-optimierung)
- Ratgeber exists as coded pages (not Wix Blog): 8 articles of about 610-670 words, all published 28 Oct 2026, each opening with a "Kurz & knapp" summary, H2 questions, a Fazit and 3 FAQ. No author name, no visible date, no images beyond a shared hero, no outbound sources — [example article](https://www.ozperformance.de/ratgeber/getriebeoel-wechseln-intervall-kosten)
- Competitive context for P1735: a web search for "P1735 P1736 DQ381 Drucksensor Reparatur Bochum" returned eBay parts, absstuurapparaten.nl (dedicated pages per code) and kfz-dietrich.com (blog article marked "Fachlich geprüft"), not ozperformance.de — [absstuurapparaten.nl](https://absstuurapparaten.nl/en/pages/solution-dq381-dq500-dsg-7-error-codes-p173500-and-p173600), [kfz-dietrich.com](https://kfz-dietrich.com/blog/vw-audi-dsg-mechatronik-defekt-dq200-dq250-dq381-diagnose/)

### Inferences
- The site answers "what does OZ repair and for how much" well but not "what does code X mean on my car", which is the query type behind "VW P1735". The raw material (code lists, prices, real customer reviews mentioning P1736 on a Tiguan) is already there to build dedicated code pages.
- The 16 offer pages and 6 city pages share about 250 words of identical template text each; they are differentiated enough to index, but the city pages are close to doorway-style duplicates.
- "Chiptuning" is a high-volume term the site does not target at all.

### Gaps
- Search volumes and current rankings per keyword were not measured (no rank-tracking or Search Console access).
- Whether the text was AI-generated cannot be determined; the uniform length and structure of the 8 Ratgeber articles published on the same day suggests batch production.

## 3. Technical SEO state

### Takeaway
Technically clean base: server-side rendered HTML, self-referencing canonicals, single 301 hops, AI crawlers allowed, fast TTFB, auto-generated llms.txt. Main defects are the incomplete/polluted sitemap, missing legacy redirects, duplicated head tags on shop pages, empty alt text on price-table images and Google Fonts loaded from Google servers.

### Cited Findings
- robots.txt (Wix default, unedited): `User-agent: * Allow: / Disallow: *?lightbox=`; AdsBot rules; `User-agent: PetalBot Disallow: /`; Crawl-delay 10 for dotbot and AhrefsBot; Sitemap line. No rule names GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, Claude-SearchBot, PerplexityBot, Google-Extended, CCBot or Bingbot, so all are allowed by the wildcard — [robots.txt](https://www.ozperformance.de/robots.txt)
- Requests with GPTBot, ClaudeBot, PerplexityBot, OAI-SearchBot, Googlebot and bingbot user agents all received HTTP 200 with the identical 69 KB homepage HTML (no UA-based blocking; real bot IP ranges could not be tested) — [homepage](https://www.ozperformance.de/)
- llms.txt exists (HTTP 200, text/plain) but is the Wix auto-generated file: one homepage link plus a description of the site's MCP endpoint (/_api/mcp) and its tools; it lists no services, prices, pages or business facts. /llms-full.txt is 404. The MCP endpoint answered 401 to a plain GET — [llms.txt](https://www.ozperformance.de/llms.txt). Wix: the file is generated and maintained automatically and can be edited or reset in SEO & GEO > Tools and settings — [Wix: Understanding Your Site's llms.txt File](https://support.wix.com/en/article/understanding-your-sites-llms-txt-file)
- Rendering: all text, headings, prices, FAQ and JSON-LD are in the initial HTML (Astro SSR). Only the shop cart button/drawer are client-only islands; maps and videos load after consent. Content does not depend on JavaScript — [homepage source](https://www.ozperformance.de/)
- Redirects: https://ozperformance.de/* returns 301 to https://www.ozperformance.de/* in one hop (path preserved); trailing-slash URLs 301 to slashless; HSTS header present (max-age=31556952). URLs are case-sensitive (/KONTAKT is 404). Unknown URLs return a real 404 status — [apex](https://ozperformance.de/), [www](https://www.ozperformance.de/)
- Canonicals: every 200 page has a self-referencing canonical on https://www. Query-string URLs (/?x=1) return 200; canonical handling for parameters was not separately verified — [example](https://www.ozperformance.de/leistungen/dsg-reparatur)
- Indexability: no noindex except /404 and /termin/verwalten; no X-Robots-Tag header observed — [example](https://www.ozperformance.de/termin/verwalten)
- hreflang: none (single-language site, `<html lang="de">`, og:locale de_DE); not needed — [homepage source](https://www.ozperformance.de/)
- Mobile: viewport meta present, responsive Tailwind classes, images with srcset/sizes; not tested in a real mobile browser or Lighthouse — [homepage source](https://www.ozperformance.de/)
- Speed hints: TTFB about 0.65 s from a US data centre, Brotli compression, homepage 69 KB HTML (16 KB compressed), one 73 KB CSS file, very little JS (cart islands about 8 KB), images lazy-loaded from static.wixstatic.com. Negative: cf-cache-status BYPASS (HTML not edge-cached), no preload for the hero image, all images JPG at q_90 (no WebP/AVIF), /img/logo.png is 89 KB and served with max-age=0, _astro assets cached only 1 hour, 4 font families loaded render-blocking from fonts.googleapis.com — [homepage source](https://www.ozperformance.de/)
- Google Fonts are loaded directly from fonts.googleapis.com/fonts.gstatic.com before any consent — [homepage source](https://www.ozperformance.de/)
- Duplicate head tags on Wix Stores pages: product and category pages contain two `<title>` elements and two canonical links (one from the Astro layout, one injected with wix-seo-tags="true"), both with the same value — [product page](https://www.ozperformance.de/products/dq200-0am-mechatronik-schieberkasten-neuteil)
- Titles/descriptions: 18 of 65 titles exceed 60 characters; 4 descriptions exceed 160 (/termin 210, /partner 180, /karriere 174, /leistungen 166); the homepage description is reused on /impressum, /datenschutz, /agb, /widerruf and the 404 page; weak generic titles on /ueber-uns, /galerie, /videos, /kontakt — crawl data, e.g. [/termin](https://www.ozperformance.de/termin)
- H1s: exactly one per page, but several are slogans without keyword or place ("Getriebetechnik vom Spezialisten", "Konkrete Leistungen mit Festpreis", "Getriebetechnik mit Haltung", "Wissen rund ums Getriebe"); service-page H1s are the bare service name without "Bochum" — [/leistungen](https://www.ozperformance.de/leistungen)
- Image alt text: every img has an alt attribute, but most content images in price tables use alt="" (30 of 34 on the Spülung page, 21 of 29 on Mechatronik, 18 of 23 on Software); gallery and hero images have descriptive alts — [/leistungen/automatikgetriebe-spuelung](https://www.ozperformance.de/leistungen/automatikgetriebe-spuelung)
- Internal linking: header shows only "Leistungen & Preise", "Über uns", "Kontakt"; footer links Angebote, Shop, Ratgeber, Standorte, Galerie, Videos, Karriere, Partner and legal pages. Inlinks from the 65 crawled pages: hub pages 65 each; service pages 4-16; offer pages 3-5; Ratgeber articles and city pages only 2 each (hub plus one neighbour). Ratgeber articles are not linked from the matching service/offer pages, and offer pages are not linked from Ratgeber; /category/all-products has 0 inlinks. Visible breadcrumbs exist on detail pages — crawl data, e.g. [Ratgeber article](https://www.ozperformance.de/ratgeber/getriebe-notlauf-was-tun)
- Search Console: the HTML carries a google-site-verification meta tag with the comment "Google Search Console ownership (Site Verification API, META method)", but Wix's own Search Console integration reports status NOT_CONNECTED and no setup events (no sitemap submission through Wix) — [homepage source](https://www.ozperformance.de/); Wix GSC API read on 25 Nov 2026, no public URL
- No analytics tag (GA4/GTM/Meta pixel) was found in the server HTML; the cookie banner mentions "Statistik" loaded after consent — [homepage source](https://www.ozperformance.de/)

### Inferences
- AI crawlers face no technical barrier; the limiting factors are discoverability (sitemap, 404s) and content depth, not access.
- Loading Google Fonts from Google without consent is a known German data-protection risk (LG München I, 2022) and contradicts the site's own consent promise; self-hosting also removes a render-blocking third-party request.
- Core Web Vitals are probably good given the light page weight, but this is unmeasured.

### Gaps
- Plain http:// could not be tested (sandbox proxy only tunnels HTTPS); the http to https redirect is assumed from HSTS and Wix defaults.
- No Lighthouse/PageSpeed/CrUX measurement and no real-device mobile test were run.
- Bing Webmaster Tools / IndexNow status unknown.

## 4. Structured data

### Takeaway
Structured data is broad and valid JSON (AutoRepair site-wide; Service with Offer prices, BreadcrumbList, FAQPage, Article, Product on the relevant templates). Missing or weak: richer organisation facts (legalName, founder, logo, hasMap, credentials), author Person, review/rating data, VideoObject, JobPosting, complete areaServed coverage and a WebSite node on inner pages.

### Cited Findings
- Site-wide on all 65 HTML pages: `AutoRepair` with @id https://www.ozperformance.de/#business, name "OZ Performance GmbH", telephone "+49 234 54453755", email, PostalAddress (Coloniastraße 21, 44892 Bochum, DE), geo 51.4776333 / 7.2981356, priceRange "€€", areaServed 8 cities (Bochum, Herne, Gelsenkirchen, Witten, Hattingen, Castrop-Rauxel, Dortmund, Essen), openingHoursSpecification Mo-Fr 09:00-18:00 and Sa 09:00-13:00, sameAs Instagram (oz.performance), TikTok (@ozperformance), YouTube (@ozperformance18) — [homepage source](https://www.ozperformance.de/)
- Homepage additionally: `WebSite` (name "OZ Performance", url; no SearchAction) and `FAQPage` with 6 questions. The crawler also flagged a LocalBusiness-typed node on the homepage only — [homepage source](https://www.ozperformance.de/)
- Service pages: `Service` (name, serviceType, description, image, provider referencing #business, areaServed) with `offers` arrays of concrete Offer items, e.g. "DQ381 / DQ500 Getriebesteuergerät Reparatur (P1735, P1736)" price 400 EUR; plus BreadcrumbList and FAQPage (13 questions on Mechatronik). ZF Service Point and Performance-Upgrades pages have no FAQPage — [/leistungen/mechatronik-reparatur](https://www.ozperformance.de/leistungen/mechatronik-reparatur)
- Offer and city pages: Service + BreadcrumbList + FAQPage (3 and 2 questions) — [/standorte/essen](https://www.ozperformance.de/standorte/essen)
- Ratgeber: `Article` with headline, description, image (same generic image on every article), datePublished = dateModified = 2026-10-28, author and publisher both pointing to the AutoRepair @id (organisation as author, no Person) — [Ratgeber article](https://www.ozperformance.de/ratgeber/getriebe-notlauf-was-tun)
- Products: `Product` schema from Wix Stores with an Organization node — [product page](https://www.ozperformance.de/products/dq200-0am-mechatronik-schieberkasten-neuteil)
- Not present anywhere: aggregateRating, Review, Person, legalName, vatID, founder, logo, hasMap, hasCredential/award/memberOf, hasOfferCatalog, VideoObject, ImageObject, JobPosting, SearchAction (string search across all crawled HTML) — [homepage source](https://www.ozperformance.de/)
- The on-page rating "4,9 ★ 285 Google-Bewertungen" and the quoted Google reviews are plain text only; sameAs does not include the Google Business Profile, although the page links to Google Maps place_id ChIJKePmCCcfuUcRGWqPSqxPHMw — [homepage](https://www.ozperformance.de/)
- Google stopped showing FAQ rich results on 7 May 2026 and is removing the report and Rich Results Test support; FAQPage remains valid schema.org markup — [Search Engine Land](https://searchengineland.com/google-to-no-longer-support-faq-rich-results-476957), [Search Engine Roundtable](https://www.seroundtable.com/google-drops-faq-rich-results-41298.html) (secondary sources; Google's own documentation page was not fetched)

### Inferences
- The FAQPage markup no longer earns Google rich results but still gives machine-readable Q&A to other parsers; its value is now in the visible Q&A text itself.
- Adding aggregateRating to the business's own LocalBusiness node would not be eligible for Google review stars (self-serving reviews rule), so the absence is not a defect for Google; identity facts (legalName, founder/Meister, credentials, GBP in sameAs, logo) are the more useful additions for entity understanding.
- The Mechatronik page's JSON-LD is the largest on the site; because JSON-LD is rendered by code, Wix's dashboard limit (7,000 characters per markup, 8,000 per page) does not apply here.

### Gaps
- Markup was parsed for JSON validity and types but not run through Google's Rich Results Test or the Schema.org validator.
- The exact source of the "LocalBusiness" type flagged on the homepage was not isolated.

## 5. Entity consistency (name, address, phone)

### Takeaway
On the live site the entity is fully consistent: "OZ Performance GmbH", Coloniastraße 21, 44892 Bochum, +49 234 54453755, with the mobile number used only for WhatsApp. The inconsistencies now live off-site: old indexed titles and directories ("OZ Performance UG ...", "OZ Performnce"), a second domain under a different brand, and differing opening hours.

### Cited Findings
- Impressum: "OZ Performance GmbH, Coloniastraße 21, 44892 Bochum", Geschäftsführer Cevat Özcan, Telefon +49 234 54453755, Mobil/WhatsApp +49 176 45858800, info@ozperformance.de, Amtsgericht Bochum HRB 21451, USt-ID DE367746529, Berufsbezeichnung Kraftfahrzeugtechniker-Handwerk, Handwerkskammer Dortmund — [Impressum](https://www.ozperformance.de/impressum)
- Across all crawled HTML: "OZ Performance GmbH" 243 occurrences, "OZ Performance UG" 0, "Getriebe & Motortechnik" 0, "Software & Getriebetechnik" 0; "OZ-Performance" (hyphenated) 2; "KFZ-Meisterbetrieb" 73. Title-tag brand suffix is the short form "OZ Performance" — crawl data, e.g. [footer on homepage](https://www.ozperformance.de/)
- Phone: every tel: link is +4923454453755; every WhatsApp link is wa.me/4917645858800; the mobile number is printed only in Impressum and Datenschutz. National notation (0234 ...) is not used on the site — [Kontakt](https://www.ozperformance.de/kontakt)
- Opening hours on site (footer, Kontakt, JSON-LD): Mo-Fr 9:00-18:00, Sa 9:00-13:00, Sunday and public holidays closed — [Kontakt](https://www.ozperformance.de/kontakt)
- Descriptor variants on site: "ZF Service Point / Getriebe- und Softwaretechnik / Bochum" (hero), "Spezialist für Getriebe- und Softwaretechnik und ZF Service Point in Bochum" (footer), "Getriebe-Spezialist", "KFZ-Meisterbetrieb & ZF Service Point" (city pages), "Zertifizierter ZF-Partner", "ZF [pro]Tech Partner" (photo caption) — [homepage](https://www.ozperformance.de/), [/ueber-uns](https://www.ozperformance.de/ueber-uns)
- Off-site variants found in search results: old page titles "OZ Performnce - Software & Getriebetechnik" (typo) and "OZ Performance UG Getriebe & Motortechnik - Preise"; a directory stating the Impressum name "OZ Performance UG Software & Getriebetechnik"; "OZ Performance GmbH - KFZ Meisterbetrieb" on Cylex, ProvenExpert, ReviewHero; hours quoted as "Montag - Freitag 10:00 - 18:00, Einen Samstag im Monat nach Vereinbarung" and "Samstag: nach Vereinbarung" — [motorzentrale.de](https://www.motorzentrale.de/anbieter/oz-performance-101152), [reviewhero.io](https://www.reviewhero.io/oz-performance-gmbh-kfz-meisterbetrieb-coloniastrasse-21-bochum-b3a2), [cylex](https://web2.cylex.de/firma-home/oz-performance-gmbh---kfz-meisterbetrieb-13857858.html), [provenexpert](https://www.provenexpert.com/de-de/oz-performance-gmbh-kfz-meisterbetrieb/)
- getriebespuelung-bochum.de uses the same address and both phone numbers under the name "Getriebespülung Bochum", email info@getriebespuelung-bochum.de, "Sa nach Vereinbarung" — [getriebespuelung-bochum.de](https://getriebespuelung-bochum.de/)
- Review counts differ by source: site says 4,9 with 285 Google reviews; ReviewHero shows 4.94 from 204; another aggregator 4,90 from 244 — [homepage](https://www.ozperformance.de/), [reviewhero.io](https://www.reviewhero.io/oz-performance-gmbh-kfz-meisterbetrieb-coloniastrasse-21-bochum-b3a2)

### Inferences
- The UG to GmbH change is complete on the site; cleanup work is in directories, old index entries and the second domain, where Saturday hours and brand name contradict the main site.
- The review figure "285" is hard-coded text and will drift from the real Google count.

### Gaps
- Google Business Profile name, hours and phone were not checked here (out of scope for the site crawl).
- The Impressum of getriebespuelung-bochum.de was not extracted, so the legal name stated there is unverified.

## 6. Trust / E-E-A-T signals on the site

### Takeaway
Strong on prices, real quoted Google reviews, photos, opening hours and legal identity; weak on people and proof: no named Meister, no team, no ZF certificate or other verifiable credentials, no case studies, vague warranty statement, anonymous Ratgeber.

### Cited Findings
- Prices: "ab" prices on every service card (Getriebe-Instandsetzung ab 1.500 €, DSG and Mechatronik ab 250 €, Spülung and ZF ab 300 €, Diagnose/Software/Performance ab 150 €, Meister-Wartung ab 1.899 €), detailed fixed-price tables incl. 19 % VAT on service pages, price calculator at /termin; "€" on 38 pages — [homepage](https://www.ozperformance.de/), [/leistungen/mechatronik-reparatur](https://www.ozperformance.de/leistungen/mechatronik-reparatur)
- Reviews: "4,9 ★ 285 Google-Bewertungen" with link to the Google Maps listing and verbatim quotes with first name, month and source (e.g. Klaus W., April 2026, VW Tiguan, P1736, same-day repair) on 28 pages — [homepage](https://www.ozperformance.de/)
- Free first diagnosis and "Gläserne Werkstatt" (view from waiting room, old oil shown, digital service entry) are stated — [homepage](https://www.ozperformance.de/)
- Warranty: FAQ answer "Ja, auf unsere Reparaturen geben wir Garantie. Die genauen Bedingungen finden Sie in unserem Angebot." No duration or scope on service pages; "Garantie" occurs on only 3 pages — [homepage FAQ](https://www.ozperformance.de/)
- Meister: "KFZ-Meisterbetrieb" is asserted 73 times, but no Meister is named and no Meisterbrief is shown; the only person named anywhere is Geschäftsführer Cevat Özcan in the legal pages — [Impressum](https://www.ozperformance.de/impressum), [/ueber-uns](https://www.ozperformance.de/ueber-uns)
- ZF Service Point: claimed on 35 pages ("zertifizierter ZF Service Point", "Original-ZF-Teile"); no certificate image with readable ID, no partner number, no link to ZF's partner search; gallery caption "ZF [pro]Tech Partner" — [/leistungen/zf-service-point](https://www.ozperformance.de/leistungen/zf-service-point)
- Team/about: /ueber-uns has 289 words, no founding year, no team names or portraits, captions "Unser Werkstatthund", "Die Werkstatthalle", "Das Büro" — [/ueber-uns](https://www.ozperformance.de/ueber-uns)
- Photos/videos: 28 gallery images, video page with one featured video (Getriebespülung BMW 545i); social links to Instagram, TikTok, YouTube — [/galerie](https://www.ozperformance.de/galerie), [/videos](https://www.ozperformance.de/videos)
- Case studies: none as own pages; the review quotes are the only case-like evidence — [/ratgeber](https://www.ozperformance.de/ratgeber)
- Opening hours and NAP on every page footer and in JSON-LD; Kontakt page with form, map (on consent) and route link — [Kontakt](https://www.ozperformance.de/kontakt)
- Legal completeness: Impressum with HRB, VAT ID, chamber; Datenschutz (1,181 words), AGB (2,701 words), Widerruf — [Impressum](https://www.ozperformance.de/impressum)
- Some offer pages link out to a Kleinanzeigen listing ("Zum Kleinanzeigen-Inserat") as a primary button — [offer page](https://www.ozperformance.de/angebote/dq381-dq500-drucksensor-reparatur)
- Odd signals: "Meister-Wartung ab 1.899 €" for a page titled "KFZ-Wartung & Inspektion" (the price belongs to BMW timing chains); AGB contains house rules for DPF removal while offer pages advertise "DPF/AGR Sorglospaket" and "AdBlue Reparatur / Software" — [/leistungen/meister-wartung](https://www.ozperformance.de/leistungen/meister-wartung), [/angebote/dpf-agr-sorglospaket](https://www.ozperformance.de/angebote/dpf-agr-sorglospaket)

### Inferences
- For Google and for AI assistants, the experience evidence is carried almost entirely by third-party reviews; first-party expertise signals (who diagnoses, qualifications, documented repairs with photos and measured values) are the largest E-E-A-T gap.
- DPF/AGR/AdBlue "software solutions" are legally sensitive in Germany and could affect how cautious assistants are about recommending the business; wording should be reviewed by the owner.

### Gaps
- Whether the business is listed in ZF Aftermarket's official partner locator was not checked here.
- Image content (e.g. a certificate visible in a gallery photo) was not visually inspected.

## 7. Indexation and current visibility

### Takeaway
Could not be measured reliably. Evidence available: search engines still list pre-relaunch URLs that now 404 alongside at least the new homepage and one Ratgeber article, and Search Console is not connected through Wix. Exact indexed-page counts and ranking queries remain unknown.

### Cited Findings
- A web search on 25 Nov 2026 returned these ozperformance.de URLs: www.ozperformance.de/ ("OZ Performance Bochum"), www.ozperformance.de/ratgeber/was-ist-dsg-doppelkupplungsgetriebe, and the old URLs ozperformance.de/getriebeinstandsetzung/, ozperformance.de/leistungen/getriebeinstandsetzung, ozperformance.de/preise — search result listing; live checks: [/getriebeinstandsetzung](https://www.ozperformance.de/getriebeinstandsetzung) 404, [Ratgeber article](https://www.ozperformance.de/ratgeber/was-ist-dsg-doppelkupplungsgetriebe) 200
- For "P1735 P1736 DQ381 Drucksensor Reparatur Bochum" no ozperformance.de page appeared among 16 results (eBay, absstuurapparaten.nl, kfz-dietrich.com instead) — [absstuurapparaten.nl](https://absstuurapparaten.nl/en/pages/solution-dq381-dq500-dsg-7-error-codes-p173500-and-p173600)
- Wix Search Console integration: connection NOT_CONNECTED, readiness NOT_READY, no events, sitemaps and search analytics unavailable ("no Google account is connected for this site") — Wix GSC API read, 25 Nov 2026, no public URL; API described in [Wix GSC recipe](https://dev.wix.com/docs/api-reference/business-management/seo/google-search-console/skills/manage-google-search-console-for-a-wix-site)
- Third-party pages that currently represent the business in search: ReviewHero, Cylex, ProvenExpert, motorzentrale.de, carfield-thum.de, YouTube channel "Oz Performance GmbH", Kleinanzeigen — [reviewhero.io](https://www.reviewhero.io/oz-performance-gmbh-kfz-meisterbetrieb-coloniastrasse-21-bochum-b3a2), [provenexpert](https://www.provenexpert.com/de-de/oz-performance-gmbh-kfz-meisterbetrieb/), [YouTube](https://www.youtube.com/@ozperformance18)

### Inferences
- The site is five weeks old in its current form; Google has started picking up new URLs but still serves old ones that 404. Without redirects those entries will drop out and their equity is lost.
- Because the Ratgeber and offer pages are not in the sitemap and Search Console is not wired up in Wix, there is currently no monitoring of which of the 62 indexable pages are indexed.

### Gaps
- `site:ozperformance.de` could not be evaluated: the search tool returned no domain-restricted results, Bing served unrelated US results to the sandbox, DuckDuckGo returned a bot challenge. Indexed-page counts for Google and Bing are therefore unknown.
- No ranking positions, impressions or click data. Needs Search Console (property appears to be verified via meta tag by some Google account) and Bing Webmaster Tools.
- Visibility inside ChatGPT, Perplexity, Gemini, Claude and AI Overviews was not tested in this part of the research.

## 8. Wix capabilities and limits relevant to this site

### Takeaway
Because the site is a Wix-managed headless Astro project, most classic Wix editor limits do not apply: pages, JSON-LD and templates are code, so scaling to hundreds of fault-code pages is a development task, while robots.txt, llms.txt, redirects and SEO defaults remain dashboard tools. The trade-off is that content changes need a developer/AI deploy, and Wix auto-SEO only covers routes that are properly registered.

### Cited Findings
- Wix-managed headless with the Astro integration: Wix hosts on its CDN and "generates SEO tags from the settings a Wix user edits in the dashboard" (titles, meta descriptions, canonicals, social tags, robots directives, structured data); main pages get tags injected automatically, item pages need code — [Wix: About SEO Support](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/feature-guides/seo/about-seo-support), [Manage SEO for Main Pages](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/feature-guides/seo/manage-seo-for-main-pages)
- Sitemap: Wix generates /sitemap.xml as an index; pages-sitemap.xml comes from the page registry at /_wix/pages.json and covers main pages plus item routes registered with wixMetadata; each installed business solution gets its own sitemap — [About Sitemaps in the Astro Integration](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/feature-guides/seo/about-sitemaps-in-the-astro-integration)
- Item pages (parameterised routes) need two steps: register the route and render Wix-resolved tags at request time — [Add SEO Support to Item Pages](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/feature-guides/seo/add-seo-support-to-item-pages)
- robots.txt: editable in SEO & GEO > Tools and settings > Robots.txt Editor; Wix documents blocking AI crawlers (GPTBot, CCBot, ChatGPT-User) there, so the same editor can state explicit Allow rules — [Editing Your Site's Robots.txt File](https://support.wix.com/en/article/editing-your-sites-robotstxt-file), [Blocking AI Crawlers from Your Site](https://support.wix.com/en/article/blocking-ai-crawlers-from-your-site)
- llms.txt: generated for all sites with a premium plan, custom domain and indexing enabled; can be viewed, edited (auto-updates then stop) or switched off in the dashboard — [Understanding Your Site's llms.txt File](https://support.wix.com/en/article/understanding-your-sites-llms-txt-file), [feature release note](https://support.wix.com/en/article/seo-request-making-llms-txt-available-for-all-sites)
- Redirects: URL Redirect Manager supports single and group 301 redirects, CSV import of up to 500 per file, maximum 5,000 redirects per site, custom domains only; Wix recommends redirects when old-site URLs cannot be matched — [Setting Up a 301 Redirect](https://support.wix.com/en/article/setting-up-a-301-redirect-for-a-page-on-your-site), [Importing or Exporting URL Redirects](https://support.wix.com/en/article/importing-or-exporting-url-redirects-with-a-csv-file), [multilingual redirects (5,000 limit)](https://support.wix.com/en/article/setting-up-a-301-redirect-for-a-multilingual-site). The live site already has two working redirects (/preise, /preisrechner), so the mechanism works on this project — [/preise](https://www.ozperformance.de/preise)
- Structured data in the Wix dashboard is JSON-LD only, under 7,000 characters per markup and 8,000 per page; AI-generated markup exists only for Wix Blog posts — [Troubleshooting Your Structured Data Markup](https://support.wix.com/en/article/troubleshooting-your-structured-data-markup), [Adding Structured Data Markup](https://support.wix.com/en/article/adding-structured-data-markup-to-your-sites-pages-2546962). On this site JSON-LD is emitted by the Astro templates (observed: multiple script blocks per page) — [service page source](https://www.ozperformance.de/leistungen/mechatronik-reparatur)
- Blog: Wix Blog is not installed; the Ratgeber is a coded route /ratgeber/[slug]. An Astro blog template for Wix Blog exists if dashboard-editable posts are wanted — Wix site context; [Astro templates](https://dev.wix.com/docs/go-headless/wix-managed-headless/full-integration-astro/get-started/astro-templates-for-wix-managed-headless)
- Search Console: Wix offers a GSC integration (connect account, verify, submit sitemap, request indexing, read search analytics, inspect URLs with 2,000 inspections per property per day) — [Wix GSC recipe](https://dev.wix.com/docs/api-reference/business-management/seo/google-search-console/skills/manage-google-search-console-for-a-wix-site)
- Dashboard content edits (products, bookings, CMS items) appear on the live headless site without a new release; layout/template changes need a release — [Develop Your Project](https://dev.wix.com/docs/go-headless/wix-managed-headless/develop-your-project)
- Wix exposes an MCP endpoint for AI agents on the site (/_api/mcp, advertised in llms.txt) with tools for business details, site search, bookings and purchases — [llms.txt](https://www.ozperformance.de/llms.txt)

### Inferences
- Fault-code pages at scale are feasible with the existing pattern: one more dynamic route (e.g. /fehlercodes/[slug]) fed from a data file or a Wix CMS collection, with Article/FAQ markup from the template. The prerequisite is fixing route registration so such pages enter the sitemap.
- The llms.txt should be hand-edited to carry real business facts and key URLs; today it is effectively empty for an LLM.
- The source code of the Astro project is the single point of control; whoever built it (the comment style suggests an AI-assisted build) must be available for every structural SEO change.

### Gaps
- Whether the Ratgeber/offer content lives in code files or in a Wix CMS collection could not be determined (project source is not accessible; Wix reported no retrievable static files for this release).
- Wix plan tier and any page/CMS item limits of that plan were not checked.
- Whether dashboard SEO settings (SEO & GEO > SEO Settings) override the coded titles on this project was not tested, because that would require a write.
