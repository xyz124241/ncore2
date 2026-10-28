# NeptunCore

NeptunCore ist das einzelne Paper-Plugin für die enthaltenen Neptun-Module. GitHub Actions baut aus dem Java-Quellcode **eine JAR-Datei**; es werden keine zusätzlichen Plugin-JARs oder ein separates Server-Paket angehängt.

## Projektstruktur

- `src/main/java/` – Java-Quellcode
- `src/main/resources/plugin.yml` – Plugin-Metadaten und Commands
- `.github/workflows/build.yml` – automatischer GitHub-Build
- `pom.xml` – Maven-Konfiguration

Die `[i]`-Chat-Item-Funktion ist in `ChatItemListener.java` enthalten. Sie zeigt Informationen zum Item in der Haupthand an.

## GitHub-Build

Bei Push, Pull Request oder manuellem Start baut GitHub Actions das Projekt mit Java 21 und Maven. Öffne danach **Actions → Build NeptunCore → den neuesten erfolgreichen Lauf → Artifacts → NeptunCore**. Das Artifact enthält nur `NeptunCore-1.0.0.jar` (bzw. die JAR der aktuellen Projektversion).

Bei einem gepushten Tag wie `v1.0.1` wird zusätzlich ein GitHub Release mit der einzelnen JAR veröffentlicht.

## Installation

1. Stoppe den Paper-Server und sichere die bisherige JAR sowie den Plugin-Datenordner.
2. Lade das Artifact `NeptunCore` aus dem erfolgreichen GitHub-Actions-Lauf herunter.
3. Lege nur `NeptunCore-1.0.0.jar` in den Serverordner `plugins/`.
4. Starte den Server neu und kontrolliere die Konsole auf Fehler.

Vault, PlayerPoints und LuckPerms sind optionale Integrationen; falls du Funktionen verwendest, die sie benötigen, müssen die jeweiligen Plugins weiterhin separat installiert sein.

## Lokal bauen

Voraussetzungen: JDK 21 und Maven 3.9 oder neuer.

```bash
mvn --batch-mode --no-transfer-progress clean verify
```

Die fertige JAR liegt unter `target/NeptunCore-1.0.0.jar`.
