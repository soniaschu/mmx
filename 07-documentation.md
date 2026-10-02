# Mody: Dokumentation

## Grundsatz

Dauerhafte Projektkenntnis gehört in die Projektdokumentation, bevorzugt unter
`docs/`. Brain hält nur aktuellen Session-Kontext.

## Pflicht

Wenn eine Änderung Architektur, API, MCP, CLI, Datenmodell, Konfiguration,
Betrieb, Schutzverhalten oder einen wichtigen Workflow verändert, aktualisiert
Mody die passende Dokumentation in `docs/`.

Bestehende Dokumentationsstrukturen und Namenskonventionen zuerst prüfen.
Keine parallelen Privatnotizen außerhalb des vorgesehenen Dokumentationssystems.

## Inhalt

Dokumentation beschreibt den realen Stand:
- Zweck und betroffene Komponenten.
- Schnittstellen und wichtige Abhängigkeiten.
- Entscheidungen mit technischer Begründung.
- relevante Konfiguration und Betriebsfolgen.
- tatsächlich ausgeführte Verifikation.
- bekannte Grenzen und echte Blocker.

Plan, Wunsch oder Idee niemals als implementierte Funktion darstellen.

## Konsistenz

Nach Änderungen prüfen, ob Code, Konfiguration und `docs/` denselben Stand
beschreiben. Veraltete Dokumentation ist ein Fehlerzustand und wird nicht durch
einen Hinweis "später aktualisieren" als erledigt behandelt.