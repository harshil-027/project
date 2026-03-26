# Development Plan
## AI Resume + Interview Coach

---

## Overview

This is the 4-week MVP development plan for AI Resume + Interview Coach. Every task is assigned to a specific week and has a clear deliverable. The plan is structured so the foundation is rock solid in Week 1, the two core pillars (Resume Intelligence and Interview Coaching) are built in parallel in Weeks 2 and 3, and Week 4 is reserved entirely for polish, bug fixes, and demo prep.

**Timeline:** 4 weeks
**Builder:** Solo
**MVP Goal:** Working product where a student can upload their resume, paste a job description, get AI-powered feedback and bullet rewrites, run a dynamic mock interview, receive a scored debrief, and upgrade to Pro — all in a single session.

---

## Tech Stack

| Layer | Choice | Reason |
|-------|--------|--------|
| **Frontend** | Next.js (App Router) | File-based routing, SSR, easy API routes |
| **Backend** | Next.js API Routes + Node.js | Keeps stack unified, no separate server |
| **Database** | Supabase (PostgreSQL) | Auth built-in, RLS, real-time, free tier |
| **AI — Resume** | OpenAI GPT-4o | Best instruction-following for JD alignment |
| **AI — Interview** | OpenAI GPT-4o | Dynamic follow-up quality is critical |
| **AI — Transcription** | OpenAI Whisper | Voice mode (Phase 2, scaffolded in Week 3) |
| **Embeddings** | OpenAI text-embedding-3-small | For question bank semantic search |
| **File parsing** | pdf-parse + mammoth | PDF and DOCX resume extraction |
| **Payments** | Razorpay (India) + Stripe (global) | ₹299 price point requires local payment |
| **Analytics** | PostHog (free tier) | Event tracking for North Star metric |
| **Hosting** | Vercel | Zero-config Next.js deployment |

---

## Week 1 — Foundation & API Contracts

> Goal: Auth works. Database is live. Resume upload and parse works. Every API route is scaffolded. No AI calls yet — infrastructure and contracts only.

---

### Setup & Infrastructure
- [ ] Initialise Next.js project with App Router — folder structure, TypeScript, ESLint, Prettier
- [ ] Create `.env.local` with all required keys: `OPENAI_API_KEY`, `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`, `RAZORPAY_KEY_ID`, `RAZORPAY_KEY_SECRET`, `POSTHOG_KEY`
- [ ] Connect Supabase — verify connection from Next.js
- [ ] Set up Supabase Auth — email/password + Google OAuth configured
- [ ] Create JWT middleware for all protected API routes
- [ ] Set up GitHub Actions CI — lint + build check on every push
- [ ] Configure Vercel deployment — staging environment live

**Deliverable:** Running Next.js project, Supabase connected, CI passing, staging URL live.

---

### Database Schema
Create all tables in Supabase with RLS enabled:

- [ ] `users` — id, email, name, plan (free/pro), usage_counts (JSONB), created_at
- [ ] `resumes` — id, user_id, file_url, parsed_content (JSONB), created_at, is_active
- [ ] `jd_scans` — id, user_id, resume_id, jd_text, match_score, breakdown (JSONB), missing_keywords (array), created_at
- [ ] `bullet_rewrites` — id, user_id, resume_id, jd_scan_id, original_bullet, suggestions (JSONB), accepted_suggestion, created_at
- [ ] `interview_sessions` — id, user_id, role_category, round_type, status, started_at, ended_at
- [ ] `interview_messages` — id, session_id, role (ai/user), content, scores (JSONB), created_at
- [ ] `interview_debriefs` — id, session_id, overall_score, dimension_scores (JSONB), improvements (array), created_at
- [ ] `questions` — id, domain, subcategory, difficulty, question_text, ideal_framework, created_at
- [ ] `subscriptions` — id, user_id, plan, status, started_at, expires_at, payment_provider, payment_id
- [ ] `analytics_events` — id, user_id, event_name, properties (JSONB), created_at
- [ ] Enable Row-Level Security on all tables — users can only read/write their own rows

**Deliverable:** All tables created, RLS policies verified, schema documented.

---

