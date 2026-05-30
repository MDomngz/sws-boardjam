# SWS Board Portal

A secure, mobile-responsive board dashboard for Susquehanna Waldorf School, hosted on GitHub Pages. All sensitive documents live in Google Drive; this site provides the portal, navigation, and snapshot content.

---

## Files

| File | Purpose |
|---|---|
| `index.html` | The portal itself — login screen + full dashboard |
| `board-data.json` | All content: agenda, calendar, news, documents |
| `BOARD-PORTAL-README.md` | This file |

---

## How to Deploy (GitHub Pages)

1. Create a **new private repository** (e.g., `sws-board-portal`) — separate from any other repos
2. Copy `index.html` and `board-data.json` into it
3. Go to **Settings → Pages**
4. Set Source to `Deploy from a branch` → `main` → `/ (root)`
5. GitHub will give you a URL like `https://yourusername.github.io/sws-board-portal/`
6. Share that URL with board members

> ⚠️ **Important:** GitHub Pages makes HTML and JSON publicly accessible by URL. The password gates the dashboard UI only — it is NOT a substitute for restricting documents to authorized Google accounts in Drive. Keep truly sensitive content in Drive with proper sharing permissions.

---

## Changing the Password

Open `index.html` and find this line near the top of the `<script>` section:

```javascript
const BOARD_PASSWORD = 'waldorf2025'; // ← CHANGE THIS
```

Replace `waldorf2025` with your chosen password. Commit and push. The change takes effect immediately.

**Password hygiene:**
- Change the password whenever a board member leaves
- Notify all current board members of the new password
- Avoid obvious choices (school name, year, etc.)

---

## Updating Content

**All content lives in `board-data.json`.** Edit that file and push to GitHub — the dashboard polls for changes every 5 minutes and updates automatically.

### Fields you'll update most often

#### `meetingMonth`
The label shown in the nav bar.
```json
"meetingMonth": "September 2025"
```

#### `chairMessage`
Optional message from the Board Chair on the Overview tab. Delete the field or set to `""` to hide it.

#### `agenda`
Update before each meeting. Each item can have:
- `title` — required
- `type` — `"action"`, `"info"`, or `"discussion"` (controls badge color)
- `duration` — e.g., `"15 min"`
- `description` — optional detail
- `driveUrl` — link to supporting document in Drive

#### `calendar`
Add events for the full year at the start of each school year. Dates must be `YYYY-MM-DD` format.

#### `news`
Replace with current month's 3–5 items. Each needs:
- `emoji`, `title`, `category`, `date`, `summary`
- `driveUrl` — link to full document in Drive

#### `documents`
Organized by category. Add/remove files as needed. Each file needs a `title` and `driveUrl`.

---

## Getting Google Drive Links

1. Right-click any file/folder in Google Drive
2. Select **Share → Copy link**
3. Set access appropriately (board emails only for sensitive docs)
4. Paste the URL into `board-data.json` as the `driveUrl` value

---

## Auto-Refresh

The dashboard fetches `board-data.json` every **5 minutes**. When you push an update, all open dashboards update automatically within 5 minutes.

Change the interval in `index.html`:
```javascript
const REFRESH_INTERVAL = 5 * 60 * 1000; // 5 minutes
```

---

## Security Notes

| What's protected | How |
|---|---|
| Dashboard UI | Shared password (session-based, resets on browser close) |
| Actual documents | Google Drive sharing permissions |
| Site URL | Share only with board members |

The password is client-side — a technical user could find it in HTML source. For typical school governance content, this is generally acceptable. For stronger security, upgrade to Google OAuth (requires developer setup).

---

## Offboarding Checklist

When a board member leaves:
- [ ] Change the portal password in `index.html` and push
- [ ] Notify remaining board members of the new password
- [ ] Remove their Google account from all Drive folder sharing
- [ ] Update the Board Member Directory in Drive

---

## Contact

Questions? Contact the board secretary at board@susquehannawaldorf.org
