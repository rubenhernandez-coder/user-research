# UA6 — Specification

The Stage 3 deliverable. Pulls everything from Stages 1 and 2 into a single document that a developer — human or AI — can build from.

The screens are the spine. In a small project the screens are the functional requirements: each screen names what the system does in terms a user would recognize.

MVP scoping is not a section in this document. Which screens get built first emerges during wireframing as the deadline forces choices, not from a planning artifact written before the work begins.

---

## Overview

### Positioning statement

> For teenagers juggling academics and extracurricular obligations, who struggle to balance their academic workload with everything else competing for their time, OnTrack is a smart study planner that turns a chaotic schedule into a clear plan, reducing the stress of juggling academics and outside commitments. Unlike trying to remember every deadline in your head, setting it as an alarm, or basic planner apps, our product tells you how to use your time effectively and is built around the reality of a teenager's packed schedule.

### Summary

OnTrack is a web application designed to tackle academic overload for high schoolers. It works by actively tracking deadlines and structuring a plan to tackle the work.

---

## Screen inventory

A flat list of every screen the system needs.

| # | Screen | Purpose (one sentence) | Scenarios that pass through it |
|---|--------|------------------------|--------------------------------|
| 1 | Login | Sign in with Google; auto-pulls assignments from Google Classroom on first sign-in. | All three — entry point for every user. |
| 2 | Calendar | Main/home screen — a timeline view of all assignments across time. Houses the left sidebar navigation and opens with the Daily Plan panel visible by default. Also the place to manually add a missing assignment. | Job 1 (Jayden), Job 2 (Jovan), Job 3 (Luis) — all users land here after login. |
| 3 | Daily Plan | A panel that opens within the Calendar view — today's prioritized work list showing what to tackle and in what order. | Job 1 (Jayden), Job 2 (Jovan), Job 3 (Luis) |
| 4 | Classes | Left sidebar section showing all classes as folders; open a folder to see its individual assignments. Previously called "Assignments." | Job 3 (Luis — navigating to an assignment to add context) |
| 5 | Assignment Details | Details for a single assignment, including estimated time and whether it should be broken into daily chunks; reachable from the Daily Plan panel or from Classes → class folder → assignment. | Job 3 (Luis — adding time estimate and chunking for the history project) |
| 6 | Assistant | Left sidebar section that opens an AI conversation — explains the current plan in plain language and can adjust it based on what the student reports. | Job 1 (Jayden — reporting biology running long), Job 2 (Jovan — reporting late start), Job 3 (Luis — reporting biology incomplete) |
| 7 | Settings | Let the student configure notifications, availability hours, accessibility options, and their connected Google account. | Not walked in any scenario — infrastructure screen. |

---

## Screen descriptions

### Screen 2 — Calendar

- **Purpose:** Show all assignments across time so the student can see their full workload at a glance; also the place to manually add a missing assignment.
- **Who lands here:** Every logged-in student — this is the main/home screen. The Daily Plan panel opens alongside it by default. The left sidebar (Calendar, Classes, Assistant, Daily Plan) is always visible here.
- **What's shown:** A timeline of assignments in the selected view (daily, weekly, or monthly). View toggle at the top. Add assignment button visible on screen.
- **What they can do:**
  - Switch between daily, weekly, and monthly view
  - Tap an assignment on the timeline to open its details
  - Tap "add assignment" to open the add assignment form
  - Submit the add assignment form (fields: class, assignment name, topic, due date, estimated time)
- **Where each action goes:**
  - Switch view → timeline updates on the same screen
  - Tap assignment → Assignment Details
  - Tap "add assignment" → form appears over the Calendar
  - Submit form → assignment added, form closes, Calendar and Daily Plan update

---

### Screen 3 — Daily Plan (panel)

- **Purpose:** Show today's prioritized assignment list so the student knows exactly what to work on and in what order.
- **Who lands here:** Any logged-in student — the Daily Plan panel opens by default alongside the Calendar every time OnTrack is opened. Also reachable by tapping Daily Plan in the left sidebar.
- **What's shown:** A scrollable list of today's assignments, each showing: class name, assignment name, due date, and time to work on it tonight. If there are no assignments, shows "No assignments posted yet." A fixed chat input sits at the bottom of the panel and does not scroll away.
- **What they can do:**
  - Tap an assignment to open the status popup
  - Type in the chat input at the bottom to message the Assistant
