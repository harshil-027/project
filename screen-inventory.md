# 🖥️ Screen Inventory
### AI Resume + Interview Coach

> A complete catalogue of every screen, modal, and state in the product. Used as the reference for design handoff and dev ticketing.

---

| Field | Details |
|-------|---------|
| **Document** | Screen Inventory v1.0 |
| **Date** | March 2026 |
| **Scope** | Phase 1 screens (web, mobile-responsive) |
| **Total Screens** | 24 screens / states (Phase 1) |
| **Phase 2 Additions** | 7 screens |

---

## Screen Count Summary

| Section | Phase 1 Screens | Phase 2 Additions |
|---------|----------------|-------------------|
| Public / Auth | 4 | 0 |
| Dashboard | 1 | 1 |
| Resume | 7 | 3 |
| Interview | 6 | 2 |
| Account | 3 | 0 |
| Modals & overlays | 3 | 1 |
| **Total** | **24** | **7** |

---

## Public & Auth Screens

<details>
<summary><strong>SCR-01 · Landing Page</strong></summary>

<br>

**Purpose:** Convert visitors into sign-ups. Communicate value in under 10 seconds.

**Key elements:**
- Hero headline + sub-headline (the one-liner value prop)
- "Get started free" CTA — primary action above the fold
- 3-panel feature overview: Match Score · Bullet Rewriter · Mock Interview
- Social proof strip: "X resumes improved this week"
- Pricing teaser: "Free to start · Pro from ₹299/month"
- Footer with privacy policy, terms

**States:**
- Default (logged out)
- Post-signup redirect (shows "Welcome, let's get started" banner)

**Design notes:**
- No more than 2 CTAs above the fold
- Mobile: hero CTA must be thumb-reachable
- Load time target: under 2 seconds

</details>

---

<details>
<summary><strong>SCR-02 · Pricing Page</strong></summary>

<br>

**Purpose:** Convert free users to Pro. Answer every objection on the page.

**Key elements:**
- Free vs Pro comparison table (full feature list)
- Price displayed prominently: ₹299/month or $4.99/month
- "Most popular" badge on Pro tier
- Student discount callout: "3 months free with .edu email"
- FAQ accordion (at minimum: "Can I cancel anytime?", "Is my resume data safe?", "What payment methods?")
- "Get Pro" CTA → payment flow

**States:**
- Default
- Post-paywall redirect (arrives from inside the app) — shows "You were about to [action]. Upgrade to continue."
- Student discount applied (price shows as ₹0 for 3 months)

</details>

---

<details>
<summary><strong>SCR-03 · Sign Up Screen</strong></summary>

<br>

**Purpose:** Low-friction account creation.

**Key elements:**
- Google SSO button (primary)
- Email + password form (secondary)
- "By signing up you agree to our Terms and Privacy Policy" — linked
- Already have an account? → Login link

**States:**
- Default
- Error state (email already exists, invalid password)
- Loading (after submit)

