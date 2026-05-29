# OnTrack — Web Application Build Specification

**Version:** 1.0  
**Date:** 2026-05-29  
**For:** An AI agent or developer building the OnTrack web app from scratch.

---

## 1. What You Are Building

OnTrack is a smart study planner for high schoolers. It connects to Google Classroom, pulls a student's assignments automatically, and generates a prioritized daily plan: which assignment to work on tonight, in what order, and for how long. When something takes longer than expected, the student can tell the AI assistant and the plan adjusts in real time.

The core value proposition is **active prioritization**, not passive deadline tracking. Every other tool tells students what is due. OnTrack tells them what to work on *right now* and in what order.

**Positioning statement (exact wording to use in product copy):**
> For teenagers juggling academics and extracurricular obligations, who struggle to balance their academic workload with everything else competing for their time, OnTrack is a smart study planner that turns a chaotic schedule into a clear plan, reducing the stress of juggling academics and outside commitments. Unlike trying to remember every deadline in your head, setting it as an alarm, or basic planner apps, our product tells you how to use your time effectively and is built around the reality of a teenager's packed schedule.

---

## 2. Technical Stack

**Requirements (agent must choose specific technologies):**
- Web application — no mobile app in v1
- Google OAuth 2.0 for authentication (Google sign-in only — no email/password accounts)
- Google Classroom API for pulling assignment data
- An AI/LLM backend for the Assistant screen (chat interface that interprets natural language updates and adjusts the plan)
- No server-side storage of student data in v1 — all assignment data is pulled live from Google Classroom on each session to minimize FERPA/COPPA exposure. User preferences (availability hours, notification settings) are stored locally (e.g., localStorage) or in a minimal backend keyed to the Google user ID with no educational record data.

**Suggested stack (agent may substitute):**
- Frontend: React or Next.js
- Styling: Tailwind CSS
- Auth: NextAuth.js or Google Identity Services
- Google Classroom: Google Classroom API v1 (REST)
- AI assistant: Anthropic Claude API (model: `claude-sonnet-4-6`) or OpenAI GPT-4o
- Deployment: Vercel or similar

---

## 3. Screen Inventory

| # | Screen | Route | Purpose |
|---|--------|-------|---------|
| 1 | Login | `/` | Sign in with Google, trigger Classroom sync |
| 2 | Calendar | `/app` | Main screen — timeline of all assignments |
| 3 | Daily Plan | Panel within `/app`, also `/app/daily-plan` | Today's prioritized work list |
| 4 | Classes | `/app/classes` | All assignments organized by class folder |
| 5 | Assignment Details | `/app/assignment/:id` | Single assignment view + editing |
| 6 | Assistant | `/app/assistant` | AI chat — explains and adjusts the plan |
| 7 | Settings | `/app/settings` | Notifications, availability hours, accessibility |

---

## 4. Screen Specifications

### Screen 1 — Login (`/`)

**Layout:** Centered card on a light gray background.

**Elements:**
- OnTrack logo/wordmark (large, bold)
- Tagline: "Your smart study planner"
- "Sign in with Google" button (standard Google OAuth button styling with Google icon)
- Annotation text below button: "First sign-in pulls your assignments from Google Classroom automatically"

**Behavior:**
1. User clicks "Sign in with Google" → Google OAuth flow
2. On successful auth:
   - First-time user: system triggers Google Classroom sync, then redirects to `/app` with the Daily Plan panel open
   - Returning user: redirect to `/app` with the Daily Plan panel open

**Error state:**
- If OAuth fails: show inline error message, keep button active

---

### Screen 2 — Calendar (`/app`) — Main/Home Screen

**Layout:** Three-panel layout:
- Left: fixed sidebar (200px wide)
- Center: main calendar area (flex: 1)
- Right: Daily Plan panel (264px wide, visible by default)

**Sidebar (always visible on all `/app/*` routes):**
- OnTrack logo at top
- Navigation items: Calendar, Classes, Assistant, Daily Plan
- Settings link at the bottom (visually separated)
- Active item has a left border indicator and bold weight

**Calendar main area:**

Top bar:
- Current date label (e.g., "May 26, 2026")
- View toggle buttons: Day | Week | Month (only one active at a time)
- "+ Add assignment" button (dashed border style, right side)

Calendar grid (weekly view is the default):
- Column headers: one column per day, the current day highlighted
- First column is a time label column (3pm, 5pm, 7pm, 9pm, etc.)
- A "Due" row at the top of the grid showing assignment chips on the day they are due
- Time rows below showing scheduled study session chips placed at their planned time slot
- Each chip shows: assignment name, estimated duration (smaller text)
- Clicking a chip navigates to Assignment Details

