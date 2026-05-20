# UA5 — Stage 2 Analysis

The Stage 2 deliverable. Pulls together what exists in the space, who has a stake in the system beyond the users, who actually uses it, and what users are doing today when they need what the system would provide.

The sections are written in the order a reader would want to encounter them, but the student did not work on them in that order. Activities informed each other.

The positioning statement was revisited throughout. No clause was contradicted by Stage 2 analysis. The competitive alternative clause had already been updated in Stage 1 to name Google Classroom. One open item: the product name has shifted from "Study AI" to "OnTrack" during Stage 2 work — the positioning statement should be updated to reflect this before Stage 3 begins.

---

## Landscape

A short survey of the space OnTrack enters.

### Adjacent products

- **Google Classroom** — the real competition. Every one of the 8 respondents uses it. It's effortless to start because the teacher does all the work — assignments show up automatically, zero setup on the student's side. What it doesn't do: it only notifies students when assignments are posted, not as deadlines approach. Hard to see missing assignments (requires navigating to a different panel). No prioritization or hierarchy — just a list of what's due. No guidance on when to work on things. Students stay on it despite its gaps because switching costs are zero and it's already embedded in their school day. OnTrack has to be equally effortless or it faces the same rejection Ruben gave Google Calendar: "too complicated, waste of time."

- **myHomework** — was beloved by students for a while. Clean, simple, purpose-built for tracking homework. Then it added complexity and a paywall and lost most of its users. The lesson: students abandoned it the moment it stopped feeling effortless. Passive deadline tracker. The gap OnTrack addresses (telling you *when* to work, not just *what* is due) is the same gap myHomework left.

- **MyStudyLife** — similar story to myHomework. Tracks what's due but doesn't tell you when to work on things. Students have to enter everything manually, the interface feels dated, and there's no intelligence behind the scheduling. Shows you the pile, doesn't help you get through it. Ruben's complaint about Google Calendar applies directly here.

- **Trevor AI** — the closest product to what OnTrack wants to be. It takes tasks and auto-schedules them into the user's day. The gap: it's built around a professional's calendar — work meetings, Slack integrations, a 9-to-5 structure. A high schooler's day doesn't look like that. Practice runs until 6pm, homework happens in 20-minute windows on the bus, family responsibilities at night. Trevor AI has no concept of that reality. None of the 8 respondents mentioned it.

- **Notion / Todoist** — general-purpose productivity tools some students use. Require significant setup and customization before they become useful. None of the 8 respondents mentioned them. Not real competition for this user — they're not looking for a configurable system, they want something that works out of the box.

### Open-source candidates

- **shreyashankar/planner** (GitHub) — a smart planner that determines when to study and work on assignments. The user enters a task with a due date and estimated length, and it schedules work sessions automatically. Conceptually close to what OnTrack wants to do. Low adoption, not a polished product. Worth knowing for two reasons: the code exists to learn from, and it confirms the idea isn't novel — someone else had it and started building it. Not a threat; a reference.

### Category

- The category customers think they're shopping in: **smart study planner**
- What that brings with it: deadline visibility, reminders/notifications, low input expectations, simple panelling, ready-to-use immediately (value within the first 60 seconds)
- Whether this is a fit: yes — "smart study planner" is the search term the target user would type, and OnTrack's core function (telling you when to work, not just what is due) fits the category while going meaningfully beyond existing options

### Inherited conventions

Conventions OnTrack is taking on whether it knows it or not. Decided explicitly:

