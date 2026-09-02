# Agent Home — D365 Custom Web Resource

![Agent Home Screenshot](screeshot.png)

A unified agent dashboard for Dynamics 365 Customer Service, providing real-time presence, queue management, performance metrics, and schedule visualization in a single web resource.

---

## Features

### My Presence
- Set and display your current presence status (Available, Busy, Do Not Disturb, Away, Offline)
- Presence is resolved from the org's own `msdyn_presence` records, so **custom presences** (for example "Busy - After Conversation Work") show their real name and correct colour
- Polling interval: 10 seconds (throttle-safe)

### Recent Conversations
- Shows the Omnichannel conversations the signed-in agent actually handled
- Filter bubbles for the last **24h, 12h, 6h, 1h, 30m and 15m**
- Each row shows the channel (voice, chat, email, SMS, social), workstream, customer, handle time, sentiment and live/wrap-up/closed status
- Click a row to open the conversation record
- Channel icons are resolved from the org's own workstream channel option set, so custom channels are supported

### My Queues
- View all queues you are assigned to
- See live agent counts and queue item counts per queue

### Online Agents
- See which agents are currently online across your queues
- Shows presence indicator and queue membership per agent

### My Metrics
- CSAT trend, handle time, first-contact resolution, and other KPIs
- Filtered to your activities (no cross-agent data leakage)

### My Schedule (WFM)
- Visual timeline of your Workforce Management schedule for the current day
- Horizontal bar chart spanning your configured working hours
- **Square-corner bars** — no rounded edges
- **No text labels on bars** — clean, uncluttered view
- **Color legend** always visible below the timeline

#### Standard Schedule Type Colors

| Type     | Color   | Hex       |
|----------|---------|-----------|
| Shift    | Blue    | `#2563eb` |
| Break    | Amber   | `#f59e0b` |
| Lunch    | Green   | `#16a34a` |
| Training | Purple  | `#7c3aed` |
| Meeting  | Teal    | `#0891b2` |
| Time Off | Red     | `#ef4444` |

#### Custom / Unknown Schedule Types
If your organization uses custom WFM activity types not in the standard list above, the dashboard will:
- **Automatically detect** any schedule type not matching a known keyword
- **Assign a unique color** from a 12-color palette using a deterministic hash of the type name — the same custom type always gets the same color, across page reloads and re-renders
- **Append a legend entry** dynamically below the standard types, showing the actual type name and its assigned color
- Support **unlimited custom types** — the hash-based system scales with however many types your org creates

Custom type palette (12 colors, cycled by hash): pink, orange, sky-blue, indigo, fuchsia, rose, amber-dark, dark-green, dark-cyan, deep-violet, brown, royal-blue.

---

### Languages (Automatic Localization)
- **Automatically detects** the signed-in user's Dynamics 365 display language from their user settings (LCID) — no prompt, no manual switch
- Renders **all** UI text — greetings, section titles, metrics, queues, schedule, tasks, cases, buttons, empty states, and modals — in the detected language
- **Locale-aware** date, time, and number formatting
- Supported languages: English, French, German, Spanish, Brazilian Portuguese, Italian, Dutch, Japanese, Simplified Chinese, Korean, Russian
- Any unsupported language **falls back to English** so the UI never breaks

---

## Requirements

- Dynamics 365 Customer Service (with Omnichannel or equivalent)
- WFM / scheduling configured (for My Schedule section)
- Web resource added to a D365 model-driven app page

---

## Deployment

Import the prebuilt **`solution.zip`** (unmanaged, version 2.9.1.0) included in this repository:

1. In D365 go to **Settings → Solutions → Import** (or **make.powerapps.com → Solutions → Import solution**)
2. Select `solution.zip` and complete the import
3. Publish all customizations
4. Add the `maulabs_agent_home` web resource to your model-driven app page

Or use the Power Platform CLI:
```bash
pac solution import --path solution.zip --publish-changes --force-overwrite
```

> The solution imports as a new version (2.8.0.0), so importing over an existing Agent Home install upgrades it in place.

---

## Version History

| Version  | Date       | Key Changes |
|----------|------------|-------------|
| v2.2.0.0 | 2025-04    | Initial fixes: `window.top` removal, `console.log` removal, `'use strict'`, XSS fixes, presence poll 10 s |
| v2.3.0.0 | 2025-04    | ZIP packaging fix: forward-slash paths in archive (D365 web resource overwrite reliability) |
| v2.4.0.0 | 2025-04    | `queuemembership` filter fix: `systemuserid eq` (intersect entity) instead of `_systemuserid_value eq`; WFM schedule filter fix |
| v2.5.0.0 | 2025-04    | Schedule UI overhaul: square-corner bars, solid colors (no gradients), no text on bars, full 7-type static color legend |
| v2.6.0.0 | 2025-05    | Dynamic color system: custom/unknown schedule types auto-assigned unique colors via deterministic hash; dynamic legend shows all types including custom; `type-default` gray fallback eliminated |
| v2.7.0.0 | 2025-05    | UI: My Queues section gets white card background with border, shadow, and aligned padding |
| v2.8.0.0 | 2026-06    | **Automatic language detection (i18n):** the dashboard detects the signed-in user's Dynamics 365 display language (LCID) and renders **all** UI text in that language with no prompt. Ships with 11 languages — English, French, German, Spanish, Brazilian Portuguese, Italian, Dutch, Japanese, Simplified Chinese, Korean, Russian — plus locale-aware date/number formatting. Unsupported languages fall back to English. |

---

## Publisher

**Maulabs** — prefix `maulabs`
