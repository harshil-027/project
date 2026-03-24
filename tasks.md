# ✅ Project Tasks — Phase 1 MVP
### AI Resume + Interview Coach

> 15 tasks structured for GitHub Projects. Each task maps to a feature from the PRD and includes acceptance criteria, labels, and effort estimates so you can manage this solo without losing track.

---

## How to use this in GitHub Projects

1. Go to your repo → **Projects** → **New project** → choose **Board** view
2. Create 4 columns: `Backlog` · `In Progress` · `In Review` · `Done`
3. Create each task below as an **Issue** in your repo
4. Add the labels listed on each task (create them in Settings → Labels)
5. Drag issues onto the board

**Label colour guide to create in GitHub:**
| Label | Colour | Meaning |
|-------|--------|---------|
| `pillar: resume` | `#1A56DB` (blue) | Resume Intelligence features |
| `pillar: interview` | `#7F77DD` (purple) | Interview Coaching features |
| `type: setup` | `#888780` (gray) | Infrastructure / project setup |
| `type: auth` | `#888780` (gray) | Auth & onboarding |
| `priority: p0` | `#E24B4A` (red) | Must-have at launch |
| `priority: p1` | `#BA7517` (amber) | Launch-soon |
| `effort: S` | `#1D9E75` (teal) | Small — under 1 day |
| `effort: M` | `#1D9E75` (teal) | Medium — 1–3 days |
| `effort: L` | `#1D9E75` (teal) | Large — 3–5 days |

---

## Task List

---

### TASK-01 · Project Setup & Tech Stack Init
**Labels:** `type: setup` `effort: S`
**Priority:** P0 · **Column:** Backlog

**Description:**
Initialise the repository with the chosen tech stack, folder structure, linting, environment config, and CI pipeline. This is the foundation everything else builds on.

**Acceptance criteria:**
- [ ] Repo initialised with chosen framework (e.g. Next.js / React + Node)
- [ ] `.env.example` file created with all required environment variable keys
- [ ] ESLint + Prettier configured and passing
- [ ] Basic CI pipeline (GitHub Actions) runs lint + build on every PR
- [ ] `README.md` updated with local setup instructions
- [ ] Folder structure matches the screen inventory (`/pages`, `/components`, `/api`)

---

### TASK-02 · Authentication — Sign Up & Login
**Labels:** `type: auth` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
Implement user authentication with Google SSO and email/password. Users must be able to create an account, log in, and be redirected to the dashboard.

**Acceptance criteria:**
- [ ] Google OAuth sign-up and login working
- [ ] Email + password sign-up with validation (min 8 chars, email format)
- [ ] Forgot password flow sends reset email
- [ ] Auth state persists on page refresh (JWT or session cookie)
- [ ] Unauthenticated users are redirected to login from protected routes
- [ ] Error states handled: wrong password, email already exists

---

### TASK-03 · Resume Upload & Parse
**Labels:** `pillar: resume` `priority: p0` `effort: L`
**Priority:** P0 · **Column:** Backlog

**Description:**
Users can upload a PDF or DOCX resume. The backend parses the file and extracts structured data (contact info, experience, education, skills, summary). Parsed data is displayed in an editable preview.

**Acceptance criteria:**
- [ ] PDF and DOCX uploads accepted, max 5MB, other formats rejected with clear error
- [ ] Parsing completes and structured preview renders within 10 seconds
- [ ] Each parsed field is editable inline by the user
- [ ] Fallback manual entry form available if parse fails
- [ ] Resume data saved to user's account (persists across sessions)
- [ ] Parsing success rate ≥ 90% tested against 10 common resume templates

---

### TASK-04 · JD Input & Alignment Score
**Labels:** `pillar: resume` `priority: p0` `effort: L`
**Priority:** P0 · **Column:** Backlog

**Description:**
Users paste a job description. The AI compares the resume against the JD and returns a 0–100 match score with a breakdown by category (keywords, skills, experience) and a list of missing keywords.

**Acceptance criteria:**
- [ ] JD text area accepts up to 5,000 characters
- [ ] "Analyse" button triggers the scan; result returns within 8 seconds
- [ ] Match score (0–100) displayed with visual gauge
- [ ] Score breakdown shows minimum 3 sub-categories
- [ ] Missing keywords listed and ranked by JD frequency
- [ ] Score is consistent: same resume + JD = same score (±2 tolerance)
- [ ] Free tier: 3 scans/month enforced; paywall modal shown on attempt 4

---

### TASK-05 · AI Bullet Point Rewriter
**Labels:** `pillar: resume` `priority: p0` `effort: L`
**Priority:** P0 · **Column:** Backlog

**Description:**
Each bullet point in the experience section has an "Improve" button. Clicking it sends the bullet + JD context to the AI and returns 2–3 rewrite suggestions with labels (e.g. "Added metric", "JD-aligned"). Users can accept, reject, or edit inline.

