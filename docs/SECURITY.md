Title: Sicherheitskonzept – Email-Agent

Ziele
- Schutz von personenbezogenen Daten (PII) und Geschäftsgeheimnissen
- Minimierung von Angriffsflächen; Einhaltung von SLAs ohne Sicherheitskompromisse

Bedrohungsmodell
- Angreifervektoren: bösartige E-Mails (Phishing, Malware), SMTP/IMAP-Man-in-the-Middle, API-Missbrauch, Credential-Leaks, Prompt-Injection (LLM)
- Auswirkungen: Datenabfluss, falsche Antworten, verpasste Notfälle, Rufschädigung

Grundsätze
- Least Privilege: minimale Rechte für Services/Keys
- Verschlüsselung: in Transit (TLS 1.2+) und at Rest (AES-256, KMS)
- Datenminimierung: nur erforderliche Felder speichern; Body optional gekürzt/gehasht
- Geheimnisse: nie im Code/Logs; Rotation und Audit

Technische Maßnahmen
- Transport: SMTPS/STARTTLS, IMAPS/POP3S, HSTS/Strict TLS-Konfiguration
- Authentizität: SPF, DKIM, DMARC korrekt konfiguriert; regelmäßige Überprüfung
- Attachment-Handling: Viren-/Malware-Scan (z. B. ClamAV), Quarantäne bei Verdacht
- Eingangsfilter: MIME-Sanitizing, Header-Validierung, Schutz vor Header Injection
- LLM-Schutz: Keine PII an LLM senden ohne Einwilligung; Prompt- und Output-Filter; Red-Teaming
- Logging: PII-Redaktion (E-Mail-Adressen maskieren), keine Klartext-Secrets, Sampling
- Zugriff: SSO/MFA für Admin-Konsolen; rollenbasierte Rechte; zeitlich begrenzte Zugriffe
- Monitoring: Sicherheits-Metriken, Anomalie-Erkennung, Alerting

Prozesse
- Secret-Rotation: vierteljährlich oder bei Verdacht; dokumentiert im Runbook
- Schwachstellenmanagement: monatliche Scans, Abhängigkeits-Updates, CVE-Review
- Incident-Handling: Security-Incidents nach RUNBOOK-Prozess mit separater Root-Cause-Analyse
- Datenaufbewahrung: Lösch-/Anonymisierungspläne, Aufbewahrungsfristen (Konfig: `DATA_RETENTION_DAYS`)

Compliance & Datenschutz
- Audit-Logs manipulationssicher und zeitgestempelt
- Betroffenenrechte (DSR): Auskunft/Löschung innerhalb definierter Fristen
- Auftragsverarbeitung und Drittanbieter-Review (LLM/On-Call/Email-Provider)
