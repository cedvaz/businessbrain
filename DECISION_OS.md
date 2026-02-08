# Decision OS: Dein Betriebssystem für Entscheidungen

> Vision: Eine AI-Schicht zwischen dir und allem anderen
> Status: Konzeption & MVP-Planung
> Erster Nutzer: Du selbst (Dogfooding)

---

## Das Problem

Du hast 6+ Business-Bereiche. Jeden Tag:
- 50+ E-Mails
- WhatsApp-Nachrichten aus 4 Kontexten
- CRM-Alerts (Propstack, Energie-CRM)
- Kalender-Chaos
- Slack/Teams von Kunden

**Das Ergebnis:**
- Context-Switching kostet 40% deiner Produktivität
- Wichtiges geht unter
- Du bist Reaktiv statt Proaktiv
- Kein System sagt dir: "Das ist JETZT wichtig"

---

## Die Vision

```
┌─────────────────────────────────────────────────────────────┐
│                     DECISION OS                              │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   INPUT (alles)         AGENT LAYER         OUTPUT           │
│   ─────────────         ───────────         ──────           │
│                                                              │
│   E-Mails          ┌──────────────────┐                      │
│   WhatsApp    ───► │  Klassifiziert   │ ───► AI-Agent        │
│   Slack            │  Priorisiert     │ ───► Mensch          │
│   CRM-Alerts  ───► │  Entscheidet     │ ───► Zurück an dich  │
│   Kalender         │  Delegiert       │ ───► Archiv          │
│                    └──────────────────┘                      │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## Core Features (Priorisiert)

### 1. Agent Delegation (MVP-FOKUS)

**Was es tut:**
- AI verteilt eingehende Aufgaben automatisch
- Klassifiziert nach: Dringend/Wichtig, Kontext, Komplexität
- Delegiert an: AI-Agent, Mensch, oder zurück an dich

**Erstes Use Case: Kalender-Agent**

```
INPUT                     AGENT                     OUTPUT
──────                    ─────                     ──────
"Können wir nächste       1. Intent erkennen        Kalendereinladung
 Woche telefonieren?"  →  2. Verfügbarkeit prüfen → an beide Parteien
                          3. Slot vorschlagen
                          4. Bestätigung holen
```

### 2. Decision Inbox (Phase 2)

**Was es tut:**
- Alle Entscheidungen an einem Ort
- Priorisiert nach Impact und Deadline
- Kontextinfo automatisch angehängt

### 3. Time-ROI Engine (Phase 3)

**Was es tut:**
- Schätzt: Wie viel ist diese Aufgabe wert?
- Berechnet: Zeit-Investment vs. erwarteter Return
- Empfiehlt: Machen / Delegieren / Ignorieren

### 4. Auto-SOPs (Phase 4)

**Was es tut:**
- Erkennt wiederkehrende Entscheidungsmuster
- Dokumentiert automatisch: "Wenn X, dann Y"
- Schlägt Automatisierung vor

---

## Tech-Stack (Empfehlung)

| Layer | Technologie | Warum |
|-------|-------------|-------|
| **Orchestration** | n8n (self-hosted) | Schnell iterieren, visuell, Open Source |
| **AI Core** | Claude API (Anthropic) | Tool Use, lange Kontexte, zuverlässig |
| **Custom Logic** | TypeScript | Wenn n8n nicht reicht |
| **Zukunft** | Claude Agents SDK | Computer Use, autonome Agents |
| **Datenbank** | Supabase/PostgreSQL | Einfach, skalierbar, Echtzeit |
| **Frontend** | Next.js oder Nuxt | Falls UI nötig |

**Warum diese Kombination?**
- n8n = 80% der Arbeit in 20% der Zeit
- Claude = Beste Reasoning-Fähigkeiten
- TypeScript = Typsicherheit, gute AI-Tooling
- Alles Open Source oder Self-Hostable

---

## MVP: Kalender-Agent

### Scope

**In Scope:**
- E-Mail-Anfragen für Termine erkennen
- Kalender-Verfügbarkeit prüfen (Google Calendar)
- Antwort-Draft mit 3 Slot-Vorschlägen
- Bestätigung und Kalendereintrag

**Out of Scope (Phase 2):**
- WhatsApp-Integration
- Voice-Anfragen
- Automatische Buchung (ohne Bestätigung)
- Multi-Kalender-Management

### User Stories

1. **Als Cedric** will ich, dass eingehende Meeting-Anfragen automatisch erkannt werden
2. **Als Cedric** will ich 3 passende Slots vorgeschlagen bekommen
3. **Als Cedric** will ich mit einem Klick bestätigen können
4. **Als Cedric** will ich, dass der Termin automatisch im Kalender landet

### Technische Architektur

```
┌─────────────────────────────────────────────────────────────┐
│                    KALENDER-AGENT MVP                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   Gmail API                                                  │
│      │                                                       │
│      ▼                                                       │
│   n8n Workflow                                               │
│      │                                                       │
│      ├──► Claude API: "Ist das eine Meeting-Anfrage?"        │
│      │                                                       │
│      ├──► Google Calendar API: Verfügbare Slots              │
│      │                                                       │
│      ├──► Claude API: "Formuliere Antwort mit 3 Slots"       │
│      │                                                       │
│      └──► Gmail Draft erstellen / Slack Notification         │
│                                                              │
│   [Du bestätigst]                                            │
│      │                                                       │
│      └──► Calendar Event erstellen + Bestätigungs-E-Mail     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Implementierung (Schritte)

