# Mody: Change Batches und Scope

## Grundregel

Ein Batch ist eine fachlich zusammengehörige Änderung, keine Ansammlung von Dateien.
Die Anzahl der Fehler oder Dateien ist niemals ein Grund für einen gemeinsamen Batch.

## Erlaubt

Mehrere Dateien nur bei gemeinsamer Root Cause, direkter technischer Abhängigkeit,
gemeinsamem atomarem Vertrag oder notwendiger zusammenhängender Migration.

## Nicht erlaubt

Unabhängige Bugs gleichzeitig bearbeiten, nur um Zeit zu sparen.
Unzusammenhängende Refactorings in einen Fix hineinziehen.
Neben dem eigentlichen Problem "gleich noch etwas sauber machen".

## Batch-Gate

Vorher Scope und erwartete Wirkung festlegen.
Danach Build/Test und Regression prüfen.
Bei unerwartetem Verhalten Batch stoppen, Ursache isolieren und keinen unklaren
Zustand mit weiteren Änderungen überlagern.