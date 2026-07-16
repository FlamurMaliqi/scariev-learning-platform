# Scariev Lernplattform

Arbeitsbereich für Architektur und Umsetzung zur Ablösung der bestehenden Moodle-basierten Plattform für die medizinische Prüfungsvorbereitung.

## Aktueller Stand

Das Projekt befindet sich in der Architekturkonzeption. Eine produktionsfähige Anwendung wurde noch nicht aufgesetzt. Das erste Ergebnis ist ein kompakter Architekturvorschlag mit 1–3 Folien sowie ein erster Umsetzungsplan.

## Erstes Ergebnis

Der Vorschlag umfasst:

- Zielarchitektur und Technologieempfehlung;
- zentrales Datenmodell;
- Moodle-Import für Fragen, Formeln und Bilder;
- Funktionen für Lernende und Administration;
- Identitätsverwaltung, zeitlich begrenzte Zugänge und Einlösung von Printcodes;
- Sicherheit, Datenschutz, Monitoring und Skalierung;
- Umsetzungsphasen und wesentliche offene Entscheidungen.

## Architekturüberblick

Die aktuelle Empfehlung ist ein modularer Monolith:

- Next.js, React und TypeScript für die für Mobilgeräte optimierte Lernoberfläche und das Admin-Portal;
- eine versionierte HTTP-API innerhalb derselben auslieferbaren Anwendung;
- verwaltete OIDC-Authentifizierung mit einem internen UUID-basierten Nutzermodell;
- PostgreSQL als führendes Datensystem;
- Objektspeicher und CDN für Bilder und Quelldateien von Importen;
- ein Hintergrundprozess aus derselben Codebasis für Importe und andere länger laufende Aufgaben;
- eine AWS-Referenzbereitstellung mit CloudFront/WAF, ECS Fargate, RDS PostgreSQL, S3, SQS und CloudWatch;
- zukünftige KI-Funktionen hinter einer kontrollierten Schnittstelle und dem bestehenden Zugangsberechtigungsmodell.

Siehe [Zielarchitektur](docs/architecture.md), [Umsetzungsplan](docs/implementation-plan.md) und [ADR 0001](docs/decisions/0001-modular-monolith.md).

## Geplante Anwendungsstruktur

Die Anwendungsverzeichnisse werden ergänzt, sobald Betriebsvorgaben und Framework-Auswahl bestätigt sind.

```text
apps/
  platform/             Webanwendung für Lernende und Administration einschließlich API
packages/
  database/             Schema, Migrationen und Datenbankzugriff
  moodle-import/        Parser, Normalisierung, Validierung und Importberichte
infrastructure/         Bereitstellung und Infrastruktur als Code
docs/                   Architektur, Entscheidungen und Umsetzungsplan
```

## Bestätigte Rahmenbedingungen

1. Der Betrieb erfolgt bei AWS in einer EU-Region.
2. Aus Moodle werden ausschließlich Inhalte migriert; Nutzer, Zugangszeiträume und Lernfortschritte werden nicht übernommen.
3. Bei Online-Käufen beginnt der Zugang nach bestätigter Zahlung; bei Printprodukten beginnt er mit der Codeeinlösung.
4. Während der Zugangslaufzeit erhalten Nutzer stets die aktuell veröffentlichten Inhalte und keine feste Prüfungsedition.
5. Die Architektur wird auf eine Prüfungsspitze von bis zu 2.000 gleichzeitig aktiven Lernenden ausgelegt.