**Design notes:**
- No required fields beyond email + password (don't ask for name, phone, college — that comes in onboarding)
- Password requirements shown inline, not just on error

</details>

---

<details>
<summary><strong>SCR-04 · Login Screen</strong></summary>

<br>

**Purpose:** Return users back into the product quickly.

**Key elements:**
- Google SSO button
- Email + password form
- Forgot password link
- Don't have an account? → Sign Up link

**States:**
- Default
- Error state (wrong credentials)
- Forgot password flow (email input → confirmation message)

</details>

---

## Dashboard

<details>
<summary><strong>SCR-05 · Main Dashboard</strong></summary>

<br>

**Purpose:** Orient the user, surface their progress, and give them a clear next action.

**Key elements:**
- Greeting: "Good morning, Priya 👋"
- Resume card: current active resume name + match score for last JD scanned + "Improve" CTA
- Interview card: last mock interview score + role + "Practice again" CTA
- Quick action strip: "Upload new resume" / "Try a mock interview" / "Browse questions"
- Streak indicator: "3-day streak 🔥 Keep it up"
- Upgrade banner (free users only): "You've used 2 of 3 JD scans this month. Upgrade for unlimited."

**States:**
- First-time user (no resume uploaded yet) → shows empty state with "Let's start — upload your resume"
- Returning user with data → default state above
- Pro user → upgrade banner replaced with "Pro member ✨"

</details>

---

## Resume Section

<details>
<summary><strong>SCR-06 · Resume Upload Screen</strong></summary>

<br>

**Purpose:** Get the user's resume into the system as quickly and painlessly as possible.

**Key elements:**
- Drag-and-drop upload zone (large, centred)
- "Or browse files" link
- Accepted formats: PDF, DOCX · Max size: 5MB
- "Or fill in manually" link (fallback)
- Privacy reassurance: "Your resume is encrypted and never shared."

**States:**
- Default (empty)
- File dragged over (highlight zone)
- Uploading (progress indicator)
- Parse success → auto-navigate to Resume Editor
- Parse error → error message + "Try manual entry" CTA

</details>

---

<details>
<summary><strong>SCR-07 · Resume Editor (Main)</strong></summary>

<br>

**Purpose:** The central workspace. This is where the most time is spent.

**Layout:** Two-panel on desktop (resume preview left, feedback panel right). Single column on mobile with tabs.

**Left panel — Resume preview:**
- Editable resume content (sections: Summary, Experience, Skills, Education)
- Each bullet point has an inline "✨ Improve" button
- Accepted suggestions shown with a subtle green highlight
- Section scores shown as small badges (e.g. "Skills 6/10")

**Right panel — Feedback & JD:**
- JD input: paste job description text area with "Analyse" button
- Match score display (once JD is scanned): 0–100 gauge + category breakdown
- Missing keywords list
- Active suggestion card (shows current bullet rewrite options)

**States:**
- No JD scanned (right panel shows JD input only)
- JD scanned (right panel shows full score + keywords)
- Bullet selected for improvement (suggestion card appears in right panel)
- Pro vs Free (free shows rewrite limit counter "3 of 5 rewrites used")

</details>

---

<details>
<summary><strong>SCR-08 · Bullet Rewrite Card</strong></summary>

<br>

**Purpose:** Show 2–3 rewrite options clearly so the user can make a fast, confident decision.

**Key elements:**
- Original bullet shown at top (greyed out)
- 2–3 rewrite options, each with a label badge: "Added metric" / "Stronger verb" / "JD-aligned"
- "Best match for this JD" badge on the recommended option
- Accept / Reject / Edit buttons per option
- "Write my own" inline edit fallback

**States:**
- Loading (AI generating suggestions)
- Loaded (suggestions displayed)
- Accepted (card closes, bullet updates in editor with green highlight)
- All rejected (card closes, original bullet remains, no highlight)

</details>

---

<details>
<summary><strong>SCR-09 · Section Feedback Panel</strong></summary>

<br>

**Purpose:** Give the user a bird's-eye view of what's strong and what needs work across their whole resume.

**Key elements:**
- Tab or accordion per section: Summary · Experience · Skills · Education · Formatting
- Each section: score badge (Weak / Fair / Strong + number) + 2–4 specific suggestions
- Suggestions are expandable — show the "why" behind each suggestion
- "Mark as done" checkbox per suggestion (for user tracking)

**States:**
- No JD scanned: feedback is general best-practice
- JD scanned: feedback is JD-specific (e.g., "Your skills section is missing 'SQL' which appears 4× in this JD")

</details>

---

<details>
<summary><strong>SCR-10 · Manual Resume Entry Form</strong></summary>

<br>

**Purpose:** Fallback for users whose resume fails to parse.

**Key elements:**
- Structured form with fields mirroring a standard resume: Contact Info, Summary, Work Experience (repeating block), Education (repeating block), Skills (tag input)
- "Add another role" / "Add another degree" buttons for repeating sections
- Auto-save every 30 seconds
- "Continue to editor" CTA once at least one experience block is filled

**States:**
- Empty (initial)
- Partially filled (auto-save indicator)
- Complete (CTA becomes active)

</details>

---

<details>
<summary><strong>SCR-11 · ATS Checker · Phase 2</strong></summary>

<br>

**Purpose:** Show the user whether their resume will survive automated screening.

**Key elements:**
- ATS compatibility score (Pass / Warning / Fail per category)
- Categories: Tables detected · Headers with key info · Image content · Keyword coverage
- Keyword gap list: top 10 missing JD keywords ranked by frequency
- Fix instructions per issue (expandable)
- Free users: blurred full report with "Upgrade to see all issues" CTA

**States:**
- No JD scanned (prompt to scan JD first)
- Scan complete (results displayed)
- Free user hitting paywall (partial blur)

</details>

---

<details>
<summary><strong>SCR-12 · Version Manager · Phase 2</strong></summary>

<br>

**Purpose:** Let users manage multiple tailored resumes without losing earlier work.

**Key elements:**
- List of saved versions: label, date saved, last JD alignment score
- "Save current as new version" button (Pro only)
- "Compare two versions" → opens diff view
- Delete version (with confirmation modal)
- Restore version button

**States:**
- Free user (1 version max — shows upgrade prompt if they try to save a second)
- Pro user (up to 10 versions)

</details>

---

## Interview Section

<details>
<summary><strong>SCR-13 · Interview Setup Screen</strong></summary>

<br>

**Purpose:** Get the user into a relevant interview in under 60 seconds.

**Key elements:**
- Role category selector: SWE · PM · Business Analyst · Marketing · Design (card or dropdown)
- Round type selector: HR Screening · Technical · Behavioural · Final Round
- Estimated time: "~15–20 minutes"
- "Start Interview" CTA
- "Browse questions instead" secondary link

**States:**
- Default (no selections made — CTA disabled)
- Role selected, round not yet selected
- Both selected (CTA enabled)
- Free user on 3rd interview attempt (shows "1 of 2 free interviews used this month" counter)

</details>

---

<details>
<summary><strong>SCR-14 · Active Interview Screen</strong></summary>

<br>

**Purpose:** Simulate a real interview with minimal UI distraction.

**Key elements:**
- Question displayed clearly (large, centred text)
- Question counter: "Question 3 of 7"
- Text answer input (large textarea)
- "Submit answer" button
- Timer (optional — can be enabled/disabled in setup)
- Voice mode toggle (Phase 2)
- "End interview early" link (small, bottom corner)

**States:**
- AI question displayed (waiting for answer)
- User typing (character count / no hard limit)
- Follow-up question (AI responds to the user's answer with a follow-up before moving on)
- Last question ("This is the final question")
- Generating debrief (loading state after last answer submitted)

**Design notes:**
- No score or feedback visible during the interview — the user must answer authentically, not game the system
- No "correct answer" hints during the session

</details>

---

<details>
<summary><strong>SCR-15 · Voice Interview Mode · Phase 2</strong></summary>

<br>

**Purpose:** Audio version of the active interview for users who want to practice speaking.

**Key elements:**
- Microphone visualiser (shows audio level)
- Live transcription panel (text appears as user speaks)
- "Stop speaking" / "Submit answer" button
- Filler word counter visible in real time: "um: 2, uh: 1"
- Text fallback toggle

**States:**
- Requesting mic permission
- Active (listening)
- Processing (after user stops speaking)
- Permission denied (fallback to text mode with message)

</details>

---

<details>
<summary><strong>SCR-16 · Interview Debrief Screen</strong></summary>

<br>

**Purpose:** Deliver the most actionable feedback possible. This screen is the core value of the interview pillar.

**Layout:** Overall score at top, per-question breakdown below, summary at bottom.

**Key elements:**
- Overall score (0–100) with a label: "Needs work / Developing / Strong"
- Score breakdown radar chart: Relevance · Structure · Depth · Clarity
- Per-question accordion:
  - Question text
  - User's answer (collapsed by default)
  - Score per dimension
  - Specific AI feedback (2–3 sentences)
- "What to work on" summary: top 3 improvement areas
- CTAs: "Practice again" · "Try a different round" · "Improve your resume"

**States:**
- Loading (generating debrief)
- Loaded (full debrief)
- Partial (if user ended early — shows "Based on X of Y questions")

</details>

---

<details>
<summary><strong>SCR-17 · Question Bank Browser</strong></summary>

<br>

**Purpose:** Let users browse and study questions outside of a live interview session.

**Key elements:**
- Domain filter tabs: SWE · PM · BA · Marketing · Design
- Difficulty filter: Entry / Mid / Senior
- Question list (expandable cards)
- Each question card: question text + "Ideal answer framework" (expandable)
- "Practise this question" CTA on each card → launches a single-question mini-interview
- Free users: 1 domain visible, others locked with upgrade prompt

**States:**
- Domain selected, questions listed
- Question expanded (shows framework)
- Locked domain (free user)

</details>

---

<details>
<summary><strong>SCR-18 · Past Interviews History</strong></summary>

<br>

**Purpose:** Let users track their interview practice over time.

**Key elements:**
- List of past sessions: date, role, round, overall score
- Click to re-open debrief for any session
- "Improvement trend" indicator (score change vs. previous session of same type)

**States:**
- No history (empty state: "Complete your first mock interview →")
- History available

</details>

---

## Account & Settings

<details>
<summary><strong>SCR-19 · Profile & Settings Screen</strong></summary>

<br>

**Key elements:**
- Name, email (editable)
- Target role (editable — used to personalise defaults)
- Password change
- Notification preferences (email nudges on/off)
- Data & privacy: "Delete my account and all data"

</details>

---

<details>
<summary><strong>SCR-20 · Subscription & Billing Screen</strong></summary>

<br>

**Key elements:**
- Current plan: Free or Pro
- Free users: usage summary (JD scans used: 2/3, mock interviews: 1/2) + "Upgrade to Pro" CTA
- Pro users: renewal date, payment method, "Cancel subscription" link
- Invoice history (Pro only)

</details>

---

<details>
<summary><strong>SCR-21 · Upgrade / Payment Flow</strong></summary>

<br>

**Key elements:**
- Plan confirmation (what they're getting)
- Payment form: card details via Razorpay (India) / Stripe (international)
- Student discount field: .edu email entry for 3-month free trial
- Order summary
- Confirmation screen post-payment

**States:**
- Default
- Student discount applied
- Payment processing
- Payment success → redirect to app with Pro unlocked
- Payment failure → error with retry CTA

</details>

---

## Modals & Overlays

<details>
<summary><strong>SCR-22 · Freemium Paywall Modal</strong></summary>

<br>

**Triggered by:** Attempting a 4th JD scan, 3rd mock interview, or any Pro-only feature.

**Key elements:**
- Contextual headline: "You've reached your free limit for JD scans this month"
- What they were trying to do, clearly restated
- What Pro unlocks (short list, 3–4 items)
- Price: ₹299/month
- "Upgrade to Pro" CTA (primary)
- "Not now" / dismiss (secondary — always present)

**Design rule:** Never a hard block. Always dismissable.

</details>

---

<details>
<summary><strong>SCR-23 · Delete Confirmation Modal</strong></summary>

<br>

**Triggered by:** "Delete resume version" or "Delete my account"

**Key elements:**
- Warning message (what will be deleted, permanently)
- "Type DELETE to confirm" input field (for account deletion)
- Red "Confirm delete" button
- "Cancel" button

</details>

---

<details>
<summary><strong>SCR-24 · Onboarding Tooltips (First Session)</strong></summary>

<br>

**Purpose:** Guide first-time users through the resume editor without a separate onboarding flow.

**Tooltip sequence (max 4 steps):**
1. "Upload complete ✅ — Here's your resume. Let's make it better."
2. "Paste a job description here to get your match score."
3. "Click ✨ on any bullet to see AI-suggested rewrites."
4. "Done improving? Try a mock interview for this role →"

**States:**
- Active (first session only)
- Dismissed (user clicks "Got it" or completes all 4 steps — never shown again)

</details>

---

*AI Resume + Interview Coach · Screen Inventory v1.0 · March 2026 · Confidential*
