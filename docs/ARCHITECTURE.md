Title: Architektur – Email-Agent Always-Reply

Komponenten
1. Inbound Adapter
- Quellen: IMAP/POP3 Polling oder Provider-Webhooks (Gmail, MS Graph)
- Aufgaben: Abruf, Deduplizierung (Message-ID/Hash), Normalisierung (MIME, Anhänge)

2. Classifier & Policy Engine
- Klassifikation: incident/urgent/normal/spam (Regeln + optional ML/LLM)
- Policy: Antwortpflicht, Eskalationsregeln, Red-Flag-Filter

3. Responder & Template Engine
- Generierung von Antworten (Markdown/HTML), Sprachwahl, Personalisierung
- LLM optional mit Guardrails (Prompt-Templates, Content-Filtration)

4. Outbound SMTP & Delivery Controller
- Versand, Retries, Backoff, Deduping, Bounce-Handling

5. Escalation Service
- Anbindung an Pager/On‑Call, Eskalationsketten, Ack/Resolve-Status

6. Storage & Config
- Relationale DB (z. B. Postgres) für Mails, Tickets, Policies, Logs
- Secrets/Config über ENV, KMS/Vault für Schlüsselmaterial

7. Observability
- Metriken (SLIs), strukturierte Logs, Traces; Dashboards und Alerting

Datenfluss
Inbound -> Normalize -> Classify/Policy -> (Respond | Escalate) -> Outbound -> Log/Metric

Nichtfunktionale Anforderungen
- Verfügbarkeit: 99.9% Ziel, horizontale Skalierung der Worker
- Performance: First reply p99 ≤ 60s, Throughput ≥ 50 msg/min/Worker
- Sicherheit: Verschlüsselung in Transit/at Rest, Least Privilege, PII-Minimierung

Schnittstellen
- IMAP/POP3/Graph/Gmail API, SMTP, On‑Call API, Postgres, Metrics (Prometheus)

Deployment-Skizze
- Containerisierte Worker + Scheduler; Message-Queue optional (z. B. SQS)
- Konfiguration über ENV; CI/CD mit gestaffelten Environments
