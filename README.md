# Email-Agent: Automatischer Antwort- und Notfall-Responder

Dieser Repository definiert Zielbild, Arbeitsplan und Betriebsgrundlagen für einen produktionsfähigen E‑Mail-Agenten, der auf **jede eingehende E‑Mail** antwortet – ohne Aufschub – und in **Notfällen automatisch eskaliert**. Der Quellcode folgt nach Abschluss der Planungs‑ und Designphase. Alle Dokumente in `docs/` beschreiben präzise, wie der „Finish“-Zustand aussehen muss.

## Zielbild (Definition of Done – Überblick)
- Der Agent beantwortet jede E‑Mail automatisch mit einer kontextbezogenen Antwort oder mindestens einer zeitnahen Eingangsbestätigung (SLA siehe unten).
- Notfälle werden erkannt und nach klarer Policy sofort eskaliert (On‑Call/Incident‑Flow).
- Keine E‑Mail bleibt unbeantwortet, es gibt keine „Später“-Queues oder Aufschübe.
- Vollständige Nachvollziehbarkeit: Audit‑Log, Monitoring, Metriken, Alarmierung.
- Sichere Verarbeitung: Verschlüsselung, Secrets‑Handling, Least Privilege, Datenminimierung.
- Konfigurierbar über Umgebungsvariablen; reproducible Deployments; saubere Runbooks.

Die detaillierten Abnahmekriterien stehen in `docs/FINISH_CRITERIA.md`.

## Kernfunktionen
- Always‑Reply: Jede eingehende E‑Mail erhält innerhalb definierter SLAs eine Antwort.
- Notfall‑Erkennung: Klassifikation (z. B. „incident“, „urgent“, „normal“, „spam“).
- Eskalation: Automatisches Paging/On‑Call bei Notfällen, inklusive mehrstufiger Eskalationskette.
- Antwortgenerierung: Regel‑ und Template‑basiert; optional LLM‑gestützt mit Guardrails.
- Zustellung & Retries: Zuverlässiges SMTP mit Backoff, Idempotenz und Duplikat‑Schutz.
- Observability: Logs, Traces, Metriken, Dashboards, SLIs/SLOs/SLAs.

## Architektur (Kurzüberblick)
Die Zielarchitektur und Datenflüsse sind in `docs/ARCHITECTURE.md` beschrieben. Kernkomponenten:
- Inbound (IMAP/POP3/Webhook)
- Classifier & Policy Engine
- Responder & Template Engine (LLM‑fähig, aber policy‑gesteuert)
- Outbound SMTP & Delivery Controller
- Escalation Service (On‑Call/Pager)
- Storage (z. B. Postgres) und Secrets/Config
- Observability (Monitoring/Alerting)

## Betriebs- und Sicherheitsziele
- SLAs: Eingangsbestätigung ≤ 60s (p99), substanzielle Antwort ≤ 5min (p95), 0% unbeantwortete Mails.
- Security: Transport‑ und Ruhe‑Verschlüsselung, Secret Rotation, PII‑Schutz, minimaler Zugriff.
- Compliance: Audit‑Trails, Datenaufbewahrung, Löschkonzepte (siehe `docs/SECURITY.md`).

## Dokumentation
Die vollständige Dokumentation steht im Ordner `docs/`:
- `WORKPLAN.md`: Arbeitsplan, Phasen, Meilensteine, Risiken.
- `FINISH_CRITERIA.md`: Abnahmekriterien/Definition of Done.
- `ARCHITECTURE.md`: Zielarchitektur und Datenflüsse.
- `EMAIL_AGENT_POLICY.md`: Verhaltens- und Antwort‑Policy (inkl. Notfälle, „immer antworten“).
- `RUNBOOK.md`: Betrieb, Incident‑Response, Notfallmaßnahmen.
- `SECURITY.md`: Sicherheitskonzept, Datenschutz, Geheimnisse.
- `CONFIGURATION.md`: Konfigurations‑ und Umgebungsvariablen.
- `TEST_PLAN.md`: Teststrategie, E2E‑Szenarien, Qualitätssicherung.

## Status & Nächste Schritte
Diese Commit‑Serie liefert die vollständige Planungs‑ und Zieldokumentation. Im nächsten Schritt wird das Projektgerüst (Code, CI/CD, Infrastruktur) gemäß `docs/WORKPLAN.md` aufgebaut und iterativ bis zum Finish‑Zustand umgesetzt.
