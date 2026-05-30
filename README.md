# Susquehanna Waldorf School — Board Portal

A secure, mobile-responsive board dashboard hosted on GitHub Pages. The portal provides a central hub for board governance, fundraising, and wayfinding. All sensitive documents live in Google Drive; this site displays summaries and links.

---

## What's Included

| Section | What it does |
|---|---|
| **Overview** | At-a-glance summary — next meeting, open actions, campaign progress, recent news |
| **Announcement Banner** | Pinned notice at the top of every page for urgent updates |
| **Agenda** | Full meeting agenda with item types, durations, and Drive links |
| **Action Items** | Filterable tracker of commitments from recent meetings |
| **Development** | Fundraising thermometer, board giving participation, prospect pipeline, grant deadlines |
| **Calendar** | Full-year meeting and event schedule |
| **News & Reports** | Monthly news summaries linking out to Drive |
| **Decision Log** | Searchable history of all board votes and resolutions |
| **Our Board** | Member profiles with role, committee, term end date, and volunteer hours |
| **Documents** | Organized links to all governance, finance, and policy documents in Drive |

---

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire portal — login screen and dashboard |
| `board-data.json` | All content that editors update each month |
| `README.md` | This file |

---

## Deployment

### Step 1 — Create a dedicated GitHub repository

Create a **new, separate** GitHub repository (e.g., `sws-board-portal`). Do not mix this with other school repos. If possible, create it under a school-owned GitHub organization account rather than a personal one.

### Step 2 — Add the files

Copy `index.html` and `board-data.json` into the repo root.

### Step 3 — Enable GitHub Pages

1. Go to **Settings → Pages**
2. Under Source, select **Deploy from a branch**
3. Choose **main** branch, **/ (root)** folder
4. Click Save

GitHub will provide a URL like `https://your-org.github.io/sws-board-portal/`. This typically goes live within a minute or two.

### Step 4 — Change the password

Open `index.html` and find this line near the top of the `<script>` block:

```javascript
const BOARD_PASSWORD = 'waldorf2025'; // ← CHANGE THIS
```

Replace `waldorf2025` with your chosen password. Commit and push. The change is live immediately.

### Step 5 — Share

Send the GitHub Pages URL and password to all board members. That's it.

---

## Updating Content Each Month

**All portal content lives in `board-data.json`.** Edit the file, commit, and push. The dashboard polls for changes every 5 minutes — open portals update automatically with no manual refresh needed.

### Announcement Banner

Shows a dismissible orange bar at the top of every page. Set `text` to display it; set to `""` or remove the field to hide it.

```json
"announcement": {
  "label": "Meeting Rescheduled:",
  "text": "The June meeting has moved to June 17 at 6:30 PM.",
  "url": ""
}
```

### Chair Message

Optional message on the Overview tab. Remove the field or set to `""` to hide.

### Agenda

Update before each meeting. Item `type` controls the badge color:
- `"action"` — clay/orange (voting items)
- `"info"` — green (reports, updates)
- `"discussion"` — stone/tan (discussion items)

```json
"agenda": {
  "date": "Tuesday, September 9, 2025 · 6:30 PM",
  "location": "SWS Main Building, Room 12",
  "driveUrl": "https://drive.google.com/...",
  "items": [
    {
      "title": "Call to Order",
      "type": "info",
      "duration": "5 min",
      "description": "Optional detail text.",
      "driveUrl": "https://drive.google.com/..."
    }
  ]
}
```

### Action Items

Add items after each meeting. Update `status` as work progresses.

Valid `status` values: `"open"` · `"inprogress"` · `"done"`

```json
{
  "title": "Research HVAC vendors for Building B",
  "owner": "Marcus Webb",
  "status": "inprogress",
  "dueDate": "June 17, 2025",
  "fromMeeting": "May 13, 2025",
  "notes": "Two quotes received."
}
```

### Fundraising / Development

Update after each campaign report. Key fields:

```json
"campaign": {
  "name": "2024–25 Annual Fund",
  "goal": 120000,
  "raised": 87500,
  "boardMembersGiven": 7,
  "boardMembersTotal": 9,
  "deadline": "June 30"
}
```

The thermometer and board participation bar animate automatically based on these numbers.

