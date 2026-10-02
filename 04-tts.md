# Bob TTS — Pflichtverhalten

Diese Regel definiert ausschließlich das TTS-Verhalten. Sie entfernt keine anderen Bob-Funktionen, ersetzt keine vorhandenen Tools und erzeugt keine Mock- oder Dummy-Implementierung.

## Automatisches Sprechen
- Der Stop-Hook /home/bkg/.bob/hooks/auto-speak.mjs ist die autoritative automatische TTS-Pipeline.
- Nach jeder normalen Bob-Antwort wird der echte Antworttext an den TTS-Backend-Endpunkt gesendet.
- Transport: direkter HTTP-Aufruf an https://mcp.eysho.info/mcp mit serverseitigem TTS-Secret. Keine Browser-API und kein Frontend-Key.
- Stimme: nvidia:DE-DE.Mia, Sprache de-DE.
- TTS ist standardmäßig aktiv, solange /tmp/bob-speaks-off nicht existiert.
- /bob-speaks sowie sprich, vorlesen und tts an entfernen /tmp/bob-speaks-off.
- tts aus, stumm und stop speaking setzen /tmp/bob-speaks-off.

## Was gesprochen wird
Grundregel: Alles aus der sichtbaren Antwort wird gesprochen, außer echtem Code.

Nicht gesprochen werden:
- fenced Codeblöcke
- Inline-Code und Shell-Kommandos
- JSON-, YAML-, TOML- und ähnliche reine Konfigurationsblöcke
- rohe maschinenlesbare Payloads, Stacktraces und Binärdaten

Normaler Fließtext, Überschriften, Listen, Fehlermeldungen in menschlicher Sprache, Statusmeldungen und Erklärungen werden gesprochen. Markdown-Formatierung wird vor dem TTS entfernt, der Inhalt bleibt erhalten. URLs werden nicht als lange Zeichenketten vorgelesen, sondern als Link.

## Länge
- Bis zu 2000 Zeichen echter Prosa pro Antwort.
- Audio darf bis zu 3 Minuten dauern.
- Keine künstliche 500- oder 1500-Zeichen-Grenze.
- Bei längeren Antworten wird an Satzgrenzen in mehrere TTS-Aufrufe geteilt.

## Fehlerverhalten
- Kein stilles Vortäuschen von Erfolg.
- Wenn TTS fehlschlägt, bleibt die sichtbare Antwort vollständig erhalten.
- Kein Workaround, kein Mock, kein NOOP und kein Entfernen von Features, um einen TTS-Fehler zu verstecken.
- Die Ursache wird im Hook-Log mit HTTP-Status bzw. Backend-Fehler dokumentiert.
- Bei einem echten NVIDIA-Riva-Fehler darf die vorhandene lokale Fallback-Kette greifen. Es wird keine erfundene Stimme verwendet.

## Konfiguration
Die Bob-spezifische TTS-Konfiguration liegt in /home/bkg/.bob/tools/bob-tts.json. Die zentrale Voice-Konfiguration muss dieselbe reale NVIDIA-Stimme verwenden.

## Entwicklungsregel
TTS-Änderungen dürfen keine anderen Bob-Features entfernen oder abschalten. Bestehende Tools, Skills, Hooks und Regeln bleiben erhalten, sofern sie nicht selbst Ursache des konkreten TTS-Fehlers sind.