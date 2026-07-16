# Erster Umsetzungsplan

Status: Entwurf

Zuletzt aktualisiert: 2026-07-16

Die Phasen beschreiben Umfang und Abhängigkeiten. Zeitliche Schätzungen sollten erst ergänzt werden, wenn Teamgröße, Komplexität der Inhalte, externe Integrationen und Migrationsumfang bekannt sind.

## Phase 0: Analyse und Risikoreduzierung

- Rahmenbedingungen für Cloud, Identität, Bezahlung, Datenschutz, Verfügbarkeit und Aufbewahrung bestätigen.
- Das Lasttestziel auf Grundlage von bis zu 2.000 gleichzeitig aktiven Lernenden und einer zusätzlichen Sicherheitsreserve festlegen.
- Architekturentscheidung und MVP-Abnahmekriterien finalisieren.

Abschlusskriterium: Die verbleibenden Rahmenbedingungen und MVP-Abnahmekriterien sind bestätigt, und keine ungeklärte Vorgabe stellt die Zielarchitektur infrage.

## Phase 1: Plattformgrundlage

- Repository-Werkzeuge, kontinuierliche Integration, Umgebungen und Infrastruktur als Code einrichten.
- Eine minimale Plattform mit Zustandsprüfungen, strukturierter Protokollierung, Metriken und Geheimnisverwaltung bereitstellen.
- Verwaltete OIDC-Authentifizierung integrieren und interne Nutzer mit UUID anlegen.
- Zugriffsumfänge, feste Prüfungseditionen und zeitlich begrenzte Zugangsberechtigungen implementieren.
- Die erste Sicherheitsgrenze für den Admin-Bereich sowie Rollen, MFA-Richtlinie und Änderungsprotokoll einführen.

Abschlusskriterium: Lernende und Administratoren können sich in einer Nicht-Produktionsumgebung authentifizieren, und geschützte Zugriffe werden serverseitig durchgesetzt.

## Phase 2: MVP für Lernen und Zugang

- Kurse und Themen, feste Editionszuordnungen, versionierte Fragen, serverseitige Bewertung, Sitzungen, Fragenauslieferungen, Antwortversuche und Fortschritt implementieren.
- Den für Mobilgeräte optimierten Lernablauf und grundlegende Barrierefreiheit umsetzen.
- Chargen für Printcodes und deren atomare Einlösung implementieren.
- Eine Webhook-Integration für Online-Käufe ergänzen, sofern diese zum MVP-Umfang gehört.
- Im Admin-Bereich Nutzersuche, Einsicht in Zugänge sowie Vergabe, Verlängerung und Widerruf von Zugangsberechtigungen bereitstellen.

Abschlusskriterium: Ein berechtigter Lernender kann eine repräsentative Lernsitzung abschließen, und ein Administrator kann das Konto sicher betreuen.

## Phase 3: Inhaltsadministration und Moodle-Migration

- Den Moodle-Parser für die unterstützten Inhalte und die deterministische Normalisierung fertigstellen.
- Bilder und Formelquellen extrahieren, validieren und speichern.
- Importläufe, Diagnosen, Idempotenz, Konflikterkennung und erneute Verarbeitung ergänzen.
- Im Admin-Bereich Importvorschau, Versionshistorie der Fragen, Bearbeitung, Editionszuordnung, Freigabe und Veröffentlichung bereitstellen.
- Probemigrationen durchführen und Anzahl, Darstellung sowie Bewertungsergebnisse abgleichen.

Abschlusskriterium: Freigegebene Inhalte können wiederholt migriert werden, ohne Duplikate oder unbemerkte Änderungen an der Bewertung zu verursachen.

## Phase 4: Produktionsreife und Umstellung

- Sicherheits-, Barrierefreiheits-, Leistungs- und Wiederherstellungstests durchführen.
- Die abgestimmte Prüfungsspitze einem Lasttest unterziehen und zeitgesteuerte beziehungsweise automatisch skalierende Kapazitäten konfigurieren.
- Backups durch Wiederherstellung validieren und Monitoring sowie Reaktion auf Störungen testen.
- Datenschutzprozesse für Export, Löschung und Aufbewahrung vervollständigen.
- Einen Pilotbetrieb mit ausgewählten Nutzern durchführen, Migrationsabweichungen beheben und die Rückkehr zur vorherigen Version proben.
- Moodle-Inhalte einfrieren, die finale Migration in die vorgesehene Prüfungsedition durchführen, Ergebnisse abgleichen und die Plattform umstellen.

Abschlusskriterium: Die Verantwortlichen für Betrieb, Migration und Produkt geben den Produktivstart sowie die Bereitschaft zur Rückkehr auf die vorherige Version frei.

## Spätere Ausbaustufen

- KI-Tutor auf Basis freigegebener Inhalte.
- Kostenpflichtige Berechtigungen für KI-Funktionen, Nutzungsgrenzen und separate Aufbewahrung von Unterhaltungen.
- Regelbasiertes adaptives Lernen mit anschließenden, messbaren Modellversuchen.
- Datenlager, zusätzliche Dienste oder native Apps nur dann, wenn Produkt- oder Betriebsdaten sie rechtfertigen.

## Erstes Präsentationsergebnis

Empfohlene Struktur mit drei Folien:

1. Zielarchitektur, Technologieentscheidungen und Entscheidung für einen modularen Monolithen.
2. Datenmodell, Moodle-Import, Admin-Umfang, Sicherheit und Skalierung.
3. Umsetzungsphasen und unmittelbarer nächster Schritt bis zur Moodle-Ablösung.
