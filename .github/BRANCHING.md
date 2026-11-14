# Branches und Releases

Der Standardbranch ist `develop`. Neue Features und Fehlerkorrekturen werden per PR
nach `develop` gemergt. Die langfristigen Branches bleiben bestehen:

1. `develop`: Integration und automatische CI-Prüfungen.
2. `TuA`: Freigegebener Stand für Test und Abnahme; Schreibweise beachten.
3. `main`: Produktiver Stand nach abgeschlossener Abnahme.

## Update vorbereiten und freigeben

```sh
gh pr create --base TuA --head develop --title "Test und Abnahme: nächstes Update"
# PR prüfen und mergen; anschließend CI und Tests auf TuA abwarten.
# Nach erfolgreicher fachlicher Abnahme:
gh pr create --base main --head TuA --title "Release: abgenommenes Update"
```

Promotions mit einem **Merge-Commit** mergen, damit die gemeinsame Historie der
langfristigen Branches erhalten bleibt. Die PR-Prüfung `Promotion policy` meldet
andere Quellbranches für `TuA` und `main` als Fehler. Eine verbindliche Merge-Sperre
benötigt zusätzlich passende Branch-Schutzregeln im GitHub-Tarif.

Nach einem Release Änderungen aus `main` wieder nach `develop` übernehmen, besonders
wenn die Pipeline auf `main` automatisch Versionsnummern erhöht hat. Langfristige
Branches und bestehende Plattform- oder Artefaktbranches nicht automatisch löschen.

## Artefakt-Repository

Dieses öffentliche Repository erhält ausschließlich veröffentlichte Artefakte.
Die eigentlichen Build- und Release-Pipelines liegen im privaten Quellcode-Repository.
Der zusätzliche Branch `gh-pages`, falls vorhanden, bleibt für die OTA-Seite bestehen.

## Migration

Die Umstellung der Pipeline-Dateien auf `main` wurde mit `[skip ci]` vorgenommen,
damit die Konfigurationsmigration selbst kein Produktionsdeployment auslöst.
Die bisherigen Feature-Branches bleiben erhalten.