- **Where each action goes:**
  - Tap assignment → status popup appears on top of the Daily Plan (update status: done early, need a break, taking longer, finished, incomplete)
  - Chat input → message sent to Assistant; Assistant responds and can adjust the plan; Daily Plan updates to reflect the change

---

### Screen 1 — Login

- **Purpose:** Let the student sign into OnTrack using their Google account.
- **Who lands here:** Any student opening OnTrack for the first time, or a returning student who has been signed out. They arrived by navigating to the OnTrack URL.
- **What's shown:** The OnTrack name/logo and a single "Sign in with Google" button.
- **What they can do:**
  - Sign in with Google
- **Where each action goes:**
  - Sign in with Google → Google handles authentication → first-time users: OnTrack auto-pulls assignments from Google Classroom, then lands on Calendar with Daily Plan panel open. Returning users: Calendar with Daily Plan panel open.

### Screen 4 — Classes

- **Purpose:** Let the student browse all their assignments organized by class folder.
- **Who lands here:** A student who taps Classes in the left sidebar. They want to see their full workload outside of today's plan, or navigate to a specific assignment.
- **What's shown:** A list of class folders. Opening a folder shows the assignments for that class, each displaying: assignment name, due date, estimated time, and status (done, in progress, incomplete).
- **What they can do:**
  - Open a class folder to see its assignments
  - Tap an assignment to open its details
- **Where each action goes:**
  - Open class folder → expands to show assignment list within the same screen
  - Tap assignment → Assignment Details

---

### Screen 5 — Assignment Details

- **Purpose:** Show the full details of a single assignment and let the student edit its planning information.
- **Who lands here:** A student who tapped an assignment from the Daily Plan popup, the Calendar timeline, or a class folder in Classes.
- **What's shown:** Assignment name, class, topic, due date, estimated total time, current status, and how OnTrack has broken it into daily chunks (if applicable).
- **What they can do:**
  - Edit estimated time
  - Toggle chunking on or off (break into daily pieces vs. treat as one session)
  - Update status (done early, taking longer, finished, incomplete)
- **Where each action goes:**
  - Edit estimated time → OnTrack recalculates the Daily Plan
  - Toggle chunking → OnTrack recalculates the Daily Plan
  - Update status → status updates; OnTrack recalculates the Daily Plan if needed; student stays on this screen

---

### Screen 6 — Assistant

- **Purpose:** Let the student have a conversation with the AI to explain delays or changes, and receive an updated plan in plain language.
- **Who lands here:** A student who taps Assistant in the left sidebar, or who types in the chat input at the bottom of the Daily Plan panel.
- **What's shown:** A conversation thread between the student and the AI. The AI explains the current plan in plain language and responds to updates the student reports (e.g., "biology took longer than expected," "I'm starting late tonight").
- **What they can do:**
  - Type a message to the Assistant
  - Read the Assistant's response and updated plan
- **Where each action goes:**
  - Send message → Assistant responds; if the plan changes, the Daily Plan panel and Calendar update automatically

### Screen 7 — Settings

