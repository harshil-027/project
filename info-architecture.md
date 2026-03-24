# 🗺️ Information Architecture
### AI Resume + Interview Coach

> How the product is structured — the hierarchy of pages, flows, and states that a user navigates through from signup to getting a job.

---

| Field | Details |
|-------|---------|
| **Document** | Information Architecture v1.0 |
| **Date** | March 2026 |
| **Scope** | Phase 1 (web app, logged-in experience) |
| **Format** | Site map + user flow descriptions |

---

## Site Map Overview

<details>
<summary><strong>🗂️ Full site map — all pages & states</strong></summary>

<br>

```
AI Resume + Interview Coach
│
├── 🌐 Public (logged out)
│   ├── Landing Page
│   ├── Pricing Page
│   ├── Login / Sign Up
│   └── Blog / SEO content (Phase 3)
│
├── 🏠 Dashboard (home after login)
│   ├── Resume score summary card
│   ├── Last mock interview score card
│   ├── Quick actions: "Improve Resume" / "Start Interview"
│   └── Progress streak indicator
│
├── 📄 Resume Section
│   ├── Upload Resume
│   │   ├── Upload PDF / DOCX
│   │   └── Manual entry fallback form
│   ├── Resume Editor
│   │   ├── Parsed resume view (editable)
│   │   ├── JD input panel (paste job description)
│   │   ├── Match Score panel (0–100 + breakdown)
│   │   ├── Bullet rewriter (per bullet point)
│   │   └── Section feedback panel
│   ├── ATS Checker (Phase 2)
│   └── Version Manager (Phase 2)
│       ├── Saved versions list
│       └── Version diff view
│
├── 🎤 Interview Section
│   ├── Interview Setup
│   │   ├── Select role category (SWE / PM / Design / BA / Marketing)
│   │   └── Select round type (HR / Technical / Behavioural / Final)
│   ├── Active Interview
│   │   ├── Question display
│   │   ├── Text answer input
│   │   └── Voice mode toggle (Phase 2)
│   ├── Interview Debrief
│   │   ├── Overall score
│   │   ├── Per-question breakdown
│   │   └── "What to work on" summary
│   ├── Question Bank Browser
│   │   ├── Domain filter
│   │   ├── Difficulty filter
│   │   └── Question + ideal answer framework view
│   └── Past Interviews History
│
├── 📊 Progress Dashboard (Phase 2)
│   ├── Resume improvement chart (score over time)
│   ├── Interview performance chart
│   ├── Domains practised
│   └── Activity streak
│
└── ⚙️ Account & Settings
    ├── Profile (name, email, target role)
    ├── Subscription (Free / Pro, upgrade CTA)
    ├── Privacy & data settings
    └── Log out
```

</details>

---

## Core User Flows

<details>
<summary><strong>🔄 Flow 1 — New User Onboarding (First Visit to Aha Moment)</strong></summary>

<br>

This is the most critical flow in the product. A new user must reach their "aha moment" — seeing their resume visibly improve — within the first session.

```
Step 1: Land on homepage
        ↓
Step 2: Sign up (email or Google SSO)
        ↓
Step 3: Onboarding prompt — "Upload your resume to get started"
        ↓
Step 4: Upload PDF / DOCX
        ↓
Step 5: AI parses resume → shows structured preview
        ↓
Step 6: Prompt — "Paste a job description you want to apply for"
        ↓
Step 7: User pastes JD → AI runs alignment scan
        ↓
Step 8: Match Score displayed (e.g. 41/100) with breakdown
        ↓
Step 9: AI highlights 3 weakest bullet points → shows 1 rewrite suggestion (free)
        ↓
Step 10: User accepts suggestion → score updates → "aha moment"
        ↓
Step 11: CTA — "See all improvements" (paywall after 5 rewrites)
         or "Try a mock interview for this role" (free, 2/month)
```

**Target time from Step 1 → Step 10:** Under 8 minutes.

**Drop-off risk points:**
- Step 4: If upload fails or is slow → offer manual entry immediately
- Step 7: If JD paste is unclear what to do → show example JD tooltip
- Step 8: If score feels wrong → show "Why this score?" explainer

</details>

<details>
<summary><strong>🔄 Flow 2 — Resume Improvement Loop (Returning User)</strong></summary>

<br>

For a returning user who already has a resume uploaded and wants to tailor it to a new job.

```
Step 1: Log in → land on Dashboard
        ↓
Step 2: See resume score summary card
        ↓
Step 3: Click "Improve for new role"
        ↓
Step 4: Paste new JD → new alignment score generated
        ↓
Step 5: Work through bullet rewrites section by section
        ↓
Step 6: Review section feedback (Summary, Skills, Education)
        ↓
Step 7: Save updated resume (Pro: save as new version with a label)
        ↓
Step 8: Final score displayed → share or download resume
```

</details>

<details>
<summary><strong>🔄 Flow 3 — Mock Interview Flow</strong></summary>

