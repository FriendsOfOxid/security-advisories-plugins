# Security Advisories

Zentrales Security-Metapackage zur Vermeidung bekannter verwundbarer Composer-Abhängigkeiten in OXID-Projekten.

Dieses Paket definiert conflict-Regeln für unsichere Paketversionen und verhindert deren Installation oder Aktualisierung.

## Zweck

- Schutz vor bekannten Sicherheitslücken in Drittanbieter-Paketen
- Zentrale Pflege durch die Agentur
- Automatische Durchsetzung bei composer update


## Installation

```
composer require friendsofoxid/security-advisories
```

## Vulnerability Check

Zur Prüfung, ob ein Projekt verwundbare Abhängigkeiten enthält, kann ein Dry-Run verwendet werden:

```
composer update --dry-run --with-all-dependencies || exit 1
```

## Verhalten

- Kein Konflikt → alle Abhängigkeiten gelten als unkritisch
- Konflikt erkannt → Composer bricht mit Fehlermeldung ab
  enthält Details zu betroffenen Paketen und Versionen

## Funktionsweise

Das Paket nutzt Composer's native conflict-Mechanik:

- Verwundbare Versionen werden explizit ausgeschlossen
- Der Dependency Resolver verhindert deren Installation
- Auch indirekte (transitive) Abhängigkeiten werden berücksichtigt

## Update-Strategie

Da neue Sicherheitslücken laufend ergänzt werden:

```
composer update friendsofoxid/security-advisories
```

## Empfohlen:

- regelmäßige Updates (z. B. im Rahmen normaler Wartung)
- Integration in CI/CD-Pipelines

## Einschränkungen

- Erkennt Probleme nur beim Dependency-Resolving
- Kein Ersatz für Laufzeit-Sicherheitsprüfungen
- Bestehende Installationen werden erst beim nächsten update geprüft

## Empfehlung

Für maximale Sicherheit:

- Kombination mit composer audit
- regelmäßige Dependency-Updates
- optionaler automatisierter Check in CI