**Daily Plan panel (right side, always open on `/app`):**
- Header: "Daily Plan" + current date below it in smaller text
- Scrollable list of today's assignments, each card shows:
  - Class name (small, uppercase, muted)
  - Assignment name (bold)
  - Due date (e.g., "Due tomorrow") + estimated time for tonight (e.g., "90 min")
- Clicking an assignment card opens a status popup (see below)
- Fixed at the bottom of the panel: a single-line chat input with a send button (→ arrow); submitting navigates to the Assistant screen with the message pre-filled

**Status popup (appears on top of the Daily Plan when a card is clicked):**
- Title: "Update status"
- Buttons:
  - Done early
  - Need a break
  - Taking longer → tell assistant (navigates to Assistant with context)
  - Finished
  - Incomplete
- Clicking outside the popup closes it

**Add assignment overlay (triggered by "+ Add assignment"):**
- Modal overlay (dark background, centered card)
- Form fields:
  - Class (dropdown — populated from synced classes)
  - Assignment name (text input, required)
  - Topic (text input, optional)
  - Due date (date picker, required)
  - Estimated time in minutes (number input, required)
- Actions: Cancel | Add assignment
- On submit: assignment added to system, overlay closes, Calendar and Daily Plan update

---

### Screen 3 — Daily Plan (standalone, `/app/daily-plan`)

**Layout:** Full main area (no right panel — this is the panel, now full-width).

**Elements:**
- Screen title: "Daily Plan" + today's date
- Same prioritized list as the panel version
- Same status popup behavior

This screen is reached via the "Daily Plan" link in the sidebar. On screens narrower than the full layout, this replaces the panel.

---

### Screen 4 — Classes (`/app/classes`)

**Layout:** Full main area (no right panel).

**Elements:**
- Screen title: "Classes"
- List of collapsible class folders, one per class (pulled from Google Classroom)
- Each folder header shows: class name + chevron (▶ collapsed, ▼ expanded)
- Clicking the header expands/collapses the folder
- Expanded folder shows a table with header row: Assignment | Due | Est. time | Status
- Each assignment row: assignment name, due date, estimated time, status badge
- Status badges: Upcoming | In progress | Finished | Incomplete
- Clicking an assignment row navigates to Assignment Details

---

### Screen 5 — Assignment Details (`/app/assignment/:id`)

**Layout:** Full main area, max-width 580px, scrollable.

**Elements:**
- "← Back to Classes" link at top
- Assignment title (large, bold)
- Class name + sync source (e.g., "Biology · Synced from Google Classroom")

Detail fields grid (2 columns):
- Due date (read-only)
- Status (read-only, reflects current state)
- Estimated time (editable text input — default pulled from Classroom if available, otherwise blank; user can set/override)
- Topic (read-only, pulled from Classroom)

Toggle row:
- Label: "Break into daily chunks"
- Description: "OnTrack splits this across multiple sessions"
- Toggle switch (on/off)

When chunking is ON, a "Planned sessions" preview box appears below showing:
- Each planned session: day/date on the left, duration on the right
- A note: "OnTrack will reschedule if a session is reported incomplete."

Status update section:
- Label: "Update status"
- Buttons in a row: Done early | Taking longer | Finished | Incomplete

**Behavior:**
- Editing estimated time → triggers Daily Plan recalculation
- Toggling chunking → triggers Daily Plan recalculation
- Clicking any status button → updates the assignment status; if "Taking longer" or "Incomplete", triggers Daily Plan recalculation

---

### Screen 6 — Assistant (`/app/assistant`)

**Layout:** Full-height chat interface.
- Upper area (flex: 1, scrollable): message thread
- Bottom: fixed chat input bar

**Message thread:**
- Each message has a sender label above it ("OnTrack" or "You")
- OnTrack messages: light gray background bubble, left-aligned
- User messages: medium gray background bubble, right-aligned
- Messages use plain language — no markdown formatting in the bubbles

**On first open (when no conversation exists):**
The AI should generate an opening message that explains today's plan in plain language, e.g.:
> "Here's your plan for tonight:
> 1. **Biology Lab Report** — 90 min (due tomorrow — top priority)
> 2. **Algebra HW 9** — 45 min (due Wed)
> 3. **History Essay chunk 1** — 45 min (due Thu)
>
> That's about 3 hrs total. Let me know if anything changes."

**On receiving a user message:**
The AI interprets natural language input about the student's situation (running late, an assignment taking longer, finishing early, feeling overwhelmed) and:
1. Acknowledges what the student said
2. States what it is changing in the plan
3. Gives the updated plan in plain language
4. The system updates the Daily Plan to reflect the change

