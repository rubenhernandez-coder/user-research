# OnTrack — Design Specification

**Product:** OnTrack — Smart study planner for teenagers  
**Version:** Wireframe v1 (May 2026)  
**Screens:** Login, Calendar (Day / Week / Month), Daily Plan, Classes, Assignment Details, Assistant, Settings

---

## 1. Product summary

OnTrack is a web application that helps high school students manage their academic workload alongside extracurricular commitments. It pulls assignments automatically from Google Classroom, prioritizes them, and tells the student exactly what to work on and when. The AI assistant adjusts the plan in real time when the student reports delays or changes.

**Core value:** Students open OnTrack, see a clear prioritized plan for tonight, and can tell the assistant when something takes longer — without any manual setup.

---

## 2. Design system

### 2.1 Color tokens

| Token | Hex | Usage |
|---|---|---|
| `--bg` | `#f0f2f7` | Page background |
| `--surface` | `#ffffff` | Cards, sidebar, panels |
| `--surface-2` | `#f8f9fb` | Table headers, secondary areas |
| `--border` | `#e8eaf0` | All borders and dividers |
| `--text` | `#111827` | Primary text |
| `--text-muted` | `#6b7280` | Secondary text, labels |
| `--text-subtle` | `#9ca3af` | Placeholder text, time labels |
| `--accent` | `#4f6ef7` | Primary action color (buttons, active nav, today indicator) |
| `--accent-light` | `#eef0fe` | Accent tint backgrounds |
| `--accent-dark` | `#3a56d4` | Accent hover state |

**Class colors** — each subject has a full color + light tint pair used consistently across chips, cards, left borders, and badges:

| Class | Color | Tint | Text on tint |
|---|---|---|---|
| Biology | `#10b981` | `#d1fae5` | `#065f46` |
| Algebra II | `#3b82f6` | `#dbeafe` | `#1e3a8a` |
| History | `#f59e0b` | `#fef3c7` | `#78350f` |
| English | `#8b5cf6` | `#ede9fe` | `#4c1d95` |

### 2.2 Typography

**Font family:** System font stack — `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`  
**Font smoothing:** antialiased

| Role | Size | Weight | Usage |
|---|---|---|---|
| Page title | 17px | 700 | Screen headers |
| Card title | 15px | 700 | Panel headers, overlay titles |
| Body | 13–14px | 400–500 | General content |
| Label | 12px | 600 | Form labels, badge text |
| Meta / caption | 11px | 500 | Dates, durations, status |
| Micro label | 10–11px | 700 | Section headers (uppercase + letter-spacing 0.5px) |
| Logo | 20px | 800 | Sidebar logo |
| Login logo | 30px | 800 | Login screen only |

### 2.3 Border radius

| Token | Value | Usage |
|---|---|---|
| `--r-sm` | `6px` | Small chips, status badges, inner controls |
| `--r` | `10px` | Buttons, inputs, plan items, detail fields |
| `--r-lg` | `16px` | Cards, folders, calendar grid, modals |
| `--r-xl` | `20px` | Login card, add assignment overlay |

### 2.4 Shadows

| Token | Value | Usage |
|---|---|---|
| `--shadow-xs` | `0 1px 3px rgba(0,0,0,0.06)` | Sidebar, subtle elevation |
| `--shadow-sm` | `0 2px 8px rgba(0,0,0,0.08)` | Calendar grid, class folders |
| `--shadow` | `0 4px 16px rgba(0,0,0,0.10)` | Floating elements |
| `--shadow-lg` | `0 8px 28px rgba(0,0,0,0.13)` | Login card, modal overlays, status popup |

### 2.5 Spacing

Base unit: **8px**. Common values: 4, 6, 8, 10, 12, 14, 16, 18, 20, 24, 28, 36, 48px.

---

## 3. Layout structure

The app has two top-level layouts:

### 3.1 Login layout
Full-viewport centered card. No sidebar. Gradient background.

### 3.2 App shell (all other screens)
Two-column flex row:

```
┌──────────────┬──────────────────────────────────────────┐
│   Sidebar    │             Main content area             │
│   212px      │             flex: 1                       │
│   fixed      │             background: --bg              │
└──────────────┴──────────────────────────────────────────┘
```

The Calendar screen adds a third column (Daily Plan panel, 272px) to the right of the main area.