- **Notifications / reminders** — keep. Non-negotiable per respondents. Liam and Aramis both named this directly. Students will abandon a tool that doesn't remind them.
- **Deadline visibility (two-panel: today + this week)** — keep, with intention. A "today" view as primary panel, a "this week" view as secondary. The today view needs to feel manageable — not a condensed version of the overwhelming pile. That's what separates OnTrack from filtered Google Classroom.
- **Low input as hard constraint** — keep. Jovan: "if it automatically had all useful information on it." Google Classroom integration is the obvious answer. Manual entry is the reason students abandoned every other tool. If OnTrack requires manual assignment entry, it will face the same rejection.
- **Ready to use immediately** — keep. Not "set up your profile, add your classes, configure your preferences." Value in the first 60 seconds or the user is gone. Every respondent confirmed this.
- **Task completion mechanism** — open. Want something better than checkboxes if possible — but not committed to a specific mechanism. Stage 3 problem.

---

## Stakeholders and users

### Stakeholders

Everyone with a stake in whether OnTrack succeeds beyond the students using it.

| Stakeholder | Stake | Their version of "success" |
|---|---|---|
| Teachers | Students submit assignments on time. Also: third-party access to assignment data teachers and schools post to Google Classroom — OnTrack would be reading that data without teacher involvement. | Students submitting on time; OnTrack not creating data access or privacy issues teachers have to manage. |
| Google | Controls the Google Classroom API and sets the rules for how third-party apps can use it. Can revoke access or change terms at any time. Real platform dependency risk. | API used within terms; OnTrack doesn't create compliance problems for Google. |
| Parents | Want to know their kids are caught up academically. Academic performance visibility — knowing whether their kid is on top of their work. Could become a feature someday; could also be a student privacy concern. | Kid stays on top of assignments; parents have confidence they're not falling behind. |
| Creator (Rubén Hernández) | Impact stake: students stop drowning — they can fully recover from each day's work and feel good. Practical stake: OnTrack gets adopted, works reliably, doesn't create legal liability from mishandling student data. | Consistent use by the target user; product stays legally sound and technically reliable. |
| Schools | FERPA — a federal law protecting student educational records. If OnTrack pulls data from Google Classroom, it's touching data that falls under FERPA. A school can block students from using OnTrack if it doesn't comply. | OnTrack handles student data lawfully; no FERPA violations that create school liability. |

### Users (recap from Stage 1, with Stage 2 updates)

- **Primary user type:** Teenagers juggling academics and extracurricular obligations — unchanged from Stage 1. The 8 respondents confirmed this is a real and recurring problem, not a seasonal anomaly.
- **Secondary user types:** None identified.
- **What's been added since Stage 1:** Stage 2 surfaced two distinct subtypes within the primary user:
  1. **Crunch-mode users** (Jayden, Ruben) — the problem hits hard and predictably at seasonal peaks (winter season + finals, track + end of semester). They push through on their own but sacrifice sleep and retention doing it.
  2. **Normal-day users** (Jovan) — not in crisis, but don't have a system for deciding what to work on first on an ordinary day. The friction of deciding leads to avoidance (social media, then just doing whatever's due soonest). Both types are the same target user; they come to OnTrack for slightly different reasons.

### Compliance and accessibility considerations

- **FERPA** — OnTrack would pull assignment data from Google Classroom. That data constitutes student educational records under FERPA. Schools have a legal stake in how it's handled. A school could block OnTrack from operating in its environment if it doesn't comply. OnTrack needs to be built so that student data is not stored or shared beyond what's required to generate the schedule.
- **COPPA** — the target user range goes down to age 13. Apps that collect personal data from users under 13 require verifiable parental consent under COPPA. If OnTrack pulls assignment data from Google Classroom for a 12- or 13-year-old, COPPA applies. This isn't a blocker but it shapes the sign-up flow.
- **PII** — assignment data, schedule information, and school/name data are personally identifiable. Needs careful handling even outside of FERPA/COPPA requirements.
- **Accessibility** — not yet answered. Surfaced as a consideration; Stage 3 screen design should account for WCAG basics (contrast, text size, screen reader compatibility). Flagged as open.

---

## Jobs-to-be-done and scenarios

### Job 1 — Crunch prioritization

