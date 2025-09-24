Title: Runbook – Betrieb und Incident-Response

Zweck
Dieses Runbook beschreibt den operativen Betrieb des Email-Agents, inklusive täglicher Checks, Notfallabläufe (Incident-Response), Wartung und Wiederherstellung.

Kontakt & On-Call
- Primary On-Call: <Team/Rotation>, 24/7, Eskalation via Provider (z. B. PagerDuty)
- Eskalationsstufen: L1 (5min), L2 (15min), L3 (30min)
- Kommunikationskanäle: Incident-Ticket, Telefon/Chat, Status-Seite

Tägliche Betriebs-Checks (≤ 10 Minuten)
- Dashboards: SLIs/SLOs (time_to_first_reply, unanswered==0, error_rate)
- Queues: Inbound/Outbound Tiefstand, keine Backlogs, keine stuck messages
- Logs: Kein Spike bei 4xx/5xx; keine wiederholten SMTP Bounces
- Deliverability: SPF/DKIM/DMARC gültig; Bounce- und Complaint-Rate < 1%

Standardprozeduren
1) Deployment
- Über CI/CD ausrollen; Healthchecks prüfen; Canary (kleiner Traffic-Anteil)
- Rollback: Vorherige Version wiederherstellen, Change im Changelog dokumentieren

2) Konfigurationsänderungen
- Änderungen ausschließlich über ENV/Secrets; Vier-Augen-Prinzip
- Nach Änderung: Neustart/Reload, Smoke-Tests, Monitoring prüfen

3) Secret-Rotation
- Planen (Zeitfenster), rotieren (KMS/Vault), Services nacheinander aktualisieren
- Verifizieren (Healthchecks), Altes Secret nach Grace-Periode widerrufen

4) Template-/Policy-Updates
- Änderungen in `EMAIL_AGENT_POLICY.md` bzw. Templates; Unit/E2E-Tests ausführen
- Freigabe durch Fachseite; in Produktion deployen

Incident-Response (Major)
Trigger: Klassifikation „incident“ oder Metrik verletzt (z. B. unanswered>0, SLA-Verstoß)
Schritte:
1. Alarmannahme (≤ 5min): On-Call bestätigt Alarm (ACK)
2. Erstreaktion (≤ 10min): Eskalationskette aktiv; Status-Seite/Stakeholder informieren
3. Triage: Ursache bestimmen (Inbound-Fehler, Classifier, Outbound/SMTP, Escalation, DB)
4. Eindämmung: Traffic drosseln, Queue pausieren, Fallback-Antwort aktivieren
5. Behebung: Service neu starten, Konfig fixen, Provider-Störung umgehen
6. Wiederherstellung: Queues abarbeiten, Backlog priorisieren, SLAs neu kalkulieren
7. Nachbereitung: Postmortem innerhalb 48h, Maßnahmen tracken

Störungsszenarien & Playbooks (Kurzfassung)
- Inbound down: Providerstatus prüfen; Failover (zweiter Provider/Webhook) aktivieren; Backlog konservativ abarbeiten
- Klassifikation fehlerhaft: Auf Regel-Fallback schalten; ML/LLM abschalten; Templates verwenden
- Outbound Bounces: SPF/DKIM/DMARC prüfen; Rate-Limits reduzieren; Backoff erhöhen
- Escalation Provider down: Alternative Benachrichtigung (SMS/Telefon/Webhook) nutzen
- DB-Problem: Read-replica nutzen; begrenzten Degradationsmodus (nur Acknowledgements) aktivieren

Backups & Restore
- DB-Snapshots: stündlich inkrementell, täglich voll; Aufbewahrung 30 Tage
- Wiederherstellung: Snapshot wählen -> Restore -> Migrations prüfen -> Services reattachen
- Test-Restore: monatlich validieren

KPIs/SLIs/SLOs
- SLIs: time_to_first_reply, time_to_substantive_reply, delivery_success_rate, escalation_latency
- SLOs: p99 ≤ 60s (first), p95 ≤ 5min (substantive), delivery ≥ 98%
- Fehlerbudgets: Automatische Warnungen bei Budget-Burn > 2%/Tag

Wartung
- Zertifikate/Keys erneuern, Domain-DNS (SPF/DKIM/DMARC) prüfen, LLM-Models/Policies aktualisieren
- Sicherheitsupdates monatlich; Notfall-Patches zeitnah

Checklisten
- Go-Live: Health, Config, Secrets, Observability, Runbooks, Rollback getestet
- Pre-Change: Impact, Backout-Plan, Monitoring, Stakeholder informiert

Anhang
- Kontaktmatrix, Eskalationskette, Status-Seiten-Links, Provider-Kontakte
