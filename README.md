# Chronicle

### ▶ [**Open the live app → paradekrewe.github.io/Chronicle**](https://paradekrewe.github.io/Chronicle/)

*Nothing to install. Click the link above and use it right in your browser.*

---

**Convert corporate calendar exports into a clean personal archive.**

Chronicle is a fully browser-based tool for people leaving a job who want to keep their work calendar history as a personal diary. It takes Google Workspace `.ics` (or `.zip`) exports, strips out stale meeting junk, preserves the people you worked with, and splits the result into Google Calendar–ready import files.

No server. No upload. No account. Everything runs locally in your browser.
---
The problem it solves
When you leave a company, years of meetings, decisions, and collaborations disappear with your access. Google Workspace lets you export your calendar as an `.ics` file — but that file is full of noise:
Zoom, Meet, Teams, Webex, GoToMeeting dial-in instructions that expired years ago
Google's `~:~:~:~` conference metadata divider blocks
RSVP flags, METHOD:REQUEST invite artifacts, VALARM reminders
Attendee data buried in raw ICS properties instead of readable text
Files too large to import into a personal Google Calendar (1 MB / ~900 event limit per file)
Chronicle cleans all of that up and turns the export into something worth keeping.
---
Features
Accepts `.ics` files and Google Takeout `.zip` exports — no manual extraction needed
Strips meeting link clutter — Zoom, Google Meet, Microsoft Teams, Webex, GoToMeeting, BlueJeans, RingCentral, GoTo, dial-in blocks, Meeting ID / Passcode lines, Google's tilde divider signature blocks, and more
Preserves attendees cleanly — moves names and email addresses into the event description as readable text before removing raw ATTENDEE properties
Attendee cap — optionally skip attendee lists on large events (all-hands, town halls) above a threshold you set; the event still imports, just without the bulk
Strips invite metadata — removes METHOD:REQUEST, RSVP flags, and stale conferencing fields that would cause re-invite behavior
Removes alarms — cleans out VALARM reminders not needed in an archive
Cleanup report — shows original vs cleaned file size, percent reduction, events processed, attendees preserved, link blocks removed, and large events skipped
Event preview — expandable cards let you review cleaned content before downloading
Splits into importable chunks — stays under both Google's 1 MB file size limit and ~900 event limit per file, never splitting in the middle of an event
Guided import flow — step-by-step instructions walk you through each file one at a time with a progress bar, or download all at once if you prefer
---
How to use
Option 1 — Use the hosted app (easiest)
Just open **[paradekrewe.github.io/Chronicle](https://paradekrewe.github.io/Chronicle/)**. No download, no build step, no installation.
Option 2 — Run the file locally
Download `index.html` from this repository and open it in any modern browser. It works fully offline — no dependencies to install.
Option 3 — Host your own copy on GitHub Pages
Fork this repository
Go to Settings → Pages
Set source to `main` branch, `/ (root)`
Your Chronicle instance will be live at `https://yourusername.github.io/chronicle/`
---
Exporting your Google Workspace calendar
From Google Calendar (before losing access)
Go to calendar.google.com
Click the ⚙ gear icon → Settings
In the left sidebar click Import & export
Click Export — Google downloads a `.zip` file containing one `.ics` per calendar
Drop that `.zip` directly into Chronicle — no need to unzip
From Google Takeout (works after leaving, if Takeout access remains)
Go to takeout.google.com
Deselect all, then select Google Calendar
Export and download the `.zip`
Drop it into Chronicle
---
Importing into Google Calendar
After Chronicle generates your cleaned, split files:
Go to calendar.google.com
Consider creating a new calendar first: Other calendars → + → name it something like "Work Archive 2018–2025"
Click ⚙ gear icon → Settings → Import & export → Import
Select one file, choose the target calendar, click Import
Wait for the confirmation ("X events imported"), then repeat for each file
Chronicle's guided import mode walks you through this one file at a time with a checklist and progress bar.
---
What the cleaned description looks like
Before:
```
Quarterly planning sync

Join with Google Meet
https://meet.google.com/abc-defg-hij

-::~:~::~:~:~:~:~:~:~:~:~:~:~:~:~:~:~::~:~::-
Learn more about Meet at: https://support.google.com/a/users/answer/9282720
Please do not edit this section.
-::~:~::~:~:~:~:~:~:~:~:~:~:~:~:~:~:~::~:~::-
```
After:
```
Quarterly planning sync

--- Attendees ---
Required:
  - Jane Doe <jane@example.com>
  - John Smith <john@example.com>
Optional:
  - Alex Lee <alex@example.com>
Organizer:
  - Pat Rivera <pat@example.com>
-----------------
```
---
Privacy
Chronicle processes everything locally in your browser using the File API and JSZip. Your calendar data is never transmitted to any server, never stored, and never logged anywhere. You can run it offline after the page loads.
The only external resource loaded is JSZip from cdnjs.cloudflare.com, used to unpack `.zip` exports in-browser.
---
Technical notes
ICS parsing follows RFC 5545 including line-folding (continuation lines prefixed with whitespace), VTIMEZONE block preservation, and proper ATTENDEE parameter parsing (CN, ROLE, RSVP, PARTSTAT).
Chunking respects both of Google Calendar's import limits: 1 MB per file (with a 10 KB safety margin) and approximately 900 events per file (under Google's ~1,000 event soft cap). Chunks never split mid-event.
Date handling parses DTSTART/DTEND components directly from the ICS integer format (YYYYMMDDTHHMMSS) without passing through JavaScript's `Date` string constructor, which interprets date-only strings as UTC midnight and shifts the displayed date for users in negative UTC offset timezones.
Attendee roles — attendees with `ROLE=OPT-PARTICIPANT` are listed under Optional; all others are listed under Required. The ORGANIZER property is preserved separately.
---
Browser compatibility
Works in any modern browser (Chrome, Firefox, Safari, Edge). No Internet Explorer support. Tested on Chrome 120+ and Safari 17+.
---
License
MIT — do whatever you want with it. If you improve the meeting-link stripping patterns, a pull request would be welcome.