Add **prospects** with `name`, `stage`, `askAmount`, and `boardLead`. Valid stages: `Identification` · `Cultivation` · `Solicitation` · `Stewardship`

Add **deadlines** with a `date` in `YYYY-MM-DD` format. Deadlines within 14 days automatically turn red with a countdown badge.

### Decision Log

Add one entry after each meeting for every motion voted on. This is your running record — do not skip entries.

```json
{
  "date": "June 17, 2025",
  "title": "Approved 2025–26 budget",
  "category": "Finance",
  "description": "Board approved the operating budget as presented.",
  "vote": "9–0",
  "unanimous": true,
  "driveUrl": "https://drive.google.com/..."
}
```

Valid `category` values for color coding: `Finance` · `Governance` · `Facilities` · `Personnel`

### Board Member Profiles

Update at the start of each year or when membership changes. Volunteer hours should be updated monthly or quarterly.

```json
{
  "name": "Eleanor Voss",
  "role": "Board Chair",
  "email": "evoss@susquehannawaldorf.org",
  "committee": "Executive, Development",
  "termEnd": "June 2026",
  "volunteerHours": [
    { "activity": "Committee meetings", "hours": 24 },
    { "activity": "Donor events", "hours": 12 }
  ]
}
```

### Calendar

Add all known dates at the start of each school year. Dates must be in `YYYY-MM-DD` format. Past events fade out automatically.

### News & Reports

Replace with the current month's items before each meeting (typically 3–5). Each item links to a document in Drive.

### Documents

Organized by category. Update Drive URLs whenever documents are revised. Structure:

```json
{
  "category": "Finance",
  "files": [
    {
      "emoji": "📊",
      "title": "Monthly Financial Reports",
      "description": "Current and past monthly financials",
      "driveUrl": "https://drive.google.com/..."
    }
  ]
}
```

---

## Google Drive Links

To get a shareable link for any file or folder:

1. Right-click the item in Google Drive
2. Select **Share → Copy link**
3. Set access to specific board member email addresses for sensitive documents
4. Paste the URL into `board-data.json` as the `driveUrl` value

> **Important:** Drive links on mobile open in the Drive app rather than a browser. Some members may find this unexpected — it is normal behavior.

---

## Changing the Password

Edit `index.html`, change `BOARD_PASSWORD`, commit, and push. The new password is live immediately.

**When to change the password:**
- Whenever a board member leaves or their term ends
- If you suspect the password has been shared outside the board

Notify all current board members of the new password after changing it.

---

## Auto-Refresh

The dashboard fetches `board-data.json` every 5 minutes while open. No manual refresh needed after you push an update.

To change the interval, edit this line in `index.html`:
```javascript
const REFRESH_INTERVAL = 5 * 60 * 1000; // 5 minutes
```

---

## Security Notes

The password in `index.html` is client-side — it controls access to the dashboard UI, not the underlying files. A technically motivated person could find it in the page source.

**Your real security layer is Google Drive.** Restrict sensitive documents to specific board member email addresses in Drive sharing settings. That way, even if someone gets the portal URL and password, they cannot open the actual documents.

| Layer | Protection |
|---|---|
| Portal URL | Share only with board members |
| Dashboard password | Blocks casual access; resets on browser close |
| Drive permissions | Restricts document access to authorized accounts |

---

## Offboarding a Board Member

When a member's term ends or they resign:

- [ ] Change the portal password in `index.html` and push
- [ ] Notify remaining board members of the new password
- [ ] Remove their Google account from all Drive folder sharing
- [ ] Update their entry in `boardMembers` in `board-data.json`
- [ ] Update the Board Member Directory document in Drive

---

## Recommended Monthly Workflow

**Before each meeting (secretary or designated editor):**
1. Update `agenda.items` with the current meeting agenda
2. Add any new `news` items and remove stale ones
3. Update `fundraising.campaign` numbers from the Development Director
4. Update `actionItems` — mark completed items as `"done"`, add new items from last month
5. Set `announcement.text` if there is anything urgent to flag
6. Commit and push — the portal updates within 5 minutes

**After each meeting:**
1. Add new action items to `actionItems`
2. Add each voted motion to `decisions`
3. Clear or update the `announcement` if no longer relevant
4. Update `fundraising.prospects` if any pipeline changes occurred

---

## Contact

Questions about the portal? Contact the board secretary at board@susquehannawaldorf.org