**Chat bar:**
- Single text input: placeholder "Tell OnTrack what's happening..."
- Send button

---

### Screen 7 — Settings (`/app/settings`)

**Layout:** Full main area, max-width 520px.

**Sections:**

**Notifications:**
- Study reminder: dropdown (30 min before | 1 hr before | At start time | Off)
- Deadline reminders: toggle (on/off)

**Availability hours:**
- "I'm usually free after": time picker (default: 4:00 PM)
- "I stop working by": time picker (default: 10:00 PM)

**Accessibility:**
- High contrast mode: toggle
- Color-blind friendly display: toggle
- Text size: dropdown (Default | Large | Extra large)

**Google account:**
- Shows the connected email address
- "Disconnect" button — on click, confirms with the user, then disconnects and redirects to Login

**Behavior:** Every change saves immediately. Availability hours changes trigger a Daily Plan recalculation.

---

## 5. Prioritization Algorithm

The Daily Plan ordering must be computed by the system, not shown arbitrarily. The agent must implement this logic:

**Inputs per assignment:**
- Due date
- Estimated total time (minutes)
- Chunking on/off
- Student's availability window (start time, end time from Settings)
- Current time
- Subject type (cumulative vs. standalone — cumulative subjects like math, biology need to be done earlier because later topics depend on earlier understanding)

**Ordering rules (in priority order):**
1. Assignments due soonest come first
2. Among same-due-date assignments: cumulative/sequential subjects (math, science, foreign language) before standalone subjects (English reading responses, history essays)
3. Hardest/highest cognitive load first in the session (when the student is freshest)
4. Easiest/lowest-stakes tasks last (can be done when tired)

**Time allocation:**
- System uses the availability window to estimate how many minutes are available tonight
- Assignments are stacked in priority order until the window is full
- If an assignment is chunked, only tonight's chunk is scheduled; remaining chunks go to future days
- If an assignment is marked "taking longer," the system drops the lowest-priority item from tonight and reschedules it to the next available slot

**Failure mode:**
- If there is not enough time before a deadline to fit the estimated work, warn the student: "Not enough time before the deadline. Adjust your estimated time or availability hours in Settings."

---

## 6. Google Classroom Integration

**Scope of data pulled:**
- List of courses (classes) the student is enrolled in
- List of assignments per course with: name, due date, description/topic (if available), submission status

**OAuth scopes needed:**
- `https://www.googleapis.com/auth/classroom.courses.readonly`
- `https://www.googleapis.com/auth/classroom.coursework.me.readonly`
- `https://www.googleapis.com/auth/classroom.student-submissions.me.readonly`

**Sync behavior:**
- Sync triggers on login
- Optionally: re-sync button in Settings or automatic re-sync interval (every 30 min in background)
- If sync fails, show an error banner on the Calendar: "Could not sync assignments from Google Classroom. [Retry]"
- The system must never prevent the student from using OnTrack if sync fails — allow manual assignment entry as fallback

**Data handling:**
- No Google Classroom data is written to a database
- Data lives in application state (React state / session) for the duration of the session
- The only server-side persistence: user preferences (availability hours, notification settings) stored by Google user ID — no assignment names, due dates, or class names stored server-side

---

## 7. AI Assistant Integration

The Assistant uses an LLM (Claude or GPT-4) to:
1. Generate the opening daily plan summary in natural language
2. Interpret free-text updates from the student
3. Decide how to adjust the plan
4. Return the new plan in natural language

**System prompt guidance (to be passed to the LLM):**

```
You are OnTrack's assistant, a smart study planner for high school students. 
You speak in plain, direct language — no bullet-point overload, no jargon.
You always know the student's current assignment list and availability window.
When the student tells you something changed (took longer, starting late, finished early), 
you acknowledge it briefly and give them an updated prioritized plan.
Keep your responses short. Never lecture. Never be patronizing.
Always end with "Let me know if anything changes."
```

**Context to inject per request:**
- Current date and time
- Student's availability window (from Settings)
- Full list of today's assignments with due dates and estimated times
- Any previously reported status updates in this session

---

## 8. Notification System

Web push notifications (or browser notifications via the Notifications API):
- Study reminder: fires X minutes before the student's availability start time (configurable in Settings)
- Deadline reminder: fires 24 hours before an assignment is due (if the assignment is not yet marked Finished)

For v1, browser notifications are acceptable. Native push notifications require a service worker.

---

## 9. Design System

