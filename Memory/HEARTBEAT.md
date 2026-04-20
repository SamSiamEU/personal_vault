# HEARTBEAT — Monitoring Checklist

> This file tells the heartbeat script (`heartbeat.py`) what to monitor and how to behave.
> Edit this file to tune what gets surfaced and when.

## Schedule

- **Frequency:** Every 30 minutes
- **Active hours:** 07:00–20:00 CET, Monday–Friday
- **Daily reflection:** 07:30 CET daily (separate script: `memory_reflect.py`)

## Monitoring Checklist

### Calendar
- [ ] Meetings in the next 2 hours with no prep notes in vault
- [ ] Meetings today with no follow-up notes (after they've passed)
- [ ] Deadlines on calendar within 48 hours

### Gmail
- [ ] Threads awaiting reply for more than 48 hours
- [ ] New messages from Acqura stakeholders, Eksido clients, Merkle leadership
- [ ] Auto-generate drafts for qualifying threads (see drafting criteria in USER.md)

### Salesforce (Eksido pipeline)
- [ ] Opportunities with CloseDate within 30 days and no recent activity (>7 days)
- [ ] Overdue tasks assigned to Dennis
- [ ] Contacts not contacted in 30+ days (from people on radar in MEMORY.md)

### Vault / Open Loops
- [ ] Items tagged `[TODO]`, `[FOLLOW-UP]`, `[BLOCKED]`, `[WAITING]` in daily logs older than 3 days
- [ ] Milestones in MEMORY.md with no recent log activity
- [ ] Draft files in `drafts/active/` older than 24 hours → move to `drafts/expired/`

### Habits
- [ ] Check objective pillar auto-detection rules (see HABITS.md)
- [ ] After 17:00 CET: nudge for unchecked pillars

## Notification Thresholds

Only notify (macOS + Slack DM) when:
- Item is new since last heartbeat run (state diffing via `heartbeat-state.json`)
- Item requires attention within 24 hours
- A milestone is flagged as behind or blocked

Suppress:
- Repeated notifications for the same item (already in state)
- Items outside active hours

## Draft Management

1. Scan Gmail for threads matching drafting criteria in USER.md
2. For each qualifying thread: search `drafts/sent/` for voice-matching examples (top 3 similar)
3. Generate draft → save to `Memory/drafts/active/YYYY-MM-DD_email_<slug>.md`
4. Expire drafts older than 24h → move to `Memory/drafts/expired/`
5. When Dennis replies on Gmail: capture real reply text → save to `Memory/drafts/sent/`

## Actions Heartbeat Will Take Automatically (Assistant Level)

- Append entries to `Memory/daily/YYYY-MM-DD.md`
- Move files within `Memory/drafts/` (active → expired)
- Write draft files to `Memory/drafts/active/`
- Check objective habit pillars in `Memory/HABITS.md`
- Update `Memory/MEMORY.md` open loops section (via daily reflection)

## Actions Heartbeat Will NEVER Take

- Send any email, Slack, or Teams message
- Delete any file or record
- Write outside `Memory/`
- Access financial systems
- Post to social media