**Acceptance criteria:**
- [ ] Every experience bullet has a visible "Improve" button
- [ ] Suggestions return within 4 seconds of clicking "Improve"
- [ ] 2–3 options displayed, each with an improvement label
- [ ] "Best match for this JD" badge shown on the recommended option
- [ ] Accept / Reject / Edit inline actions all work correctly
- [ ] Accepted suggestions saved and counted toward "resumes improved" metric
- [ ] Free limit: 5 rewrites/session enforced with upgrade prompt on attempt 6
- [ ] If no JD scanned: rewrites are general; if JD scanned: rewrites are JD-specific

---

### TASK-06 · Resume Section Feedback Panel
**Labels:** `pillar: resume` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
A panel that reviews the resume at section level: Summary, Experience, Skills, Education, and Formatting. Each section gets a score (Weak / Fair / Strong) and 2–4 specific, actionable suggestions.

**Acceptance criteria:**
- [ ] Minimum 4 sections reviewed: Summary, Experience, Skills, Education
- [ ] Each section shows a score badge and label (Weak / Fair / Strong)
- [ ] Each section has minimum 2 specific suggestions (not generic)
- [ ] Suggestions reference JD content when a JD has been scanned
- [ ] Formatting feedback flags: page length, section order, white space
- [ ] Full review loads within 10 seconds

---

### TASK-07 · Freemium Access Controls & Paywall
**Labels:** `type: setup` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
Implement usage tracking and paywall logic for all free tier limits. Free limits: 1 active resume, 3 JD scans/month, 5 bullet rewrites/session, 2 mock interviews/month, 1 question bank domain.

**Acceptance criteria:**
- [ ] Usage counters tracked per user per month in the database
- [ ] Paywall modal appears at correct trigger points (not before)
- [ ] Paywall modal is always dismissable with a "Not now" option
- [ ] Pro users bypass all limits correctly
- [ ] Limits reset on the 1st of each calendar month
- [ ] Usage state shown in the account/settings page ("2 of 3 JD scans used")

---

### TASK-08 · Interview Setup Screen
**Labels:** `pillar: interview` `priority: p0` `effort: S`
**Priority:** P0 · **Column:** Backlog

**Description:**
Screen where users configure a mock interview before starting. They select a role category (5 options) and a round type (4 options). Shows estimated duration and entry point to the active interview.

**Acceptance criteria:**
- [ ] 5 role categories selectable: SWE, PM, Business Analyst, Marketing, Design
- [ ] 4 round types selectable: HR Screening, Technical, Behavioural, Final Round
- [ ] "Start Interview" CTA disabled until both selections are made
- [ ] Estimated duration shown: "~15–20 minutes"
- [ ] Free user interview counter shown: "1 of 2 free interviews used this month"
- [ ] "Browse questions" secondary link navigates to question bank

---

### TASK-09 · Active Mock Interview — Text Mode
**Labels:** `pillar: interview` `priority: p0` `effort: L`
**Priority:** P0 · **Column:** Backlog

**Description:**
The core interview experience. AI asks 5–8 role-specific questions dynamically, follows up on user answers at least once per question, and scores responses on 4 dimensions. Session auto-saves.

**Acceptance criteria:**
- [ ] Interview runs 5–8 questions for the selected role + round combination
- [ ] At least 1 dynamic follow-up question generated per answer (based on actual answer content)
- [ ] AI does not repeat the same question in a single session
- [ ] No score or feedback shown during the active interview
- [ ] "End early" option available; partial debrief generated if used
- [ ] Session auto-saves to database if user closes browser mid-interview
- [ ] Free limit: 2 sessions/month enforced

---

### TASK-10 · Interview Debrief Screen
**Labels:** `pillar: interview` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
Post-interview screen showing overall score, per-question breakdown with scores across 4 dimensions (Relevance, Structure, Depth, Clarity), and a "What to work on" summary with top 3 improvement areas.

**Acceptance criteria:**
- [ ] Overall score (0–100) displayed with a label (Needs Work / Developing / Strong)
- [ ] Per-question breakdown: question text + user's answer (collapsed) + 4 dimension scores + specific feedback text
- [ ] "What to work on" summary: exactly 3 improvement areas with actionable wording
- [ ] CTAs: "Practice again", "Try different round", "Improve your resume"
- [ ] Debrief saves to interview history
- [ ] Partial debrief generated correctly if session was ended early

---

### TASK-11 · Role-Specific Question Banks
**Labels:** `pillar: interview` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
Seed the database with question banks for all 5 launch domains. Build the browsable question bank UI with domain and difficulty filters. Free users see 1 domain; Pro sees all 5.

**Acceptance criteria:**
- [ ] Minimum 50 questions per domain (250 total at launch)
- [ ] Questions tagged by: domain, sub-category, difficulty (Entry / Mid / Senior)
- [ ] Browse mode shows question + "Ideal answer framework" (expandable)
- [ ] Domain filter and difficulty filter both work correctly
- [ ] Free user: 1 domain visible, others show upgrade prompt
- [ ] "Practise this question" CTA launches a single-question mini-interview

