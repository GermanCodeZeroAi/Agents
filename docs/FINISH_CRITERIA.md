Title: Definition of Done – Email-Agent

Funktional
- Always-Reply: 100% der eingehenden E‑Mails erhalten eine Antwort.
- SLA: Eingangsbestätigung ≤ 60s (p99), substanzielle Antwort ≤ 5min (p95).
- Notfälle: „incident/urgent“ werden in ≤ 60s eskaliert, On‑Call benachrichtigt.
- Klassifikation: ≥ 95% Präzision auf Validationset, deterministischer Fallback.
- Outbound: Zustellrate ≥ 98% in Staging, Retries/Backoff implementiert.
- Idempotenz: Keine Doppelantworten auf identische Message-ID.

Qualität & Betrieb
- Tests: Unit/Integration/E2E vorhanden; kritische Pfade abgedeckt (≥ 80% Statement-Coverage in Core).
- Observability: Metriken, strukturierte Logs, Traces, Dashboards, Alerts.
- Runbook: Vollständige Incident- und On-Call-Prozesse dokumentiert und geübt.
- Security: Secrets Management, Verschlüsselung, Least Privilege; Audit-Log unveränderlich.

Docs & Konfiguration
- README und alle `docs/*` aktuell und konsistent.
- Konfiguration über ENV-Variablen dokumentiert; sichere Defaults; Schema validiert.

Abnahme
- E2E-Drills: Simulierte Notfall-E-Mail triggert korrekte Eskalation und Antwort.
- Stakeholder sign-off mit Checkliste aus diesem Dokument.
