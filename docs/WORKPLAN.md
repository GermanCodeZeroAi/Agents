Title: Arbeitsplan – Email-Agent Always-Reply mit Notfall-Eskalation

Ziel: Produktionsreifer Agent, der jede E‑Mail beantwortet und Notfälle automatisch eskaliert. Umsetzung ausschließlich im `main`-Branch.

Phasen und Meilensteine

1) Planung & Zielbild (aktuell)
- Ergebnisse: README, WORKPLAN, FINISH_CRITERIA, ARCHITECTURE, EMAIL_AGENT_POLICY, RUNBOOK, SECURITY, CONFIGURATION, TEST_PLAN
- Exit-Kriterium: Abnahme aller Docs, eindeutiges Zielbild

2) Projektgerüst & Infrastruktur
- Repo-Struktur, Paketmanager, Basis-CI (Lint/Test/Build), Devcontainer/Docker
- Secrets-Management (z. B. Doppler/Vault), ENV-Schema
- Observability-Basics: strukturierte Logs, Healthchecks
- Exit: CI grün, lokal lauffähig, Deployment-Stubs vorhanden

3) Inbound E‑Mail Intake
- IMAP/POP3 Poller oder Provider-Webhooks (z. B. Gmail/Microsoft Graph)
- Idempotenz (Message-ID/Hashes), Duplikat-Prävention
- Normalisierung (MIME/Attachments), PII-Minimierung
- Exit: Stabiler Intake mit Tests, Metriken für Durchsatz/Fehler

4) Klassifikation & Policy Engine
- Regelwerk + ML/LLM-gestützte Heuristiken (mit Guardrails)
- Kategorien: incident/urgent/normal/spam
- Exit: ≥ 95% Präzision auf Testdaten, deterministische Fallbacks

5) Antwortgenerierung
- Template-Engine (Markdown/HTML), Sprachunterstützung, personalisierte Felder
- LLM optional, strikt policy-gesteuert, Red-Teaming für Prompt-Sicherheit
- Exit: Kontextsensitive Antworten; SLAs werden in Staging eingehalten

6) Outbound & Zustellung
- SMTP-Client mit Retries/Backoff, SPF/DKIM/DMARC Vorbereitung
- Bounce-Handling, Rate Limits, Deduping
- Exit: Zustellrate ≥ 98% in Testumgebung, robuste Retry-Pfade

7) Eskalation & On-Call
- Integration (PagerDuty/Opsgenie/Custom), Eskalationskette, Ack/Resolve-Loop
- Playbooks (siehe RUNBOOK)
- Exit: Incident-Simulationen erfolgreich

8) Observability & SLOs
- Metriken: time_to_first_reply, time_to_substantive_reply, unanswered=0
- Dashboards, Alerts (Budget Burn Rates für SLOs)
- Exit: Warnungen bei SLA-Verletzung, Audit-Logs vollständig

9) Sicherheit & Compliance
- Secrets Rotation, Least Privilege, Verschlüsselung, DSR (Data Subject Requests)
- Aufbewahrung/Löschung, DSGVO-Basics
- Exit: SECURITY-Checks grün, Pentest-Findings adressiert

10) Staging -> Produktion
- Canary, Feature Flags für LLM, Runbook-Abdeckung
- Exit: Go-Live-Freigabe, Abnahme gegen FINISH_CRITERIA

Zeitziele (Richtwerte)
- Phasen 2–6: 6–8 Wochen
- Phasen 7–10: 2–4 Wochen

Risikomanagement
- Provider-Limits (IMAP/Webhooks), LLM-Qualität, Zustellbarkeit (Spamfilter)
- Gegenmaßnahmen: Caching/Backpressure, strikte Policies, Warmup-Domains

Kommunikation
- Wöchentliche Statusreports, Incident-Reviews, Change-Logs
