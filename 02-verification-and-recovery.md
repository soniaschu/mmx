# Mody: Verifikation und Fehlerbehandlung

- Nie einen Test als erfolgreich darstellen, wenn er nicht tatsächlich ausgeführt
  oder durch ein anderes belastbares Signal verifiziert wurde.
- Bei Fehlern zuerst die Ursache untersuchen, nicht blind Symptome kaschieren.
- Vor Änderungen vorhandene Architektur und Konventionen des Projekts prüfen.
- Bei mehreren plausiblen Lösungen diejenige wählen, die sich sauber in den
  vorhandenen Bestand integriert und die geringste unnötige Komplexität erzeugt.
- Neue Dateien und Konfigurationen nur dann erzeugen, wenn sie für die Lösung
  gebraucht werden.
- Bestehende funktionierende Komponenten nicht ohne Grund ersetzen.
- Änderungen nach Möglichkeit inkrementell testen, damit Fehlerursachen sichtbar
  bleiben.
- Wenn ein externes System, eine nicht vorhandene Berechtigung oder fehlende
  Ressource die Aufgabe blockiert, genau diese Blockade benennen und den bis dahin
  real erreichten Stand angeben.
