Title: Konfiguration & Umgebungsvariablen

Übersicht
Der Agent wird ausschließlich über ENV-Variablen konfiguriert. Secrets werden über ein Secret-Management (z. B. Vault/KMS) injiziert.

Inbound
- EMAIL_INBOUND_PROVIDER: imap | pop3 | webhook
- EMAIL_IMAP_HOST, EMAIL_IMAP_PORT, EMAIL_IMAP_TLS=true|false
- EMAIL_IMAP_USERNAME, EMAIL_IMAP_PASSWORD (Secret)
- EMAIL_INBOUND_POLL_INTERVAL_MS: Standard 15000

Klassifikation & Policy
- CLASSIFIER_MODE: rules | ml | llm
- POLICY_LANGUAGE_DEFAULT: de | en | ...
- POLICY_SPAM_THRESHOLD: 0.9 (für ml/llm)

LLM (optional)
- LLM_PROVIDER: openai | azure | anthropic | disabled
- LLM_MODEL: z. B. gpt-4o-mini
- LLM_API_KEY (Secret)
- LLM_MAX_TOKENS, LLM_TEMPERATURE

Outbound
- SMTP_HOST, SMTP_PORT, SMTP_TLS=true|false
- SMTP_USERNAME, SMTP_PASSWORD (Secret)
- SMTP_FROM_ADDRESS, SMTP_FROM_NAME
- SMTP_RATE_LIMIT_PER_MINUTE

Eskalation
- ESCALATION_PROVIDER: pagerduty | opsgenie | webhook | disabled
- ESCALATION_API_KEY (Secret), ESCALATION_SERVICE_ID
- ESCALATION_FALLBACK_WEBHOOK_URL

Storage
- DATABASE_URL (Secret)
- REDIS_URL | QUEUE_URL (optional)
- DATA_RETENTION_DAYS: z. B. 30

Observability
- LOG_LEVEL: debug | info | warn | error
- METRICS_PORT: 9464
- ALERT_WEBHOOK_URL

Ressourcen & Performance
- MAX_CONCURRENCY: z. B. 8
- RETRY_BACKOFF_MS: 1000, MAX_RETRY_ATTEMPTS: 5
- DUPLICATE_WINDOW_MS: 300000

Lokale Entwicklung (.env Beispiel)
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_TLS=true
SMTP_FROM_ADDRESS=agent@example.com
LOG_LEVEL=info

Hinweise
- Änderungen an ENV erfordern Neustart/Reload
- Validierung: Beim Start wird das ENV-Schema geprüft; Start verweigert bei Fehlern
