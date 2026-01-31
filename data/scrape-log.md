# WG-Finder Scrape Log

**Datum:** 2026-01-31T13:01 UTC

## Ergebnisse nach Quelle

### ✅ WG-Gesucht (wg-gesucht.de)
- **Status:** Erfolgreich via Browser (openclaw profile)
- **Methode:** `web_fetch` lieferte nur generischen SEO-Text (Listings sind JS-gerendert), daher Fallback auf headless Browser
- **Cookie-Banner:** Musste akzeptiert werden (automatisch via Browser-Snapshot gelesen)
- **Ergebnis:** **19 echte Angebote** extrahiert (von 934 Gesamtangeboten auf der Plattform)
- **Anmerkungen:**
  - Leverkusen-Angebot übersprungen (nicht Köln)
  - Einige Duplikate (z.B. zwei Luis-Anzeigen für gleiche Adresse) bereinigt
  - Preis bei WG-Gesucht ist typischerweise Warmmiete
  - Paginierung nicht gescraped (nur erste Seite)

### ❌ ImmoScout24 (immobilienscout24.de)
- **Status:** Gescheitert — CAPTCHA-Sperre
- **Methode:** Sowohl `web_fetch` (HTTP 401) als auch Browser (visuelles CAPTCHA "Die Uhren auswählen") blockiert
- **Ergebnis:** 0 Angebote
- **Anmerkungen:**
  - ImmoScout hat aggressive Bot-Erkennung
  - CAPTCHA ist ein Bilder-Rätsel ("Uhren auswählen"), das programmatisch nicht lösbar ist
  - Würde manuellen Browser-Zugang oder API-Key erfordern

### ✅ Kleinanzeigen (kleinanzeigen.de)
- **Status:** Erfolgreich via `web_fetch`
- **Methode:** Direkter HTTP-Fetch, kein Bot-Block
- **Ergebnis:** **18 echte Angebote** extrahiert
- **Anmerkungen:**
  - Einige Anzeigen sind Zwischenmieten/Untermieten (trotzdem WG-relevant)
  - Monteurzimmer-Anzeige übersprungen (kein WG-Zimmer)
  - Klettenberg-Zwischenmiete (1.600€ ganze Wohnung) übersprungen
  - Zimmergröße nicht immer separat angegeben (Gesamtfläche vs. Zimmergröße)
  - Manche Einträge haben kein explizites Verfügbar-ab-Datum

## Zusammenfassung

| Portal | Methode | Status | Angebote |
|--------|---------|--------|----------|
| WG-Gesucht | Browser | ✅ Erfolg | 19 |
| ImmoScout24 | Browser | ❌ CAPTCHA | 0 |
| Kleinanzeigen | web_fetch | ✅ Erfolg | 18 |
| **Gesamt** | | | **37** |

## Datenqualität

- **Preisspanne:** 231€ – 985€ (Median ca. 600€)
- **Zimmergröße:** 9–25 m² (wo angegeben)
- **Stadtteile:** 20+ verschiedene Kölner Stadtteile abgedeckt
- **Verfügbarkeit:** Meist ab Feb/März 2026, einige sofort
- **Fehlende Daten:** Einige Kleinanzeigen ohne explizite Zimmergröße oder Verfügbar-ab-Datum (als `null` gespeichert)

## Nächste Schritte (Vorschläge)

- ImmoScout24 könnte über deren offizielle API oder mit einem echten Browser-Profil (mit Cookies) funktionieren
- Für mehr Angebote: Paginierung auf WG-Gesucht und Kleinanzeigen implementieren
- Regelmäßiges Scraping einrichten (z.B. alle 6 Stunden), um neue Angebote schnell zu finden