- **Purpose:** Let the student configure how OnTrack behaves for them.
- **Who lands here:** A student who taps Settings at the bottom of the left sidebar.
- **What's shown:** Four setting areas: notifications, availability hours, accessibility, and connected Google account.
- **What they can do:**
  - Set notification preferences (when and how often to be reminded)
  - Set availability hours (what time they're usually free to work, so OnTrack plans around their schedule)
  - Toggle accessibility options (text size, high contrast mode, color-blind friendly display)
  - View or disconnect their connected Google account
- **Where each action goes:**
  - Any change → saves immediately; OnTrack adjusts behavior going forward
  - Disconnect Google account → returns to Login screen

---

## Use Cases

Precise system behavior for each of the three jobs. These translate the Stage 2 scenarios into step-by-step flows a developer can build from, including failure states.

---

### Use Case 1 — Knowing what to work on during a crunch

**Trigger:** Student opens OnTrack when overwhelmed by multiple assignments.

1. Student opens OnTrack and lands on the Calendar with the Daily Plan panel open.
2. System has already pulled all assignments from Google Classroom on login.
3. System calculates priority order: cumulative/high-dependency subjects (e.g., biology before math packet), ordered by risk of falling behind, with easiest/lowest-stakes tasks last.
4. System estimates time per assignment for tonight based on the student's configured availability hours and total estimated time per assignment.
5. Daily Plan panel displays the ordered list — each item shows: class name, assignment name, due date, time to work on tonight.
6. Student taps an assignment → status popup appears with options: done early, need a break, taking longer than expected, finished, incomplete.
7. Student selects "taking longer than expected."
8. System recalculates remaining assignments for the night using updated available time.
9. If time runs short, system drops the lowest-priority task from tonight's plan.
10. Daily Plan updates immediately to reflect the new order and time estimates.

**Failure state:** If Google Classroom sync fails on login, system displays an error message on the Calendar and prompts the student to retry or add assignments manually.

---

### Use Case 2 — Getting started on a normal day

**Trigger:** Student opens OnTrack on a regular day with no crisis — they just don't know where to start.

1. Student opens OnTrack and lands on the Calendar with the Daily Plan panel open.
2. System detects current time and calculates available window based on the student's configured availability hours.
3. If the student is starting later than usual (e.g., lost time on the bus commute), system recalculates the plan around the remaining available time.
4. System flags any assignment whose deadline has become tighter due to the late start (e.g., "Friday deadline now tighter than this morning").
5. Daily Plan displays the adjusted prioritized list — hardest/most cognitively demanding first, easiest last.
6. Student types a message in the chat input at the bottom of the Daily Plan panel (e.g., "I'm starting late tonight").
7. Assistant receives the message, recalculates, and responds in plain language explaining the adjusted plan.
8. Daily Plan panel updates to reflect the new plan.

**Failure state:** If the student has no assignments in Google Classroom, Daily Plan shows "No assignments posted yet."

---

### Use Case 3 — Chipping away at a long-term project

**Trigger:** Student has a months-long project and wants OnTrack to break it into daily pieces.

1. Student navigates to Assignment Details for the long-term project (via Calendar timeline or Classes → class folder → assignment).
2. Assignment Details shows the assignment pulled from Google Classroom with its due date.
3. Student sets estimated total time (e.g., 6 hours per sub-assignment).
4. Student toggles chunking on — OnTrack will break the assignment into daily pieces rather than scheduling it as one session.
5. System calculates the number of daily chunks needed and distributes them across available days between now and the deadline.
6. Chunks appear in the Daily Plan alongside other assignments each day — scheduled earlier in the evening when cognitive load is higher.
7. If OnTrack underestimates the time needed for another assignment on the same night (e.g., biology review), that assignment runs over and the student marks it incomplete via the Daily Plan popup.
8. System reschedules the incomplete assignment to the next day as the first priority, with a longer time block.
9. Long-term project chunk remains on schedule for that night — the student still completes it.

**Failure state:** If the student sets an estimated time that is too short for OnTrack to fit into available days before the deadline, system warns: "Not enough time before the deadline. Adjust estimated time or availability hours."

---

## Requirements

- OnTrack must pull assignment data from Google Classroom automatically on login — no manual entry required for synced assignments
- Notifications must be supported — non-negotiable per user research (Liam and Aramis named this directly)
- Availability hours must be configurable so the Daily Plan reflects the student's actual free time, not an assumed schedule
- Accessibility settings must include high contrast mode and a color-blind friendly display option

---

## Constraints and assumptions

- No student data stored by OnTrack in v1 — all assignment data pulled live from Google Classroom to minimize FERPA and COPPA exposure
- Google sign-in only — no email/password accounts
- Web application only — no mobile app in v1
- OnTrack's planning is only as good as the time available — for users with very compressed windows (late commute, late return home), the value is prioritization, not schedule relief; this scope should be communicated clearly in the product

---

## Open questions

- How does OnTrack calculate prioritization — what is the algorithm for deciding which assignment goes first (cumulative subjects, due date proximity, estimated time, or a combination)?
- What does the student see if Google Classroom is down or the sync fails on login?
- Task completion mechanism — something more nuanced than checkboxes is preferred (e.g., reflecting partial completion or "took longer than expected"), but the specific mechanism is not yet decided