---

### TASK-12 · Main Dashboard
**Labels:** `type: setup` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
The landing screen after login. Shows resume score summary, last interview score, quick action strip, streak indicator, and upgrade banner for free users. Empty state for first-time users.

**Acceptance criteria:**
- [ ] Resume card: active resume name + last JD match score + "Improve" CTA
- [ ] Interview card: last session score + role + "Practice again" CTA
- [ ] Quick actions: "Upload resume" / "Start interview" / "Browse questions"
- [ ] Streak indicator shows consecutive active days
- [ ] Empty state shown correctly for first-time users with clear onboarding CTA
- [ ] Upgrade banner shown for free users; hidden for Pro users
- [ ] Dashboard loads within 3 seconds

---

### TASK-13 · Onboarding Tooltips (First Session)
**Labels:** `type: setup` `priority: p0` `effort: S`
**Priority:** P0 · **Column:** Backlog

**Description:**
A 4-step tooltip sequence that guides first-time users through the resume editor without a separate onboarding flow. Shown once per user; dismissed permanently after completion or skip.

**Acceptance criteria:**
- [ ] 4 tooltips shown in sequence: upload confirmation → JD input → bullet improve → interview CTA
- [ ] "Got it" / "Skip tour" dismisses the tooltip and marks it complete in the database
- [ ] Tooltips never shown again after dismissal (flag stored per user)
- [ ] Tooltips do not block critical UI elements
- [ ] Tooltip sequence works correctly on mobile viewport

---

### TASK-14 · Pricing Page & Pro Upgrade Flow
**Labels:** `type: setup` `priority: p0` `effort: M`
**Priority:** P0 · **Column:** Backlog

**Description:**
Build the pricing page with the Free vs Pro comparison table, and wire up the upgrade flow through a payment provider (Razorpay for India / Stripe for international). Pro features unlock immediately after payment.

**Acceptance criteria:**
- [ ] Pricing page shows full Free vs Pro feature comparison table
- [ ] Price displayed in both INR (₹299) and USD ($4.99)
- [ ] Student discount field: valid `.edu` email → 3 months free applied
- [ ] Payment flow completes and user's account is upgraded within 60 seconds of payment
- [ ] Payment failure shows clear error with retry CTA
- [ ] Pro status persists correctly; cancellation downgrades at end of billing period
- [ ] Paywall modal "Upgrade to Pro" CTA routes correctly to pricing page with context

---

### TASK-15 · Analytics & KPI Instrumentation
**Labels:** `type: setup` `priority: p0` `effort: S`
**Priority:** P0 · **Column:** Backlog

**Description:**
Instrument the key events needed to track the North Star metric (resumes improved/week) and the Phase 1 OKRs. Without this, we cannot tell if the product is working.

**Acceptance criteria:**
- [ ] `resume_improved` event fired when user accepts any AI suggestion (bullet or section)
- [ ] `jd_scanned` event fired on every alignment scan
- [ ] `interview_completed` event fired when debrief is generated
- [ ] `paywall_shown` and `paywall_converted` events tracked per trigger point
- [ ] `session_started` and `user_signed_up` events tracked
- [ ] Dashboard or analytics tool (e.g. PostHog / Mixpanel free tier) shows live event stream
- [ ] Weekly "resumes improved" count queryable from day 1

---

## Task Summary

| Task | Area | Priority | Effort | Status |
|------|------|----------|--------|--------|
| TASK-01 · Project setup | Setup | P0 | S | Backlog |
| TASK-02 · Auth (sign up / login) | Auth | P0 | M | Backlog |
| TASK-03 · Resume upload & parse | Resume | P0 | L | Backlog |
| TASK-04 · JD input & alignment score | Resume | P0 | L | Backlog |
| TASK-05 · AI bullet rewriter | Resume | P0 | L | Backlog |
| TASK-06 · Section feedback panel | Resume | P0 | M | Backlog |
| TASK-07 · Freemium access controls | Setup | P0 | M | Backlog |
| TASK-08 · Interview setup screen | Interview | P0 | S | Backlog |
| TASK-09 · Active mock interview | Interview | P0 | L | Backlog |
| TASK-10 · Interview debrief | Interview | P0 | M | Backlog |
| TASK-11 · Question banks | Interview | P0 | M | Backlog |
| TASK-12 · Main dashboard | Setup | P0 | M | Backlog |
| TASK-13 · Onboarding tooltips | Setup | P0 | S | Backlog |
| TASK-14 · Pricing page & upgrade flow | Setup | P0 | M | Backlog |
| TASK-15 · Analytics instrumentation | Setup | P0 | S | Backlog |

**Total effort estimate:** 3S + 7M + 4L ≈ **8–10 weeks solo** (assuming 1 large = 4 days, 1 medium = 2 days, 1 small = 1 day, working 5 days/week)

---

*AI Resume + Interview Coach · Phase 1 Task List · March 2026*
