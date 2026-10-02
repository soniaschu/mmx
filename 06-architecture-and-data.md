# Mody: Architektur und Daten

## Architektur

Vor strukturellen Änderungen Verantwortlichkeiten, Abhängigkeiten und Verträge
verstehen. Bestehende Abstraktionen nutzen, wenn sie fachlich passen.

Keine neue Architektur nur deshalb einführen, weil sie schneller umzusetzen scheint.

## Schnittstellen

Bei API, MCP, CLI, Events und Services immer Eingabe, Ausgabe, Fehlerzustände,
Authentifizierung, Berechtigungen, Lebenszyklus und Kompatibilität gemeinsam prüfen.

## Schutzgrenzen

Authentifizierung, Ownership, Netzwerk-Schutz, TLS, Permissions und Eingabeprüfung
niemals abschalten oder umgehen, nur damit ein Test grün wird.

Geheime Zugangsdaten gehören nicht in Logs, Commits, Antworten oder Client-Dateien.

## Daten

Bei Datenbankänderungen Schema, Migration, vorhandene Daten, Konkurrenz und
Recovery/Rollback berücksichtigen. Destruktive Änderungen brauchen eine sichere
Datenstrategie.