---

## 4. Sidebar

**Width:** 212px  
**Background:** `--surface`  
**Right border:** 1px solid `--border`  
**Shadow:** `--shadow-xs`

### Sections

**Logo area** (top, border-bottom)  
- Text: "OnTrack" in accent color, 20px / 800 weight  
- Subtext: "beta" in muted, 13px / 400 weight, inline  
- Padding: 18px 20px 16px

**Nav** (flex: 1, padding 10px)  
Each nav item:
- Layout: flex row, gap 9px (icon + label)
- Padding: 9px 12px
- Border-radius: `--r`
- Font: 13px / 500
- Default color: `--text-muted`
- Hover: background `--surface-2`, color `--text`
- **Active state:** background `--accent-light`, color `--accent`, font-weight 600
- Icons (emoji): 📅 Calendar · 📚 Classes · 💬 Assistant · ✅ Daily Plan

**Bottom section** (border-top, padding 10px 10px 14px)  
- ⚙️ Settings nav item (same style as above)

---

## 5. Components

### 5.1 Buttons

**Primary button**
- Background: `--accent` (#4f6ef7)
- Text: white, 13px / 700
- Padding: 9px 20px
- Border-radius: `--r`
- Hover: background `--accent-dark`

**Secondary button**
- Background: `--surface`
- Border: 1.5px solid `--border`
- Text: `--text-muted`, 13px / 600
- Padding: 9px 16px
- Border-radius: `--r`
- Hover: background `--surface-2`

**Add assignment button** (in calendar toolbar)
- Background: `--accent`
- Text: white, 13px / 700, prefix "＋"
- Padding: 7px 14px
- Border-radius: `--r`

**Disconnect button** (in Settings)
- Secondary style, hover border-color `#ef4444`, hover text `#ef4444`

### 5.2 Toggle switch

- Pill shape: 38px × 22px, border-radius 11px
- Off state: background `--border`
- On state: background `--accent`
- Knob: white circle 18px, top 2px, left 2px (off) / left 18px (on)
- Knob shadow: `0 1px 3px rgba(0,0,0,0.2)`
- Transition: 0.2s

### 5.3 Text inputs

- Border: 1.5px solid `--border`
- Border-radius: `--r`
- Padding: 9px 12px
- Font: 13px
- Focus: border-color `--accent`

Chat input (in Assistant and Daily Plan panel):
- Same base styles, border-radius 24px for the full-width bar version

### 5.4 Select / dropdown

- Border: 1.5px solid `--border`
- Border-radius: `--r-sm`
- Padding: 6px 10px
- Font: 12px / 500

### 5.5 Status badges

Pill-shaped inline labels:

| Badge | Background | Text color |
|---|---|---|
| In progress | `--alg-light` (`#dbeafe`) | `#1e3a8a` |
| Upcoming | `--surface-2` + border | `--text-muted` |
| Done | `--bio-light` (`#d1fae5`) | `#065f46` |

Font: 11px / 600, padding: 3px 9px, border-radius 20px

### 5.6 Plan item card

Used in Daily Plan panel and standalone Daily Plan screen.

- Background: `--surface`
- Border: 1px solid `--border`
- Border-radius: `--r`
- Padding: 11px 13px
- Left colored bar: 4px solid, border-radius applied to left corners
- Hover: `--shadow-sm` + `translateY(-1px)`
- Class label: 10px / 700, uppercase, letter-spacing 0.6px, class color
- Assignment name: 13px / 600
- Meta row: 11px / regular, `--text-muted`, flex with gap 10px

Left bar colors by class: Bio `#10b981` · Algebra `#3b82f6` · History `#f59e0b` · English `#8b5cf6`

### 5.7 Calendar chips (Week / Month views)

- Border-radius: `--r-sm`
- Padding: 4px 8px
- Font: 11px / 500
- Left border: 3px solid class color
- Background: class tint color
- Text: class dark text color
- Small subtext: 10px, 75% opacity, displayed as block below name

### 5.8 Class folder

- Background: `--surface`
- Border: 1px solid `--border`
- Border-radius: `--r-lg`
- Shadow: `--shadow-xs`
- Header: 13px / 700, padding 13px 18px, color dot (10px circle, class color) + label
- Chevron: 11px, `--text-subtle`, rotates 90° when open
- Header hover: background `--surface-2`
- Assignments area revealed below header on click

### 5.9 Chat message bubble

AI message:
- Background: `--surface`, border: 1px solid `--border`
- Border-radius: 4px (top-left) / `--r-lg` (other corners)
- Shadow: `--shadow-xs`

User message:
- Background: `--accent`
- Text: white
- Border-radius: `--r-lg` (top-left) / 4px (top-right) / `--r-lg` (bottom corners)

Message label above bubble: 10px / 700, `--text-subtle`, uppercase, letter-spacing 0.5px

---

## 6. Screens

### Screen 1 — Login

**Layout:** Full viewport, flex center  
**Background:** `linear-gradient(135deg, #eef0fe 0%, #f0f2f7 60%, #fef3c7 100%)`

**Login card:**
- Width: 340px, padding: 48px 44px
- Border-radius: `--r-xl` (20px)
- Shadow: `--shadow-lg`
- Background: white

**Contents (top to bottom):**
1. Logo — "OnTrack", 30px / 800, color `--accent`, margin-bottom 6px
2. Tagline — "Your smart study planner", 13px, `--text-muted`, margin-bottom 36px
3. Google sign-in button — full-width, Google logo icon + "Continue with Google", border 1.5px `--border`, hover `--surface-2`
4. Note below button — "First sign-in pulls your assignments from Google Classroom", 11px, `--text-subtle`, italic, margin-top 14px

**Interaction:** Clicking "Continue with Google" → navigates to Calendar screen (app shell appears)

---

### Screen 2 — Calendar (default / home screen)

**Layout:** App shell with sidebar. Main area split horizontally:
- Left: Calendar main (flex 1, padding 20px 24px)
- Right: Daily Plan panel (272px, fixed width)

#### 2a. Calendar toolbar

Flex row, space-between, margin-bottom 16px:

- **Left:** Title text ("May 2026" / "Tuesday, May 26" depending on view), 17px / 700
- **Right:** View toggle group + Add assignment button

**View toggle group:**
- Background: `--surface-2`, border: 1px solid `--border`, border-radius `--r-sm`, padding 3px, gap 2px
- Three buttons: Day · Week · Month
- Active button: white background, `--shadow-xs`, text `--text`
- Default active: Week

**Interaction:** Clicking a tab switches the calendar view below and updates the title text.

---

#### 2b. Day view

Single day (Tuesday, May 26). Vertical timeline.

**Container:** Grid with 2 columns — time labels (58px) + events area (flex 1)  
**Background:** `--surface`, border-radius `--r-lg`, shadow `--shadow-sm`

**Time column:**
- 8 rows from 3 PM to 10 PM, each 64px tall
- Labels: 10px / 600, `--text-subtle`, right-aligned
- Right border: 1px solid `--border`

**Events area:**
- 8 hour-line dividers (64px each)
- Events positioned absolutely within the column

**"Now" indicator line:**
- 2px horizontal line, color `--accent`
- Small filled circle (10px) on left end, same color
- Positioned at current time

**Events on Tue May 26:**

| Assignment | Class | Time | Top offset | Height |
|---|---|---|---|---|
| Homework 9 | Algebra II | 5:00–5:45 PM | 130px | 46px |
| Lab Report — Cell Membranes | Biology | 7:00–8:30 PM | 258px | 94px |
| Essay — chunk 1 of 3 | History | 8:30–9:15 PM | 354px | 46px |

**Event block styling:**
- Border-radius: `--r`
- Left border: 4px solid class color
- Background: class tint
- Text color: class dark text
- Internal: class label (10px / 700 uppercase) + name (12px / 700) + time range (10px, 70% opacity)
- Hover: opacity 0.9, `--shadow-sm`

---

#### 2c. Week view

Shows Mon May 25 – Sun May 31 as 7 columns.

**Grid:** `52px` (time) + `repeat(7, 1fr)`  
**Background:** `--surface`, border-radius `--r-lg`, shadow `--shadow-sm`

**Header row:** Day abbreviations + date number, 11px / 600, uppercase. Today (Tue 26) highlighted with `--accent-light` background and `--accent` text.

**Rows:** DUE row (assignment chips showing due dates) + time rows (3 PM, 5 PM, 7 PM, 9 PM)

**Content:**

| Time | Tue 26 | Wed 27 | Thu 28 |
|---|---|---|---|
| DUE | Bio Lab Report | Algebra HW 9 | History Essay |
| 5 PM | Algebra HW 9 study (45m) | — | History Essay ch.1 study (45m) |
| 7 PM | Bio Lab Report study (90m) | — | History Essay ch.2 study (45m) |

---

#### 2d. Month view

Full May 2026 calendar grid.

**Structure:** 7 columns (Mon–Sun) × 5 rows. April days (27–30) gray/faded.  
**Cell size:** min-height 90px, padding 7px 8px  
**Today (May 26):** Day number shown as filled blue circle (26px, background `--accent`, white text)

**Assignment indicators per day:**

| Date | Chips |
|---|---|
| May 8 | English: Reading Response #3 |
| May 12 | Algebra: Algebra Test |
| May 14 | Biology: Ch.6 Quiz |
| May 15 | English: Essay Draft |
| May 20 | History: Mid-term Project |
| May 22 | Algebra: HW 8 |
| May 25 | History: Essay study |
| May 26 (today) | Biology: Lab Report study · Algebra: HW 9 study |
| May 27 | Biology: Lab Report DUE · History: Essay study |
| May 28 | Algebra: HW 9 DUE · History: Essay study |
| May 29 | History: Essay DUE |

Month chips: 10px / 600, padding 2px 6px, border-radius 4px, class tint + dark text. Truncate with ellipsis if too long.

---

#### 2e. Daily Plan panel (right side of Calendar)

**Width:** 272px  
**Background:** `--surface`  
**Left border:** 1px solid `--border`  
**Layout:** Column — header / scrollable list / chat input

**Header:** "Daily Plan" (15px / 700) + "Tuesday, May 26" (11px, `--text-muted`). Padding 16px 18px 12px. Border-bottom.

**Plan list (3 items for today):**

1. Biology — Lab Report · Due tomorrow · 90 min
2. Algebra II — Homework 9 · Due Wed · 45 min
3. History — Essay (chunk 1 of 3) · Due Thu · 45 min

Each item uses the plan item card component with its class color.  
**Interaction:** Tapping any item → status popup appears near cursor

**Chat input bar** (bottom, `--surface-2` background, border-top):
- Text input: placeholder "Tell the assistant..."
- Send button "→": accent color, border-radius `--r`
- **Interaction:** Pressing send (or clicking →) → navigates to Assistant screen

---

### Screen 3 — Daily Plan (standalone)

Reachable via sidebar "Daily Plan" nav item.

**Layout:** App shell (no right panel). Page header + scrollable list.

**Page header:** "Daily Plan" (17px / 700) + date subtitle. Background `--surface`, border-bottom.

**Content:** Same 3 plan items as the panel, displayed in a column with max-width 380px, gap 8px, padding 24px. Same plan item card component and interactions.

---

### Screen 4 — Classes

**Layout:** App shell. Page header + scrollable content area (padding 24px).

**Page header:** "Classes"

**Content:** Four class folders stacked vertically with gap 10px.

**Class folders (in order):**
1. Biology (green dot)
2. Algebra II (blue dot)
3. History (amber dot)
4. English (purple dot)

Each folder starts collapsed. Clicking the header toggles it open.

**Open Biology folder shows:**

| Assignment | Due | Est. time | Status |
|---|---|---|---|
| Lab Report — Cell Membranes | May 27 | 90 min | In progress |
| Chapter 7 Reading | Jun 2 | 30 min | Upcoming |

**Open Algebra II folder shows:**

| Assignment | Due | Est. time | Status |
|---|---|---|---|
| Homework 9 — Quadratics | May 28 | 45 min | In progress |
| Quiz Review | Jun 3 | 60 min | Upcoming |

**Open History folder shows:**

| Assignment | Due | Est. time | Status |
|---|---|---|---|
| Essay — Industrial Revolution | May 29 | 135 min | In progress |

**Open English folder shows:**

| Assignment | Due | Est. time | Status |
|---|---|---|---|
| Reading Response #4 | Jun 5 | 45 min | Upcoming |

**Assignment row styling:** Grid `1fr 90px 72px 100px`, 12px text, hover `--surface-2`.  
**Column header row:** 10px / 700, uppercase, `--text-subtle`, `--surface-2` background.  
**Interaction:** Clicking any assignment row → Assignment Details screen.

---

### Screen 5 — Assignment Details

**Reachable from:** Daily Plan item popup · Calendar chip · Classes row  
**Layout:** App shell. Page header with back link + scrollable content (max-width 600px, padding 24px).

**Page header:** Back link "← Classes" (12px / 600, `--text-muted`, hover turns accent)

**Content:**

**Title:** "Lab Report — Cell Membranes", 22px / 800  
**Class tag:** Pill badge in class tint with color dot, class name + "· Synced from Google Classroom"  
- Biology example: green tint, green dot, text `#065f46`

**Details grid (2×2):**

| Field | Value | Notes |
|---|---|---|
| Due date | May 27, 2026 | Read-only |
| Status | In progress badge | Read-only |
| Estimated time | 90 min | Editable text input (editing recalculates plan) |
| Topic | Cell Membranes | Read-only |

Each field is a card: white, border 1px `--border`, border-radius `--r`, padding 12px 14px.  
Field label: 10px / 700, uppercase, `--text-subtle`.  
Field value: 14px / 600.  
Editable field: borderless input inside the card, focus shows border-bottom `--accent`.

**Chunking toggle row:**
- Label: "Break into daily chunks" (13px / 600)
- Description: "OnTrack splits this across multiple sessions" (11px, `--text-muted`)
- Toggle switch on the right
- Default state: ON for the Biology Lab Report example

**Chunks preview** (shown when toggle is ON):
- Background `--surface-2`, border `--border`, border-radius `--r`, padding 14px
- Section title: "Planned sessions", 11px / 700, `--text-muted`, uppercase
- Two rows: "Tonight (Tue May 26) — 45 min" · "Tomorrow (Wed May 27) — 45 min"
- Note below: "OnTrack reschedules automatically if a session is marked incomplete.", 11px, `--text-subtle`

**Update status section:**
- Section title: 11px / 700, uppercase, `--text-subtle`, margin-top 20px
- Four inline buttons: "Done early" · "Taking longer" · "Finished" · "Incomplete"
- Style: border 1.5px `--border`, border-radius `--r`, 12px / 600, `--text-muted`
- Hover: border `--accent`, text `--accent`, background `--accent-light`

---

### Screen 6 — Assistant

**Layout:** App shell, full height column — header / scrollable chat messages / chat input bar

**Header:** "Assistant" (17px / 700) + subtitle "Ask anything about your plan" (12px, `--text-muted`). Background `--surface`, border-bottom.

**Chat messages** (padding 20px 24px, gap 16px):

*AI opening message:*
> Here's your plan for tonight:
> 1. **Biology Lab Report** — 90 min (due tomorrow — top priority)
> 2. **Algebra HW 9** — 45 min (due Wed)
> 3. **History Essay chunk 1** — 45 min (due Thu)
>
> That's about 3 hrs total. Let me know if anything changes.

*Student message:*
> Biology is taking way longer than I thought — been on it 2 hours and I'm still not done.

*AI follow-up:*
> Got it — I've moved Algebra and History to tomorrow.
>
> Updated plan for tonight:
> 1. **Biology Lab Report** — finish it (you're almost there)
>
> I'll slot Algebra and History chunk 1 in tomorrow around your other assignments.

Messages are right-aligned for the student, left-aligned for the AI. Max-width 78%. See component spec §5.9 for bubble styling.

**Chat input bar** (padding 14px 24px, `--surface` background, border-top):
- Full-width pill input: "Tell OnTrack what's happening...", border-radius 24px
- "Send" button: `--accent`, border-radius 24px, 13px / 700

---

### Screen 7 — Settings

**Layout:** App shell. Page header + scrollable content (max-width 540px, padding 24px).

**Page header:** "Settings"

Four settings sections:

#### Notifications
| Row | Control |
|---|---|
| Study reminder — "OnTrack reminds you when it's time to start" | Select: 30 min before / 1 hr before / At start time / Off |
| Deadline reminders — "Alerts as due dates approach" | Toggle (default ON) |

#### Availability hours
| Row | Control |
|---|---|
| I'm usually free after — "OnTrack plans sessions starting from this time" | Time input (default 4:00 PM) |
| I stop working by — "OnTrack won't schedule past this time" | Time input (default 10:00 PM) |

#### Accessibility
| Row | Control |
|---|---|
| High contrast mode | Toggle (default OFF) |
| Color-blind friendly display | Toggle (default OFF) |
| Text size | Select: Default / Large / Extra large |

#### Google account
| Row | Control |
|---|---|
| ruben@students.school.edu — "Assignments synced automatically from Google Classroom" | "Disconnect" button (danger hover) |

**Section title style:** 11px / 700, uppercase, `--text-muted`, letter-spacing 0.6px, margin-bottom 10px  
**Settings card:** `--surface`, border 1px `--border`, border-radius `--r-lg`, `--shadow-xs`, rows separated by 1px `--border`  
**Row padding:** 14px 18px  
**Row label:** 13px / 600  
**Row description:** 11px, `--text-muted`, margin-top 2px

---

## 7. Overlays

### 7.1 Status popup

Appears near the tapped plan item (cursor position + 10px offset, constrained to viewport).

- Background: `--surface`, border-radius `--r-lg`, shadow `--shadow-lg`, padding 10px, width 230px
- Section title: 11px / 700, uppercase, `--text-muted`
- Five options:
  1. ✓ Done early
  2. ⏱ Taking longer → tell assistant *(navigates to Assistant)*
  3. 🏁 Finished
  4. ↩ Incomplete
  5. ☕ Need a break
- Each option: full-width button, 12px / 500, transparent background, border-radius `--r-sm`, hover `--surface-2`
- **Dismiss:** click outside the popup

### 7.2 Add assignment overlay

Triggered by "+ Add assignment" button in calendar toolbar.

- **Backdrop:** `rgba(0,0,0,0.4)` with `backdrop-filter: blur(2px)`, click backdrop to close
- **Card:** `--surface`, border-radius `--r-xl`, shadow `--shadow-lg`, padding 28px, width 380px

**Form fields:**
1. Class (select): Biology / Algebra II / History / English
2. Assignment name (text input): placeholder "e.g. Chapter 8 Reading"
3. Topic (text input, optional): placeholder "e.g. Photosynthesis"
4. Due date (date input) + Est. time in minutes (number input) — in a 2-column row

**Actions:** "Cancel" (secondary) + "Add assignment" (primary) — right-aligned

---

## 8. Navigation flows

```
Login
  └── "Continue with Google" → Calendar (default screen)

Sidebar
  ├── Calendar  → Calendar screen (Daily Plan panel visible on right)
  ├── Classes   → Classes screen
  ├── Assistant → Assistant screen
  ├── Daily Plan → Daily Plan standalone screen
  └── Settings  → Settings screen

Calendar
  ├── View toggle (Day / Week / Month) → switches calendar view in place
  ├── "+ Add assignment" → Add assignment overlay
  ├── Calendar chip (any) → Assignment Details
  └── Daily Plan panel
        ├── Plan item tap → Status popup
        │     └── "Taking longer → tell assistant" → Assistant
        └── Chat send button → Assistant

Classes
  └── Any assignment row → Assignment Details

Assignment Details
  └── "← Classes" back link → Classes

Assistant
  └── (no outbound navigation)

Settings
  └── "Disconnect" confirm → Login screen
```

---

## 9. Responsive behavior

This is a **web application, desktop-first.** Minimum supported viewport: 1024px wide. No mobile layout defined in v1.

Sidebar is fixed-width (212px). Calendar panel is fixed-width (272px). All other areas use `flex: 1` and scroll independently.

---

## 10. Content inventory

### Classes and assignments (sample data)

| Class | Color | Assignments |
|---|---|---|
| Biology | Green | Lab Report — Cell Membranes (due May 27, 90 min, in progress) · Chapter 7 Reading (due Jun 2, 30 min) |
| Algebra II | Blue | Homework 9 — Quadratics (due May 28, 45 min, in progress) · Quiz Review (due Jun 3, 60 min) |
| History | Amber | Essay — Industrial Revolution (due May 29, 135 min, in progress) |
| English | Purple | Reading Response #4 (due Jun 5, 45 min) |

### Today's plan (Tue May 26)

1. Biology — Lab Report · Due tomorrow · 90 min
2. Algebra II — Homework 9 · Due Wed · 45 min
3. History — Essay (chunk 1 of 3) · Due Thu · 45 min

### Google account (placeholder)
Email: `ruben@students.school.edu`
