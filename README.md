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

## Widget auf dem Android-Homescreen

Voreingestellt ist die Strecke **Stuttgart Feuersee → Stuttgart-Weilimdorf** (S6/S60, direkt).
Eine Webseite kann unter Android selbst kein Widget anlegen; man braucht eine Widget-App,
die eine Webseite als Widget anzeigt. Damit erscheinen die Infos direkt auf dem Homescreen.

**Widget-URL** (nach dem Einrichten von GitHub Pages `<user>`/`<repo>` ersetzen):

```
https://<user>.github.io/<repo>/?from=Stuttgart%20Feuersee&to=Stuttgart-Weilimdorf&widget=mini&theme=dark
```

1. Eine App installieren, die Webseiten als Widget darstellen kann
   (im Play Store nach „Website Widget“ oder „Web Widget“ suchen).
2. Auf dem Homescreen lange tippen → *Widgets* → Widget der App hinzufügen
   (Größe etwa 4×1 oder 4×2).
3. Die Widget-URL oben eintragen, Aktualisierungsintervall so kurz wie möglich (z. B. 5–15 min).
   Tippen auf das Widget lädt die Daten sofort neu.

Varianten der Widget-URL:

- `widget=mini`: eine Zeile pro Verbindung (Linie, Abfahrt, Verspätung, Minuten), passt in 4×1/4×2
- `widget=1`: ausführliche Ansicht mit Gleis, Ankunft und Störungsmeldungen (ab 4×3)
- `theme=dark` / `theme=light`: Farben fest vorgeben; `bg=transparent`: ohne Hintergrund
- Gegenrichtung: `from` und `to` tauschen

Stationen können per Name (`from=Stuttgart%20Feuersee`) oder per ID angegeben werden;
Namen werden beim ersten Aufruf über die Stationssuche aufgelöst und gespeichert.

**Als App-Icon (Alternative):** Im Browser-Menü „Zum Startbildschirm hinzufügen“.
Dann öffnet sich die Seite per Tippen im Vollbild, zeigt aber nichts direkt auf dem Homescreen an.

### URL-Parameter

| Parameter | Bedeutung |
|---|---|
| `from`, `to` | Stations-ID (IBNR/EVA) oder Stationsname |
| `fromName`, `toName` | Anzeigenamen |
| `n` | Anzahl Verbindungen (1–6, Standard 2) |
| `offset` | Vorlaufzeit in Minuten |
| `sbahn=0` | auch andere Verkehrsmittel zulassen |
| `direct=0` | auch Verbindungen mit Umstieg |
| `widget=1` / `widget=mini` | Widget-Ansicht ohne Bedienelemente (ausführlich / eine Zeile pro Verbindung) |
| `theme` | `dark` oder `light` |
| `bg=transparent` | ohne Hintergrund |
| `api` | alternative API-Basis-URL |