<br>

```
Step 1: Navigate to Interview section from Dashboard or nav
        ↓
Step 2: Select role category (e.g. "Product Management")
        ↓
Step 3: Select round type (e.g. "Behavioural")
        ↓
Step 4: Brief prep screen — "You'll be asked 5–8 questions.
        Answer as if this is a real interview. Take your time."
        ↓
Step 5: First question appears
        ↓
Step 6: User types answer
        ↓
Step 7: AI reads answer → may ask a follow-up OR move to next question
        ↓
       [Repeat Steps 5–7 for 5–8 questions]
        ↓
Step 8: "Interview complete" screen → generating debrief...
        ↓
Step 9: Debrief displayed:
        - Overall score
        - Per-question: score breakdown + specific feedback
        - Summary: "3 things to work on before your next interview"
        ↓
Step 10: CTA — "Practice again" / "Try a different round" / "Improve your resume"
```

**Voice mode (Phase 2):** User can toggle to voice at Step 4. Steps 6–7 become: user speaks → AI transcribes in real time → evaluates audio + content.

</details>

<details>
<summary><strong>🔄 Flow 4 — Upgrade to Pro (Paywall Flow)</strong></summary>

<br>

Paywalls are triggered at the moment of highest intent — never before the user has experienced value.

```
Trigger: User attempts their 4th JD scan in a month (free limit: 3)
         OR attempts their 3rd mock interview in a month (free limit: 2)
         OR clicks "See full ATS report" (Phase 2)
         ↓
Step 1: Soft paywall modal appears
        — Shows what they were about to do
        — Shows what Pro unlocks (unlimited + voice + all domains)
        — Price: ₹299/month displayed prominently
        ↓
Step 2: "Upgrade to Pro" CTA → Pricing page
        OR "Not now" → dismiss modal, return to current state
        ↓
Step 3: Pricing page — Free vs Pro comparison table
        ↓
Step 4: Click "Get Pro" → Payment flow (Razorpay / Stripe)
        ↓
Step 5: Payment confirmed → Pro features unlocked immediately
        ↓
Step 6: Return to where they were before the paywall
```

**Key principle:** The paywall is never a dead end. The user always has a "not now" option and retains access to their free tier.

</details>

---

## Navigation Structure

<details>
<summary><strong>🧭 Primary navigation (logged-in state)</strong></summary>

<br>

The main navigation is a persistent left sidebar (desktop) / bottom tab bar (mobile):

| Nav Item | Icon | Destination |
|----------|------|-------------|
| Home | 🏠 | Dashboard |
| Resume | 📄 | Resume editor / upload |
| Interview | 🎤 | Interview setup / history |
| Progress | 📊 | Progress dashboard *(Phase 2)* |
| Account | 👤 | Profile, subscription, settings |

**Secondary navigation within Resume section:**
- Editor → ATS Checker *(Phase 2)* → Version Manager *(Phase 2)*

**Secondary navigation within Interview section:**
- Setup → Active Interview → Debrief → History
- Question Bank (always accessible as a browse mode)

</details>

<details>
<summary><strong>🔔 Notification & prompt architecture</strong></summary>

<br>

| Trigger | Prompt Type | Message |
|---------|------------|---------|
| User hasn't logged in for 3 days | Email nudge | "Your resume is still at 41/100. Here's one quick fix." |
| User completes first resume improvement | In-app toast | "Nice work! Try a mock interview for this role →" |
| User hits free tier limit | Soft paywall modal | Described in Flow 4 |
| User completes 3 mock interviews | In-app prompt | "You've practised 3 times. Check your progress →" |
| User's score improves by 20+ points | In-app celebration | "Your resume jumped from 41 → 71. Share your progress?" |

</details>

---

## Page Hierarchy Summary

<details>
<summary><strong>📐 Depth map — how many clicks from home?</strong></summary>

<br>

| Page / Screen | Clicks from Dashboard |
|---------------|-----------------------|
| Resume Editor | 1 |
| JD Alignment Score | 2 (Resume → paste JD) |
| Bullet Rewriter | 2 (Resume → bullet) |
| Section Feedback | 2 (Resume → section) |
| ATS Checker *(Phase 2)* | 2 (Resume → ATS tab) |
| Version Manager *(Phase 2)* | 2 (Resume → Versions tab) |
| Interview Setup | 1 |
| Active Interview | 2 (Interview → Start) |
| Interview Debrief | auto (after interview ends) |
| Question Bank | 2 (Interview → Browse) |
| Progress Dashboard *(Phase 2)* | 1 |
| Pricing / Upgrade | 1 (from any paywall prompt) |
| Account Settings | 1 |

**Design principle:** No core action should be more than 2 clicks from the dashboard. The product is tool-first, not content-first — users come here to do something, not to browse.

</details>

---

*AI Resume + Interview Coach · Information Architecture v1.0 · March 2026 · Confidential*