**Color palette (grayscale-first, accessible):**
- Background: `#f0f0f0` (page), `#ffffff` (cards/panels)
- Sidebar background: `#e8e8e8`
- Borders: `#cccccc` (primary), `#eeeeee` (subtle)
- Text: `#222222` (primary), `#444444` (secondary), `#888888` (muted), `#aaaaaa` (placeholder)
- Active nav indicator: `#555555`
- Primary button: `#555555` background, `#ffffff` text
- Assignment chips on calendar: `#e0e0e0` background, `#999999` left border accent

**Typography:**
- Font: system font stack (`-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`)
- Base size: 14px
- Screen titles: 15px, weight 600
- Assignment names in plan: 13px, weight 600
- Class labels: 10px, uppercase, letter-spacing 0.5px, muted color

**Accessibility requirements:**
- WCAG AA contrast minimum on all text
- High contrast mode toggle: increase border weights and darken text colors
- Color-blind friendly mode: avoid using red/green alone to communicate status; use labels + icons
- Text size setting affects base font size globally (Default: 14px, Large: 16px, Extra large: 18px)
- All interactive elements keyboard-navigable
- Screen reader: semantic HTML (`<nav>`, `<main>`, `<button>`, `aria-label` on icon-only buttons)

**Interaction patterns:**
- Folder expand/collapse: smooth height transition, chevron rotates
- Overlays/modals: dark semi-transparent backdrop, centered card, click outside to close
- Status popup: appears near the clicked item (not centered), closes on outside click
- All state changes that affect the plan (status updates, time edits, chunking toggles) should update the Daily Plan immediately without a page reload

---

## 10. Wireframe Reference

The clickable HTML wireframe prototype at `/wireframes/previewwebsite-index.html` in this repository shows the exact layout, visual hierarchy, and navigation flows for all 7 screens. The agent should open and study this prototype before implementing. It is the canonical visual reference.

Key things to note from the wireframe:
- The Calendar and Daily Plan panel are side-by-side on the same screen (not separate routes) — the panel is always open on the home screen
- The sidebar is a fixed left column, not a hamburger menu
- The "Daily Plan" sidebar link navigates to the standalone Daily Plan screen (no panel)
- The chat input at the bottom of the Daily Plan panel is a shortcut to the Assistant — it sends the message and navigates there
- Assignment chips on the calendar show both the assignment name and its scheduled duration

---

## 11. Non-Functional Requirements

- **Load time:** App should be interactive within 3 seconds on a standard school Chromebook (low-end hardware, mediocre wifi)
- **Offline:** Show a graceful degradation banner if connectivity is lost; do not crash
- **Session persistence:** If a student closes the tab and reopens it, they should not have to sign in again (use refresh tokens / persistent session)
- **Privacy:** No analytics, no third-party tracking scripts in v1. No student data sent anywhere except Google's OAuth and Classroom APIs
- **COPPA note:** If the student's Google account indicates they are under 13, the sign-in flow should require parental consent acknowledgment (out of scope for v1 but flag in the code where this would be added)
- **FERPA note:** OnTrack must not store or transmit assignment data to any third party. The only external calls are to Google Classroom (student's own data) and the LLM API (use a system prompt that instructs the LLM not to train on conversation data; use Anthropic's or OpenAI's zero data retention option)

---

## 12. What Is Out of Scope for v1

These items were explicitly deferred:
- Mobile app (web only)
- Email/password authentication (Google only)
- Storing assignment data server-side
- Parent visibility features
- Grade tracking or academic performance metrics
- Social/sharing features
- Multi-account support (one Google account per session)
- Native mobile push notifications (browser notifications are fine)
- COPPA parental consent flow (flag where it would go)

---

## 13. Open Questions the Agent Must Decide

These were left open in the specification and the agent must make a concrete choice:

1. **Prioritization algorithm for "cumulative vs. standalone" subjects:** How does OnTrack know which subjects are cumulative? Options: (a) let the student tag subjects as cumulative in Settings, (b) hardcode a default list (math, science, foreign language = cumulative; English, history = standalone), (c) infer from subject name using the LLM. **Recommend option (b) with user override in Assignment Details.**

2. **Task completion mechanism:** The research noted checkboxes feel too binary. The wireframe uses status options (Done early | Taking longer | Finished | Incomplete). Implement these four states. "Finished" marks the assignment complete; "Done early" marks it complete and frees up time for tonight; "Taking longer" and "Incomplete" trigger replanning.

3. **Google Classroom sync cadence:** How often should the app re-sync while the student is using it? Recommend: sync on login + a silent re-sync every 30 minutes in the background, plus a manual "Sync now" option in Settings.

4. **AI model behavior when the plan is empty:** If the student has no assignments, the Assistant should still respond helpfully ("No assignments due — enjoy the evening") rather than giving an error.