### Auth Endpoints
- [ ] `POST /api/auth/register` — email + password signup, creates user row
- [ ] `POST /api/auth/login` — returns session token
- [ ] `GET /api/auth/me` — returns current user + plan + usage counts
- [ ] `POST /api/auth/logout` — clears session
- [ ] Google OAuth callback route working end-to-end
- [ ] Middleware: redirect unauthenticated users from all `/dashboard/*` routes to `/login`

**Deliverable:** Full auth flow working — sign up, log in, Google SSO, protected routes.

---

### Resume Upload & Parse
- [ ] `POST /api/resume/upload` — accepts PDF or DOCX (max 5MB), rejects other formats with clear error
- [ ] File storage: upload to Supabase Storage bucket `resumes/{user_id}/{filename}`
- [ ] PDF parsing: `pdf-parse` extracts raw text from PDF
- [ ] DOCX parsing: `mammoth` extracts raw text from DOCX
- [ ] Parsing success rate: test against 10 common resume templates — target ≥ 90%
- [ ] `POST /api/resume/parse` — takes raw text → GPT-4o prompt → structured JSON (contact, summary, experience[], education[], skills[])
- [ ] `GET /api/resume/:id` — returns parsed resume for current user
- [ ] `PATCH /api/resume/:id` — updates any field (user edits inline)
- [ ] Fallback: if parse fails, return empty structure so user can fill manually
- [ ] Test: upload 5 real resume files, verify structured output

**Deliverable:** Upload → parse → structured JSON working. Parsed data stored in `resumes` table.

---

### Scaffold All Remaining Routes
All routes below return `200 { status: "not implemented" }` — no logic yet. This lets the frontend build against real endpoints from Week 2.

