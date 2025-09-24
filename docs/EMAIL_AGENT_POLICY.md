Title: Email Agent Policy – Always Reply & Emergencies

Grundprinzipien
- Always Reply: Jede E‑Mail erhält eine Antwort. Keine Aufschübe, keine manuelle Verschiebung.
- Safety First: Notfälle sofort eskalieren, dann minimal hilfreiche Antwort senden.
- Transparenz: Klar kommunizieren, was automatisiert ist; bei Unsicherheit konservative Antworten.

Klassifikation
- incident: Lebens-/Geschäftskritisch, eindeutige Notfallindikatoren ("outage", "data breach", "urgent help")
- urgent: Zeitkritisch, aber nicht existenziell
- normal: Standardanfragen
- spam: Werbe/Phishing/irrelevant; dennoch minimal höfliche Ablehnung wenn eindeutig

Antwortregeln
- incident: Sofort On‑Call eskalieren; automatisches Acknowledgement inkl. Ticket/Incident-ID; Follow-up innerhalb 5min
- urgent: Bestätigung ≤ 60s, substanziell ≤ 5min; ggf. Priorisierung
- normal: Kontextbezogene Antwort oder qualifizierte Bestätigung mit ETA
- spam: Höfliche Ablehnung oder keine Antwort, je nach Policy und rechtlichem Rahmen

Inhaltliche Leitplanken
- Keine vertraulichen Daten preisgeben; minimal notwendige Informationen verwenden
- Keine rechtlichen Zusagen; keine Falschinformationen; Quellen vermerken, wenn relevant
- Mehrsprachigkeit anhand Eingangs-Mail; Fallback Englisch/Deutsch

Qualitätssicherung
- Templates mit Pflicht-Platzhaltern; LLM-Antworten durch Regeln postvalidieren
- Blacklist/Whitelist von Triggerwörtern für Eskalation
- Stichprobenhafte manuelle Reviews
