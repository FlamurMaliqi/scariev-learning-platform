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

Die Anwendungsverzeichnisse werden ergänzt, sobald die technische Voruntersuchung das Moodle-Format, die Betriebsvorgaben und die Framework-Auswahl bestätigt hat.

```text
apps/
  platform/             Webanwendung für Lernende und Administration einschließlich API
packages/
  database/             Schema, Migrationen und Datenbankzugriff
  moodle-import/        Parser, Normalisierung, Validierung und Importberichte
infrastructure/         Bereitstellung und Infrastruktur als Code
docs/                   Architektur, Entscheidungen und Umsetzungsplan
```

## Noch ausstehende Entscheidungen

1. Ob AWS in einer EU-Region akzeptabel ist.
2. Ob die Migration neben Inhalten auch Moodle-Nutzer, Zugangszeiträume und Lernfortschritte umfasst.
3. Ein repräsentativer Moodle-Export sowie eine Übersicht der Fragetypen und Plugins.
4. Ob der Produktzugang mit dem Kauf, der Codeeinlösung oder der ersten Nutzung beginnt.
5. Ob Produkte eine feste Prüfungsedition oder stets die aktuellen Inhalte freischalten.
6. Die erwartete maximale Anzahl gleichzeitig aktiver Lernender.
