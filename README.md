# Canvas-Due-tracker
# Canvas Due Tracker

A small Chrome extension that pulls everything due from your Canvas LMS into one popup, organised by subject. Per-course toggles let you choose where each course pulls from. No API token needed — it uses your existing Canvas browser session.

Matte-black UI with a single electric-lime accent. Manifest V3, vanilla JS, no dependencies.

---

## Features

- One collapsible card per active Canvas course
- Per-course source toggles, independently remembered:
  - **Announcements** — scans `/courses/{id}/discussion_topics?only_announcements=true` and keeps posts that look like work (mentions tests, handouts, PDFs, deadlines, linked assignments)
  - **To-Do** — pulls `/users/self/todo` + `/planner/items` and filters to that course (this is what Canvas's own "To Do" dashboard widget reads)
  - **Modules** — walks `/courses/{id}/modules?include[]=items&include[]=content_details`, keeping all work-type items (Assignment / Quiz / Discussion) plus dated Pages/Files
  - **Get All** — flips all three on at once
- Aggregated, deduplicated, sorted-by-due tasks per subject
- **Auto-tick** assignments Canvas marks `submitted` / `graded` / `pending_review`
- Stale-tick cleanup: anything Canvas still lists on `/todo` is guaranteed visible
- Check off tasks → fade out → persisted hidden across re-opens
- Hide whole courses with × ; restore them from Settings
- Background refresh every 30 minutes (and auto-refresh on popup open if cache is stale)
- "Show completed" toggle, global "Reset completed" button

## Install

1. **Download**: click the green **Code** button (top of this page) → **Download ZIP** → unzip.
2. Open Chrome → `chrome://extensions`
3. Turn on **Developer mode** (top-right toggle).
4. Click **Load unpacked** → pick the unzipped folder.
5. Click the puzzle-piece icon in the toolbar and pin **Canvas Due Tracker**.

## First-time setup

1. Click the extension icon → click the **gear** icon (top-right of popup).
2. Enter your Canvas hostname — e.g. `canvas.instructure.com`. Just the host, no `https://`, no trailing slash. Copy from your address bar when logged in.
3. Click **Save**. Chrome may ask permission for the host — click **Allow**.
4. You'll see all your active courses as cards. Click one to expand and toggle which sources to pull from.

You must be **logged into Canvas in this Chrome profile** for the extension to fetch data. If you see "Not signed in," open Canvas in a tab, log in, and hit the refresh button.

## Daily use

Just click the icon. New work appears within 30 minutes of being posted. Submit something in Canvas → next popup open auto-ticks it.

If a course is noisy (old lesson pages, etc.), either disable its Modules pill or click the × on its card to hide it. Hidden courses live in Settings, restorable any time.