- **JTBD statement:** When I'm overwhelmed by assignments, I want to know what to work on, so I can have a sense of relief.
- **How do we know it's a real job:** Jovan: *"Sometimes I don't know where to start — starting is probably the hardest part for me, but after that it's usually smooth sailing."* Jayden: *"I often misjudge the work itself or forget about it entirely because of other things I'm focusing on"* — and he picks the shortest assignment first, not the most important. Ruben: *"I usually choose what's easiest or takes the least amount of work."* All three describe the same moment: assignments are piling up and the default is to pick what feels manageable, not what's most critical.
- **What people do today:** Open Google Classroom → see a list of what's posted and due → pick whatever feels easiest or most urgent in that moment → start working on it without knowing if it's the right thing to prioritize. Biology gets done last when it should go first. The wrong order doesn't become obvious until the next morning.
- **Why has the current way persisted:** Zero effort. The information is already in Google Classroom, no setup required, no thinking needed upfront. The cost of bad prioritization only shows up later — and even then, everyone survives. Jayden pushed through to 1am and passed. Ruben pulled through his 2-week crunch. The consequences are real but not catastrophic, which removes the urgency to find a better system.

#### Scenario 1.1 — Jayden's Tuesday

> It's a Tuesday in late November. Jayden gets home at 7pm after practice and a long commute. He opens OnTrack — it's already pulled in all five assignments from Google Classroom automatically. It ranks them: biology reading first (cumulative, high risk to delay), then math packet, then history quiz, then two smaller tasks. Estimated finish: 9:30pm.
>
> He starts with biology. Thirty minutes in he realizes the reading is dense — there are concepts from last week he didn't fully understand, and he has to keep stopping to re-read. An hour passes and he's only halfway through. OnTrack's estimate was wrong; it had no way of knowing the reading would require backtracking.
>
> He's now off schedule. He marks biology as "taking longer than expected." OnTrack adjusts — it drops the lowest-priority task (one of the smaller assignments) and keeps the math packet and history quiz. New estimated finish: 10:45pm. Then the math packet runs long too. It's 11:30pm and he still has the history quiz. He pushes through. Finishes at 12:45am — still later than he wanted, but he did biology first, which mattered. He retained it. He doesn't fall behind in the lab the next morning. OnTrack didn't save him from a long night, but it saved him from a long night that also set him back academically.

**Reads back against positioning statement:** Yes — OnTrack built a clear plan for what to work on and when. **Known gap:** for users like Jayden with late commutes and compressed windows, the value is *prioritization*, not *schedule relief*. OnTrack cannot create time that doesn't exist. The product needs to communicate this scope accurately.

---

### Job 2 — Getting started on a normal day

- **JTBD statement:** When I don't know what to work on, I want to be able to get started, so I can be on track in all my classes.
- **How do we know it's a real job:** Jovan: *"Sometimes I don't know where to start — starting is probably the hardest part for me, but after that it's usually smooth sailing."* Jayden (follow-up): goes for whatever is easiest or shortest on a normal day — not because he's overwhelmed, just because he has no system for deciding what matters. Two respondents confirming the same default on an ordinary week, not just during crunch.
- **What people do today:** Look at all deadlines → analyze time left → feel friction from deciding → pull out phone, scroll social media for ~5 minutes → give up on prioritizing, just do whatever's due soonest. The avoidance loop is the current process. By the time they actually start, they've lost time and done it in the wrong order.
- **Why has the current way persisted:** It works well enough. Nobody in the interview pool failed out of school. Jayden survived the long nights. The consequences of bad prioritization are real but not immediately catastrophic — so there's no urgency to find a better system. Ford said he'd use OnTrack "when I'm older." Diego said he doesn't need it because he's "responsible." The pain isn't bad enough yet to force a change — which is the hardest thing OnTrack has to overcome.

#### Scenario 2.1 — Jovan's Tuesday

