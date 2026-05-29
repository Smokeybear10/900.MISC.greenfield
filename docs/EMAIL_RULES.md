# Email organization rules

Source of truth for how Claude (and future Claude sessions) should organize my Gmail and Outlook.

## Gmail — `thomasou@sas.upenn.edu`

### Label structure

```
Jobs/
  Active        — interviews, OAs, onboarding, networking, anything requiring action
  Applications  — passive auto-replies, rejections, "thanks for applying"
  Recruiting    — Handshake/Simplify/SWElist/talent communities (ARCHIVED)
Penn            — Penn-specific events worth keeping in inbox
Newsletters     — TLDR/WSJ/NYT/WaPo/Bloomberg/IBD/Adventis (ARCHIVED)
```

### Routing rules for new emails

| Pattern | Label | Action |
|---|---|---|
| Interview invite, R1/R2/OA, recruiter cold-outreach, real opportunity, hackathon credits, workshops | `Jobs/Active` | **Keep in inbox** |
| "Thanks for applying" + rejection auto-replies | `Jobs/Applications` | Can archive |
| Handshake matches, Simplify digests, SWElist daily, talent communities | `Jobs/Recruiting` | **Archive** |
| TLDR (×5), WSJ daily, NYT Morning + opinion, WaPo daily, Bloomberg, IBD, Adventis, emailbenefithub, Apollo, Tech Week | `Newsletters` | **Archive** |
| DP, Penn Today, SAS Connect, Penn Career Services Weekly | `Newsletters` + `Penn` | **Archive** |
| Penn Athletics events, 12twenty workshops, real Penn opportunities | `Penn` only | Keep in inbox |

### Calendar integration

Interview/application deadlines should also create a Google Calendar event:
- All-day event on deadline date (or specific time if known)
- Reminders: popup @ 24h, popup @ 1h, email @ 48h
- Event color: red (`colorId: 11`) for deadlines

### Why this scheme

Binary split: **"stuff to look at vs passive bs."** `Jobs/Active` is the single bucket requiring action. Everything else is browsable but not urgent. ~25 emails/day, ~80% noise — without filtering the inbox is unusable.

---

## Outlook — Amazon work (`tommyou@amazon.com`)

### Folder structure

```
Work/
  Code Reviews    — CR-XXXXXXX notifications from code.amazon.com
  SIM             — Issue tracker updates
  MCM             — Change management notifications
  Pipelines       — Build/deploy alerts
  Slack           — Slack notifications
  DLs             — Distribution list emails
  Wiki/Quip       — Doc edits
```

### Outlook rule patterns

| Filter | Action |
|---|---|
| Subject contains `CR-` OR from `code.amazon.com`/`codereview` | Move to `Work/Code Reviews`, mark as read |
| Subject contains `SIM-` or `[SIM]` OR from `sim-noreply` | Move to `Work/SIM` |
| Subject contains `MCM-` or `[MCM]` | Move to `Work/MCM` |
| From `pipelines.amazon.com` OR subject contains `Pipeline`/`Build failed`/`Build succeeded` | Move to `Work/Pipelines` |
| From `slack.com` OR `notifications@slack` | Move to `Work/Slack` |

---

## Known MCP limitations

- Anthropic Gmail MCP **cannot delete or rename labels** — user does that in Gmail UI manually
- Anthropic Gmail MCP **cannot create Gmail filters** — user creates filters manually if they want auto-categorization on new emails
- Gmail MCP is **per-account** — switching accounts requires `/mcp` disconnect/reconnect
- Outlook has **no MCP integration** — can only write rules for user to apply manually

## Future automation options

- **Gmail filters** (free, instant, runs on Google's side) — best for noise sender filtering
- **`/schedule`** Claude routine (cron-based remote agent, separate API billing) — best for nuanced categorization that needs judgment
- **Hybrid** — Gmail filters handle obvious noise, scheduled Claude handles tricky stuff