- [ ] `POST /api/jd/scan`
- [ ] `POST /api/resume/rewrite-bullet`
- [ ] `GET /api/resume/section-feedback`
- [ ] `POST /api/interview/start`
- [ ] `POST /api/interview/:id/message`
- [ ] `POST /api/interview/:id/end`
- [ ] `GET /api/interview/:id/debrief`
- [ ] `GET /api/questions` (with domain + difficulty filters)
- [ ] `POST /api/payments/create-order`
- [ ] `POST /api/payments/verify`
- [ ] `GET /api/usage` (returns user's monthly usage counts)
- [ ] `POST /api/analytics/event`

**Deliverable:** All routes return 200. Frontend can start building without waiting for logic.

---

### Frontend — Auth Screens
- [ ] `/login` — email/password form + Google SSO button, error states handled
- [ ] `/signup` — email/password form + Google SSO, inline validation
- [ ] `/forgot-password` — email input → sends reset link
- [ ] Auth state persists on page refresh
- [ ] Loading states on all form submissions

**Deliverable:** Auth screens fully usable. User can sign up, log in, log out.

---

## Week 2 — Resume Intelligence Pillar

> Goal: The JD alignment score works. Bullet rewrites are live. Section feedback is live. The aha moment — upload resume, paste JD, see score improve — is working end to end.

---

### JD Alignment Score
- [ ] Implement `POST /api/jd/scan` — full logic
- [ ] Prompt: resume text + JD text → GPT-4o → match score (0–100) + breakdown by category (keywords, skills, experience, tone) + missing keywords ranked by JD frequency
- [ ] Score calibration: test 10 resume + JD pairs — zero overlap must score below 20, strong match must score above 75
- [ ] Store result in `jd_scans` table with breakdown JSONB
- [ ] Response includes: `match_score`, `breakdown`, `missing_keywords[]`, `scan_id`
- [ ] Response time target: under 8 seconds — test on slow connection
- [ ] Track `jd_scanned` event to PostHog on every call
- [ ] Free tier enforcement: check `usage_counts.jd_scans_this_month` — reject with `402` if ≥ 3

**Deliverable:** JD scan returns accurate score + keywords in under 8 seconds. Free limit enforced.

---

### AI Bullet Point Rewriter
- [ ] Implement `POST /api/resume/rewrite-bullet` — full logic
- [ ] Inputs: `bullet_text`, `resume_context` (role + company), `jd_scan_id` (optional), `user_id`
- [ ] Prompt: original bullet + JD context (if available) → GPT-4o → 3 rewrites each with improvement label (`added_metric`, `stronger_verb`, `jd_aligned`, `star_format`)
- [ ] Mark one rewrite as `recommended: true` (highest JD alignment if JD scanned, else strongest impact)
- [ ] Store in `bullet_rewrites` table
- [ ] Response time target: under 4 seconds
- [ ] `PATCH /api/resume/rewrite-bullet/:id/accept` — saves accepted suggestion, fires `resume_improved` event to PostHog
- [ ] Free tier enforcement: check `usage_counts.rewrites_this_session` — reject with `402` if ≥ 5
- [ ] Test: 20 real bullet points across SWE, PM, marketing roles — review output quality

**Deliverable:** Bullet rewriter returns 3 JD-specific suggestions in under 4 seconds. Accepted suggestions tracked.

---

### Resume Section Feedback
- [ ] Implement `GET /api/resume/section-feedback?resume_id=X&jd_scan_id=Y`
- [ ] Prompt: full parsed resume + JD (if available) → GPT-4o → section scores + suggestions for Summary, Experience, Skills, Education, Formatting
- [ ] Each section: `score` (0–10), `label` (Weak/Fair/Strong), `suggestions[]` (min 2, specific not generic)
- [ ] Suggestions must reference JD content when `jd_scan_id` is provided
- [ ] Response time target: under 10 seconds
- [ ] Test: run on 5 real resumes, verify suggestions are specific (not "use action verbs")

**Deliverable:** Section feedback returns specific, JD-aware suggestions for all 5 sections.

---

### Freemium Access Controls
- [ ] Middleware function `checkUsageLimit(userId, limitType)` — reads from `users.usage_counts`
- [ ] Limits enforced: `jd_scans` (3/month), `rewrites_per_session` (5), `mock_interviews` (2/month)
- [ ] Usage increment function `incrementUsage(userId, eventType)` — called after each successful AI call
- [ ] Monthly reset: Supabase scheduled function resets `usage_counts` on 1st of each month
- [ ] `GET /api/usage` — returns current usage counts for the logged-in user
- [ ] Pro check: `subscriptions` table queried — active Pro subscription bypasses all limits
- [ ] All limit rejections return `{ error: "limit_reached", limit_type: "jd_scans", upgrade_url: "/pricing" }`

**Deliverable:** All free limits enforced. Pro users bypass correctly. Monthly reset working.

---

### Frontend — Resume Screens
- [ ] `/dashboard/resume/upload` — drag-and-drop zone, accepts PDF/DOCX, shows parse progress, error states
- [ ] `/dashboard/resume/editor` — two-panel layout (resume preview left, feedback/JD panel right)
- [ ] Resume editor: each bullet has inline "Improve" button
- [ ] JD input panel: textarea + "Analyse" button, match score gauge renders after scan
- [ ] Score breakdown: 3 sub-categories shown with percentages
- [ ] Missing keywords list: ranked, copyable
- [ ] Bullet rewrite card: 3 options with improvement labels, Accept/Reject/Edit inline
- [ ] Section feedback panel: accordion per section, score badge + suggestions
- [ ] Free tier UI: usage counter ("2 of 3 JD scans used this month")
- [ ] Paywall modal: context-aware message, ₹299 price, "Not now" always visible

**Deliverable:** Full resume editor usable end-to-end. Aha moment (upload → JD → score → rewrite) works in browser.

---

## Week 3 — Interview Coaching Pillar

> Goal: Dynamic mock interview works end to end. Debrief is scored and specific. Question banks are seeded. All screens are usable. Voice mode is scaffolded for Phase 2.

---

### Question Bank Seeding
- [ ] Seed `questions` table: minimum 50 questions per domain × 5 domains = 250 questions total
- [ ] Domain 1 — SWE: DSA (15), System Design (20), Behavioural (15)
- [ ] Domain 2 — PM: Product Sense (15), Execution (15), Metrics (10), Estimation (10)
- [ ] Domain 3 — Business Analyst: Case-style (20), Communication (15), Excel/data (15)
- [ ] Domain 4 — Marketing: Campaign (15), Analytics (15), GTM (10), Brand (10)
- [ ] Domain 5 — Design: Portfolio Critique (15), Process (20), Design Challenge (15)
- [ ] Each question has: `domain`, `subcategory`, `difficulty` (entry/mid/senior), `question_text`, `ideal_framework`
- [ ] `GET /api/questions` — filterable by `domain`, `difficulty`, `subcategory`
- [ ] Free tier: domain filter allows 1 domain only; additional domains return `402`
- [ ] Semantic search: embed all questions with `text-embedding-3-small`, store in pgvector — enables "find similar questions" in future

**Deliverable:** 250 questions seeded. Questions API working with filters. Free domain limit enforced.

---

### Mock Interview Engine
- [ ] Implement `POST /api/interview/start` — creates `interview_sessions` row, returns `session_id` + first question drawn from question bank by domain + round_type
- [ ] Question selection: pull 8 questions for the session, shuffle, store as session queue
- [ ] No repeat questions: track asked question IDs in session, never re-ask
- [ ] Implement `POST /api/interview/:id/message` — core interview loop
  - Receives: `user_answer` (text)
  - Step 1: evaluate if a follow-up is warranted (vague answer, missing specifics, no example given)
  - Step 2a: if follow-up needed → generate dynamic follow-up referencing actual answer content
  - Step 2b: if answer sufficient → move to next question in queue
  - Step 3: score the answer silently (do not show during session): Relevance (0–10), Structure (0–10), Depth (0–10), Clarity (0–10)
  - Step 4: store message + scores in `interview_messages`
  - Returns: `{ type: "follow_up" | "next_question", content: "...", question_number: N, total: 8 }`
- [ ] Session auto-save: Supabase real-time subscription keeps session state — browser close does not lose progress
- [ ] `POST /api/interview/:id/end` — marks session complete, triggers debrief generation
- [ ] Response time target: under 3 seconds per AI response (critical for interview feel)
- [ ] Test: run 3 full interview sessions across different domains, review follow-up quality

**Deliverable:** Dynamic mock interview runs 8 questions with real follow-ups. Session auto-saves. No question repeats.

---

### Interview Debrief
- [ ] Implement `GET /api/interview/:id/debrief`
- [ ] If debrief not yet generated, trigger generation synchronously (first request)
- [ ] Debrief generation prompt: all Q&A pairs from session → GPT-4o → per-question scores + feedback + overall score + top 3 improvements
- [ ] Overall score: weighted average (Relevance 30%, Structure 30%, Depth 25%, Clarity 15%)
- [ ] Label: 0–40 = "Needs Work", 41–65 = "Developing", 66–100 = "Strong"
- [ ] Per-question feedback: 2–3 sentences, specific (references what the user actually said), never generic
- [ ] "What to work on": exactly 3 improvement areas, actionable wording ("Your answers lack specific metrics — try the XYZ framework: Accomplished X by doing Y, measured by Z")
- [ ] Store in `interview_debriefs` table
- [ ] Track `interview_completed` event to PostHog

**Deliverable:** Debrief returns scored, specific, per-question feedback. "What to work on" is always 3 actionable items.

---

### Payments — Razorpay + Stripe
- [ ] `POST /api/payments/create-order` — creates Razorpay order (India) or Stripe PaymentIntent (international) based on user's locale
- [ ] `POST /api/payments/verify` — verifies Razorpay signature or Stripe webhook, upgrades user to Pro in `subscriptions` table
- [ ] Razorpay: ₹299/month order creation working, payment modal integration in frontend
- [ ] Stripe: $4.99/month PaymentIntent working
- [ ] Student discount: `.edu` email detected → apply 3-month free coupon before payment
- [ ] Webhook handler: Razorpay + Stripe webhooks update subscription status on renewal/cancellation
- [ ] Cancellation: sets `subscriptions.status = cancelled`, plan downgrades at `expires_at`
- [ ] Test: full payment flow with Razorpay test credentials, verify Pro unlocks immediately

**Deliverable:** Payment flow works end-to-end. Pro unlocks within 60 seconds of payment. Student discount applies.

---

### Analytics Instrumentation
- [ ] PostHog client initialised in Next.js (`posthog-js`)
- [ ] Server-side PostHog for API route events (`posthog-node`)
- [ ] Events firing correctly:
  - `user_signed_up` — on registration
  - `resume_uploaded` — on successful parse
  - `jd_scanned` — on every scan, with `{ had_jd: true, match_score: N }`
  - `resume_improved` — on bullet accept, with `{ suggestion_type, had_jd }`
  - `interview_started` — with `{ domain, round_type }`
  - `interview_completed` — with `{ domain, overall_score, completed_questions }`
  - `paywall_shown` — with `{ trigger_point, limit_type }`
  - `paywall_converted` — on successful upgrade
- [ ] PostHog dashboard: "Resumes improved / week" saved as pinned insight (North Star)
- [ ] No PII in any event payload (no email, name, resume content)
- [ ] Test: trigger every event, verify in PostHog live events view

**Deliverable:** All 8 events firing. North Star metric queryable from day 1.

---

### Voice Mode Scaffold (Phase 2)
- [ ] Scaffold `POST /api/interview/:id/transcribe` — accepts audio blob, returns `{ transcript: "" }` placeholder
- [ ] Whisper integration tested locally with a sample audio file — confirm it works
- [ ] Frontend: voice toggle button present in interview UI, disabled with "Coming soon" tooltip
- [ ] Architecture decision: confirm latency budget (under 2 seconds) is achievable with Whisper on current infra
- [ ] Document what needs to be built to activate voice mode (checklist for Phase 2 Week 1)

**Deliverable:** Voice endpoint scaffolded. Whisper tested. Phase 2 activation path documented.

---

### Frontend — Interview Screens
- [ ] `/dashboard/interview/setup` — role category selector (5 cards), round type selector (4 options), "Start" CTA disabled until both selected
- [ ] `/dashboard/interview/session` — clean single-question view, text answer textarea, question counter ("3 of 8"), "End early" link, voice toggle (disabled)
- [ ] `/dashboard/interview/debrief` — overall score ring, per-question accordion (question → answer → 4 scores → feedback text), "What to work on" section, 3 CTAs
- [ ] `/dashboard/interview/questions` — question bank browser, domain tabs, difficulty filter, each card expandable to show ideal framework, "Practise this" CTA
- [ ] `/dashboard/interview/history` — list of past sessions with date, role, score, click to re-open debrief
- [ ] All interview screens: free usage counter visible ("1 of 2 interviews used this month")

**Deliverable:** All interview screens usable. Full interview loop (setup → session → debrief) works in browser.

---

### Frontend — Remaining Screens
- [ ] `/dashboard` — main dashboard: resume score card, last interview card, quick actions strip, streak counter, upgrade banner for free users
- [ ] `/pricing` — Free vs Pro comparison table, ₹299 price, student discount field, Razorpay payment modal
- [ ] `/dashboard/account` — profile (name, email), subscription status, usage summary, cancel subscription
- [ ] Onboarding tooltips — 4-step sequence on first login: upload → JD input → bullet improve → interview CTA
- [ ] All screens: mobile-responsive at 375px+, tested in Chrome DevTools

**Deliverable:** All 24 screens from screen inventory usable. Mobile-responsive verified.

---

## Week 4 — Bug Fixes, Polish & Demo Prep

> Goal: Clean, working demo. No new features. Fix every P0 bug. Polish core flows. Prepare for real users.

---

### Bug Fixes

| Task | Area |
|------|------|
| Fix all P0 bugs found during Week 3 self-QA | All |
| Fix any broken auth edge cases (token expiry, Google OAuth failure) | Auth |
| Fix resume parse failures on edge case formats | Resume |
| Fix any AI response format inconsistencies (null fields, missing data) | AI |
| Fix payment webhook failures or race conditions | Payments |
| Fix all mobile layout breaks at 375px | Frontend |
| Fix any interview session state loss on page refresh | Interview |

---

### QA Checklist — Run Everything

- [ ] Auth flow: sign up → log in → Google SSO → forgot password → session persistence
- [ ] Resume flow: upload PDF → upload DOCX → parse preview → inline edit → manual fallback
- [ ] JD flow: paste JD → score returned in under 8s → breakdown correct → missing keywords accurate
- [ ] Bullet rewriter: click Improve → 3 suggestions in under 4s → labels correct → Accept saves → free limit blocks at attempt 6
- [ ] Section feedback: full review in under 10s → suggestions specific (not generic) → JD-aware when JD scanned
- [ ] Freemium limits: JD scans block at 4th attempt → interview blocks at 3rd → rewrites block at 6th → all show paywall modal
- [ ] Payment: Razorpay test payment completes → Pro unlocks immediately → usage limits bypassed
- [ ] Interview: start → 8 questions → at least 1 follow-up per answer → end early works → debrief generates
- [ ] Debrief: scores visible → per-question feedback is specific → "What to work on" = exactly 3 items
- [ ] Question bank: domain filter works → difficulty filter works → free user blocked on domain 2+
- [ ] Dashboard: resume card shows correct score → interview card shows correct last score → streak increments
- [ ] Analytics: all 8 events visible in PostHog after running full flow

---

### Performance
- [ ] JD scan: verify under 8 seconds on a 4G connection (throttle in Chrome DevTools)
- [ ] Bullet rewrite: verify under 4 seconds
- [ ] Interview AI response: verify under 3 seconds per turn
- [ ] Dashboard load: verify under 3 seconds
- [ ] All images and assets compressed — no unoptimised imports

---

### Demo Prep

Full end-to-end demo script — rehearse this exactly:

1. **Sign up** as Priya (fresh graduate, SWE role) → lands on empty dashboard → onboarding tooltip fires
2. **Upload resume** → parse completes → structured preview shown → confirm
3. **Paste JD** (Google SWE L3) → score returns 38/100 → missing keywords shown
4. **Accept 2 bullet rewrites** → score updates → `resume_improved` fires → counter shows "2 improvements"
5. **Start mock interview** → SWE → Behavioural round → answer 3 questions → end early
6. **View debrief** → overall score shown → per-question feedback visible → "What to work on" = 3 items
7. **Hit paywall** → try 3rd JD scan → paywall modal → click upgrade
8. **Complete payment** (Razorpay test card) → Pro unlocks → scan completes with no block
9. Show **PostHog dashboard** → "Resumes improved this week" = 2 → events all visible

---

### Pre-Launch Checklist
- [ ] `.env.production` — all keys set in Vercel environment variables
- [ ] Supabase RLS: verify no data leaks between users (test with two separate accounts)
- [ ] Resume file storage: verify files in Supabase Storage are private (not publicly accessible URLs)
- [ ] Error monitoring: Sentry or Vercel error logs configured
- [ ] Rate limiting: API routes have basic rate limiting (max 20 req/min per IP)
- [ ] Privacy: confirm no resume content is sent to PostHog or any third party except OpenAI
- [ ] Write README with local setup instructions (`npm install`, env setup, Supabase migration)
- [ ] Tag `v1.0.0` release on GitHub when demo passes all checks

---

## Definition of Done

A task is **done** when:
- [ ] Code written and working locally
- [ ] Tested with at least one real data scenario (not just the happy path)
- [ ] API endpoint tested via browser + curl/Postman
- [ ] No known P0 bugs
- [ ] Mobile layout verified at 375px
- [ ] Relevant analytics event fires correctly

---

## Dependencies Map

```
Week 1: DB schema + auth + resume parse     → UNBLOCKS all Week 2 work
Week 1: All routes scaffolded               → UNBLOCKS frontend from building Week 2 day 1
Week 2: JD scan endpoint live              → UNBLOCKS bullet rewriter (needs jd_scan_id)
Week 2: Freemium controls working          → UNBLOCKS payments (need limit logic before charging)
Week 2: Resume editor UI complete          → UNBLOCKS interview setup (shared dashboard layout)
Week 3: Question bank seeded               → UNBLOCKS interview engine (needs questions to pull from)
Week 3: Interview engine complete          → UNBLOCKS debrief (needs session messages)
Week 3: Payments working                   → UNBLOCKS Week 4 QA (can test full upgrade flow)
```

**Critical path:** DB schema → resume parse → JD scan → bullet rewriter → interview engine → debrief

If resume parse is late, JD scan is late. If JD scan is late, bullet rewriter is late. Week 1 database and auth tasks are non-negotiable — they block everything.

---

## Out of Scope (This Plan)

- Voice interview simulation (scaffolded in Week 3 — activates in Phase 2)
- ATS optimisation checker (Phase 2)
- Resume version manager (Phase 2)
- Progress dashboard with charts (Phase 2)
- Cover letter generator (Phase 3)
- LinkedIn profile reviewer (Phase 3)
- B2B college portal (Phase 3)
- Slack / email integration
- Native mobile app (iOS / Android)
- Deployment pipeline / CI-CD beyond basic Vercel
- Non-English language support
- Salary negotiation coach (Phase 3)