> It's a Tuesday. Jovan finishes training and boards the bus home. He plans to use the commute to get a head start on homework — but the bus is warm and he falls asleep before he gets anything done. He gets home at 7pm, an hour later than planned, with the same amount of work and less time to do it.
>
> He opens OnTrack. It's already pulled in his assignments from Google Classroom. It recalculates around his available time — 7pm to a reasonable bedtime — and gives him a prioritized list: math first (hardest, cumulative, needs a clear head), then the history reading, then a short English response last (easy, low stakes, can be done when he's tired). It adjusts automatically for the lost bus time by flagging that Friday's deadline for one assignment is now tighter than it looked this morning.
>
> He follows the list. Math takes longer than expected — 90 minutes instead of 60. But because he did it first, he actually absorbed it. He finishes everything by 11pm and goes to sleep knowing Friday's work is manageable.

**Reads back against positioning statement:** Yes — OnTrack built a clear, day-by-day plan. Even after an unexpected setback (lost bus time), the plan adjusted and held.

---

### Job 3 — Long-term project management

- **JTBD statement:** When I'm doing a long-term project, I want to be able to chip it down little by little, so I can distribute the load.
- **How do we know it's a real job:** Luis had a months-long history project due at the same time as other major assignments — math homework, a biology midterm, an English essay — while managing sports, family responsibilities, and no home wifi. He handled it by cutting off his social life first, then cutting sleep when that wasn't enough, until the quality of his work dropped and he started slacking just to clear his head. The problem was months-long, not a one- or two-week crunch. That's a different job.
- **What people do today:** Wait for a free block of time long enough to make a dent — Luis needed 4+ hours at a stretch, and kept finding ~2-hour windows. When a bigger block finally appeared, other assignments crowded it out. The spiral: cut social life → still not enough time → cut sleep → quality drops → slack to recover → waste the little time remaining → deadline gets closer. None of it was necessary if he'd started chipping away at the project from day one.
- **Why has the current way persisted:** Long-term projects feel like they need long, uninterrupted sessions. Students delay until they can find one. The perfect moment is the enemy of the consistent moment — and by the time students realize the big block isn't coming, the deadline is close and the spiral is already in motion.

#### Scenario 3.1 — Luis's history project

> It's a Monday evening. Luis has a history project with five assignments due over the next two months — each takes roughly 6 hours. He also has math homework and biology studying for a midterm. In the past he'd wait for a free 6-hour block that never comes cleanly, then spiral. Tonight he opens OnTrack instead.
>
> OnTrack breaks the history project into daily 30-minute chunks across the two months and slots them between his other assignments. Tonight's plan: 30 minutes on the first history assignment, then math homework, then a short biology review. Manageable.
>
> Something goes wrong: OnTrack underestimates how long the biology review needs and doesn't allocate enough time for it tonight. Luis finishes the history chunk and math, but when he gets to biology there's only 20 minutes left — not enough to cover the midterm material. He marks biology as incomplete and OnTrack reschedules it to tomorrow as the first priority, with a longer block.
>
> He goes to sleep at a reasonable hour. By Friday, a third of the history project is done. He didn't lose sleep. He didn't cut off his social life. He just did 30 minutes a day.

**Reads back against positioning statement:** Yes — OnTrack built a clear, day-by-day plan before the crunch hit. Luis knew exactly what to work on and when.

---

## Open from this stage

- **Task completion mechanism** — want something better than checkboxes if possible, but not committed to a specific mechanism yet. Carry into Stage 3.
- **Prioritization scope** — OnTrack's planning is only as good as the time available. For users like Jayden with late commutes and very compressed homework windows, the benefit is prioritization, not schedule relief. Stage 3 UI needs to communicate what OnTrack is actually promising.
- **Accessibility** — surfaced but not answered. WCAG basics (contrast, text size, screen reader compatibility) should be factored into Stage 3 screen design.
- **Product name** — referred to as "OnTrack" throughout Stage 2. The positioning statement still says "Study AI." The naming should be reconciled before Stage 3 begins.
