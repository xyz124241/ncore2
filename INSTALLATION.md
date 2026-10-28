# NeptunCore – Build und Installation

## GitHub einrichten

1. Lade den gesamten Projektordner in dein GitHub-Repository hoch. Achte darauf, dass `.github/workflows/build.yml` enthalten ist.
2. Committe und pushe die Änderungen auf den Branch, den du bauen möchtest.
3. Öffne **Actions → Build NeptunCore** und kontrolliere den neuesten Lauf. Der Workflow baut mit Java 21 und `mvn --batch-mode --no-transfer-progress --errors clean verify`.
4. Bei grünem Lauf lade unter **Artifacts** das Artifact `NeptunCore` herunter. Es enthält nur die einzelne Plugin-JAR.

## Auf dem Server installieren

1. Erstelle ein Backup.
2. Stoppe den Paper-Server vollständig.
3. Sichere die alte NeptunCore-JAR und den zugehörigen Datenordner.
4. Lege die heruntergeladene `NeptunCore-1.0.0.jar` in `plugins/`.
5. Starte den Server neu und prüfe die Konsole.

Installiere keine zweite Kopie von NeptunCore. Optionale Abhängigkeiten wie Vault, PlayerPoints oder LuckPerms bleiben separate Plugins, wenn die entsprechenden Funktionen sie benötigen.

## Lokal bauen

Mit JDK 21 und Maven 3.9+ im Projektordner:

```bash
mvn --batch-mode --no-transfer-progress --errors clean verify
```

Ausgabe: `target/NeptunCore-1.0.0.jar`.

## Wenn GitHub Actions fehlschlägt

Öffne den fehlgeschlagenen Schritt **Build the single NeptunCore plugin** und lies die ersten `ERROR`-Zeilen. Wenn dort wieder `runTask is ambiguous` steht, ist wahrscheinlich nicht die aktuelle Version des Quellcodes gebaut worden. Prüfe, ob `Engine.java`, `BrowserGui.java` und `SellGui.java` jeweils `(Runnable) p::closeInventory` enthalten, und committe/pushe diese Dateien erneut.
