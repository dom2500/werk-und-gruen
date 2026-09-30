# WERK & GRÜN – Hausmeisterservice

Vollständiges, responsives Portfolio-Demoprojekt. Formular im Demo-Modus.

## Vorschau
`index.html` im Browser öffnen. Alternativ die eigenständige Datei `WERK-und-GRUEN-Vorschau.html` verwenden. Keine Installation erforderlich. Formularzustand bleibt nur im Arbeitsspeicher und geht beim Neuladen verloren.

## Aufbau
- `index.html`: Seiteninhalte und Platzhalter für Unternehmens-/Rechtstexte.
- `style.css`: responsive Gestaltung, Fokuszustände, reduzierte Bewegung.
- `config.js`: Name, Region, Kontaktwerte, Bilder und optionaler Formular-Endpunkt.
- `app.js`: Formularschritte, Validierung, lokale Foto-Vorschau, Summary und Versandadapter.
- `assets/`: lokal gespeicherte, komprimierte Bilder.

## Für einen realen Betrieb
1. Firmenname, Rechtsform, Adresse, verantwortliche Person, Telefon und E-Mail ergänzen. `config.js` ändert Markenname und Kontaktdaten; Texte über Region/Leistungsumfang und Demo-Kennzeichnung in `index.html` redaktionell anpassen.
2. Leistungsangebot, tatsächliches Einsatzgebiet und Anfahrt klären. Keine Preis- oder Antwortzeitversprechen vorhanden.
3. Bildrechte für die konkrete Verwendung prüfen, optional eigene Fotos ersetzen. Bildnachweise in `BILDNACHWEISE.md`. Abgebildete Häuser sind keine realen Referenzen des Betriebs.
4. Impressum und Datenschutzhinweise anhand des tatsächlichen Unternehmens, Hostings und Dienstleisters vervollständigen. Demo-Texte sind keine fertigen Rechtstexte.
5. Versand und Dateiannahme serverseitig implementieren. Zugangsdaten ausschließlich in Server-Umgebungsvariablen/Secret Store.
6. Erst nach erfolgreicher Ende-zu-Ende-Prüfung `formEndpoint` aktivieren, die Demo-Texte durch echte Hinweise ersetzen und noindex bewusst überprüfen. Domain und Hosting verbinden. Veröffentlichung nur nach Freigabe.

## Vorbereiteter Backend-Vertrag
Der Adapter `submitInquiry` sendet nur bei konfiguriertem, gleichursprünglichem HTTPS-Endpunkt einen POST mit `multipart/form-data`:
- `inquiry`: JSON der Formularangaben und Fotometadaten.
- `photos`: je Bild ein File, maximal fünf, jeweils maximal 10 MiB.

Erwartete Bestätigung: JSON `{ "status": "accepted", "id": "<serverseitige Vorgangsnummer>" }` und erfolgreicher HTTP-Status. Diese Antwort darf der Server erst nach dauerhafter Annahme erzeugen. Sie bestätigt keinen E-Mail-Versand. Ohne Endpunkt wird ausschließlich der eindeutig gekennzeichnete Demo-Abschluss angezeigt.

Server-Pflichten: Alle Felder unabhängig validieren; maximal fünf Dateien und 10 MiB pro Datei sowie Gesamtkörper-Limit durchsetzen; MIME-Typ, Dateisignatur und dekodierbaren Bildinhalt prüfen; Pixel-/Ressourcenlimits; sichere zufällige Dateinamen; private Speicherung außerhalb öffentlicher Webpfade; Metadaten entfernen; Rate-Limits/Spam-Schutz; Origin/CSRF-Schutz passend zum Deployment; Ausgabe escapen; Uploads nicht ausführbar machen; definierte Löschfristen; minimale Logs ohne Formulardaten; Zustellfehler behandeln. Niemals rein clientseitiger Validierung vertrauen.

## Qualitätsprüfung
JavaScript-Syntax und strukturelle Prüfungen durchgeführt. Automatisierte DOM-Prüfungen werden im beigefügten Prüfbericht dokumentiert. Die überarbeitete Gestaltung wurde im Browser bei schmalen, mobilen, Tablet- und Desktop-Breiten geprüft. Der vollständige Demo-Formularablauf inklusive Fotoauswahl wurde im Browser durchlaufen. Vor Veröffentlichung bei 375, 768, 1024 und 1440 px sowie 200 % Zoom prüfen, einschließlich Tastatur, Dateiauswahl und Dialogfokus.

## Datenschutz der Demo
Keine externen Schriftarten, Bilder, Karten oder Analyseaufrufe. Keine Formulardaten in Local Storage oder Cookies. Fotos werden lokal über Object URLs angezeigt und nicht übertragen. Hosting kann technische Zugriffsdaten verarbeiten.


## GitHub Pages

Die öffentlichen Dateien liegen direkt im Hauptordner. Verwenden Sie für Pages Branch `main` und Ordner `/(root)`. Änderungen im Entwurfsbranch `design/werk-gruen-interface` werden erst nach Freigabe und Zusammenführung nach `main` veröffentlicht.
