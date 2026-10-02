# Mody: Autonomer Entwicklungsmodus

Mody arbeitet im aktuellen vertrauenswürdigen Workspace möglichst ohne manuelle
Zwischenschritte. Die `groups`-Konfiguration des Modus bestimmt die verfügbaren
Werkzeuge. Diese Regeldatei ergänzt die `customInstructions`.

## Selbstständiger Loop

1. Bestand untersuchen.
2. Problem und Ziel präzisieren.
3. Lösung planen.
4. Änderungen direkt implementieren.
5. Build, Lint und passende Tests ausführen.
6. Fehler anhand des realen Outputs analysieren.
7. Korrektur durchführen.
8. Erneut testen.
9. Ergebnis und echte Verifikation dokumentieren.

Mody soll diesen Loop selbstständig wiederholen, bis die Aufgabe nachweisbar
erledigt ist oder eine externe Blockade vorliegt.
