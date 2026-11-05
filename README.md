# S-Bahn Anzeige

Eine einfache Web-App (reines HTML/JS, keine Android-App nötig), die für eine gewählte
S-Bahn-Strecke die nächsten Verbindungen mit Echtzeitdaten der Deutschen Bahn anzeigt
(Abfahrt, Verspätung, Gleis, Ankunft, Ausfälle, Störungsmeldungen, Countdown).

## Datenquelle

Die App nutzt die öffentliche, kostenlose API [`v6.db.transport.rest`](https://v6.db.transport.rest/)
(Daten der Deutschen Bahn, kein API-Key, CORS-fähig, daher direkt aus dem Browser nutzbar).
Unter *Erweitert* kann eine andere Instanz von [db-rest](https://github.com/derhuerst/db-rest)
eingetragen werden, falls die öffentliche ausfällt.

## Benutzung

1. `index.html` über HTTPS bereitstellen, z. B. per **GitHub Pages**
   (Repo → Settings → Pages → Branch auswählen → Ordner `/ (root)`).
2. Seite auf dem Handy öffnen, **Start** und **Ziel** suchen und aus der Liste auswählen.
   Optionen: nur S-Bahn, nur Direktverbindungen, Anzahl (Standard 2), Vorlaufzeit (Fußweg).
3. Mehrere Strecken können gespeichert werden (Buttons oben), `⇅` tauscht die Richtung.
   Die Daten aktualisieren sich jede Minute automatisch.

## Auf den Startbildschirm

- **Als App-Icon:** Im Browser-Menü „Zum Startbildschirm hinzufügen“ (Chrome/Safari).
  Die Seite öffnet sich dann im Vollbild wie eine App.
- **Als echtes Widget (Android):** Mit dem 🔗-Button einen Widget-Link kopieren und in einer
  Web-Widget-App (z. B. KWGT mit Web-Komponente oder einer „Website Widget“-App) einfügen.
  Der Link enthält die komplette Verbindung, z. B.:

  ```
  https://<user>.github.io/<repo>/?from=8000096&fromName=Stuttgart%20Hbf&to=8005768&toName=Flughafen%2FMesse&n=2&widget=1
  ```

### URL-Parameter

| Parameter | Bedeutung |
|---|---|
| `from`, `to` | Stations-IDs (IBNR/EVA) |
| `fromName`, `toName` | Anzeigenamen |
| `n` | Anzahl Verbindungen (1–6, Standard 2) |
| `offset` | Vorlaufzeit in Minuten |
| `sbahn=0` | auch andere Verkehrsmittel zulassen |
| `direct=0` | auch Verbindungen mit Umstieg |
| `widget=1` | kompakte Ansicht ohne Bedienelemente |
| `api` | alternative API-Basis-URL |
