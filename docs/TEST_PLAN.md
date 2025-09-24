Title: Testplan – Email-Agent

Ziele
- Sicherstellen, dass 100% der eingehenden E‑Mails beantwortet werden, SLAs eingehalten sind und Notfälle korrekt eskaliert werden.

Testpyramide
- Unit: Regeln, Parser, Normalisierung, Template-Platzhalter
- Integration: IMAP/Webhook Intake, SMTP Outbound, Escalation-API, DB
- E2E: Komplettfluss von Eingang bis Antwort/Eskalation
- Nicht-funktional: Last, Resilienz/Chaos, Sicherheit, LLM-Safety

Kritische Szenarien (E2E)
1) Normalanfrage -> Bestätigung ≤ 60s, substanziell ≤ 5min, keine Duplikate
2) Incident-Mail -> Eskalation ≤ 60s, Acknowledgement, Follow-up innerhalb 5min
3) Spam/Phishing -> Klassifikation „spam“, keine Zustellung an Nutzer, höfliche Ablehnung (Policy)
4) Provider-Ausfall Inbound -> Failover, Backlog-Aufarbeitung ohne SLA-Bruch
5) SMTP-Softbounce -> Retries mit Backoff, letztlich Zustellung oder Fehlerlog
6) LLM deaktiviert -> Regel-/Template-Fallback funktioniert

Qualitätsmetriken
- Coverage: ≥ 80% Statements im Core, 100% der Policies mit Tests belegt
- SLIs: time_to_first_reply p99, time_to_substantive_reply p95, delivery_success_rate

Sicherheitstests
- Fuzzing von MIME/Headers; Attachment-Malware-Simulation
- Prompt-Injection-Tests, Jailbreak-Versuche; PII-Leakage-Prevention
- Secrets-Scans, Dependency-Audits, Container-Scans

Last- & Resilienztests
- Lastprofile: 50/200/500 Mails pro Minute; Skalierung linear innerhalb ±20%
- Chaos: Inbound/Outbound/DB/Queue-Ausfall; Recovery-Zeit < 5min

Abnahmetests
- Checkliste aus `FINISH_CRITERIA.md`; Stakeholder-Sign-off
