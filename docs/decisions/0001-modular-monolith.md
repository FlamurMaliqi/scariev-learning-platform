# ADR 0001: Start als modularer Monolith

Status: Vorgeschlagen

Datum: 2026-07-16

## Kontext

Die Plattform muss Moodle ersetzen, ein für Mobilgeräte optimiertes Lernerlebnis und ein Admin-Portal bieten, komplexe Inhalte migrieren, den Lernverlauf bewahren und von einigen Tausend Nutzern bis auf 10.000 Nutzer einschließlich Prüfungsspitzen skalieren.

Die wesentlichen anfänglichen Risiken liegen in der Migration von Inhalten, der korrekten Bewertung, den Regeln für Produktzugänge, der Sicherheit und dem Nutzererlebnis. Der Durchsatz unabhängiger Dienste oder eine organisationsweite Verantwortung für Bereitstellungen gehören dagegen nicht zu den frühen Risiken.

## Entscheidung

Lernenden- und Admin-Oberfläche, versionierte API und Domänenmodule werden als eine bereitstellbare Anwendung mit PostgreSQL als Datenbank umgesetzt. Webanfragen und Hintergrundarbeiten werden als getrennte Prozesstypen aus derselben Codebasis und demselben Container-Abbild ausgeführt.

Für Identität, Zugriff, Inhalte, Lernen, Administration, Import, Betrieb und die zukünftige KI-Integration werden klare Modulgrenzen beibehalten. Diese Grenzen werden durch Codeverantwortung und öffentliche Modul-APIs statt durch Netzwerkaufrufe durchgesetzt.

## Konsequenzen

Vorteile:

- eine Codebasis, eine Bereitstellungspipeline und ein transaktionales Datenmodell;
- einfachere Entwicklung, Tests, Störungsbehebung und lokale Einrichtung;
- atomare Abläufe für Zugangseinlösung, Antwortabgabe und Veröffentlichung;
- ausreichende horizontale Skalierbarkeit für die erwartete Nutzerzahl;
- Module können später herausgelöst werden, ohne bereits jetzt spekulative Dienste entwerfen zu müssen.

Abwägungen:

- Ein Fehler oder eine Bereitstellung kann mehrere Module betreffen;
- Modulgrenzen erfordern Disziplin, da die Datenbank gemeinsam genutzt wird;
- Web- und Hintergrundprozesse folgen zunächst demselben Veröffentlichungszyklus.

## Erneute Prüfung

Ein Modul wird nur dann herausgelöst, wenn mindestens eine messbare Bedingung erfüllt ist:

- Es erfordert eine wesentlich andere Skalierung oder Verfügbarkeit;
- ein separates Team verantwortet und veröffentlicht es unabhängig;
- seine Sicherheits- oder Datenresidenzgrenze kann in der Anwendung nicht durchgesetzt werden;
- die Hintergrundlast beeinträchtigt trotz Prozesstrennung die Latenz der Anfragen von Lernenden;
- eine gemessene Kopplung von Datenbank oder Bereitstellung wird zu einer wesentlichen Einschränkung.

Bis dahin sind Kubernetes, Kafka, ein Dienstnetz und separate Datenbanken pro Modul nicht Bestandteil des Umfangs.