| Schritt | Was | Tool | Aufwand |
|---------|-----|------|---------|
| 1 | Gmail API mit n8n verbinden | n8n | Setup |
| 2 | Trigger: Neue E-Mail | n8n | 10 min |
| 3 | Claude: Meeting-Request erkennen | n8n + Claude | 30 min |
| 4 | Google Calendar API verbinden | n8n | Setup |
| 5 | Verfügbare Slots abrufen | n8n | 30 min |
| 6 | Claude: Antwort formulieren | n8n + Claude | 30 min |
| 7 | Draft erstellen + Notification | n8n | 20 min |
| 8 | Bestätigungs-Flow | n8n | 1h |

**Geschätzter Aufwand:** 1 Wochenende fokussierte Arbeit

---

## Cashflow-Brücke: Decision OS Consulting

**Idee:** Während du Decision OS für dich baust, verkaufst du es als Service.

### Angebot: "AI Operations Audit"

| Was | Beschreibung | Preis |
|-----|--------------|-------|
| **Analyse** | 2h: Wo verlierst du Zeit? Welche Entscheidungen sind repetitiv? | 1.500€ |
| **Konzept** | Welche Agents würden dir helfen? Priorisierte Roadmap | inkl. |
| **Umsetzung** | Optional: Ersten Agent implementieren | 3.000-8.000€ |

**Positioning:**
> "Ich baue gerade mein eigenes AI Operations System.
> Ich biete dir an, das Gleiche für dich zu tun."

**Vorteil:**
- Du lernst, was andere brauchen
- Du wirst bezahlt, während du R&D machst
- Du sammelst Use Cases für das Produkt

---

## Roadmap: Decision OS

### Phase 1: Kalender-Agent (2 Wochen)
- [x] Konzept definieren
- [ ] n8n Setup
- [ ] Gmail + Calendar Integration
- [ ] Claude Prompts entwickeln
- [ ] MVP live für eigene Nutzung

### Phase 2: E-Mail Triage (4 Wochen)
- [ ] E-Mail-Klassifizierung
- [ ] Automatische Labels/Folder
- [ ] Antwort-Drafts für Routine-Mails
- [ ] Priority Inbox

### Phase 3: Unified Inbox (8 Wochen)
- [ ] WhatsApp Integration
- [ ] Slack Integration
- [ ] Zentrale Inbox UI
- [ ] Cross-Channel Context

### Phase 4: Full Agent Delegation (12+ Wochen)
- [ ] Multi-Agent Orchestration
- [ ] SOP-Automatisierung
- [ ] Time-ROI Berechnung
- [ ] Delegation an Menschen (VA)

---

## Zielgruppe (für Produkt)

### Primary: Multi-Company Gründer

**Profil:**
- 2-5 verschiedene Projekte/Companies
- Inbox-Overflow
- Zu wenig Zeit für Strategie
- Bereit, für Zeitersparnis zu zahlen

**Wo finden:**
- LinkedIn (Unternehmer-Bubble)
- Twitter/X (Tech-Founder)
- Communities (Hampton, YPO, EO)

### Secondary: Ops-Manager / Chiefs of Staff

**Profil:**
- Managed den Alltag für einen CEO
- Viele Entscheidungen, wenig Ownership
- Sucht Effizienztools

---

## Wettbewerb

| Tool | Was es kann | Was es nicht kann |
|------|-------------|-------------------|
| Superhuman | Schnelle E-Mail | Keine AI-Delegation |
| Notion | Organisation | Nicht intelligent |
| Motion | Auto-Scheduling | Nur Kalender |
| Clara/x.ai | Meeting-Scheduling | Nur Meetings |
| **Decision OS** | Alles + Delegation | - |

**Differenzierung:**
> "Decision OS ist nicht ein weiteres Tool.
> Es ist die AI-Schicht, die zwischen dir und allen anderen Tools sitzt."

---

## Nächste Schritte

1. **Heute:** Kalender-Agent Scope finalisieren
2. **Diese Woche:** n8n + Gmail + Calendar Setup
3. **Nächste Woche:** MVP live für eigene Nutzung
4. **Danach:** Erste Kunden für "AI Ops Audit" finden
