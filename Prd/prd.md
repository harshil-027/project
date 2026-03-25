# 📄 Product Requirements Document
### AI Resume + Interview Coach

> **Helping students and fresh graduates land their first great job — with AI-powered, hyper-personalised resume & interview coaching.**

---

| Field | Details |
|-------|---------|
| **Product Name** | AI Resume + Interview Coach |
| **Version** | 1.0 |
| **Date** | March 2026 |
| **Author** | Product Manager |
| **Target Segment** | Fresh Graduates & Students |
| **Business Model** | Freemium |
| **Status** | 🟡 Draft — In Review |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Goals & Success Metrics](#2-goals--success-metrics)
3. [Target Users](#3-target-users)
4. [Feature Requirements](#4-feature-requirements)
5. [Freemium Business Model](#5-freemium-business-model)
6. [Non-Functional Requirements](#6-non-functional-requirements)
7. [Assumptions & Risks](#7-assumptions--risks)
8. [Product Roadmap](#8-product-roadmap)

---

## 1. Executive Summary

<details>
<summary><strong>🔍 Click to expand — The Problem We're Solving</strong></summary>

<br>

Every year, millions of students and fresh graduates enter one of the most competitive job markets in history — armed with a resume they're not sure is good enough, and zero practice for the interview that follows.

Existing tools fail in four compounding ways:

- **Feedback is too generic** — tools like Grammarly or basic resume checkers flag spelling errors but cannot tell a CS student that their bullet points aren't quantified enough for a Google SWE role.
- **No credible mock interview experience** — platforms like Interview Warmup exist but feel scripted. Users can't practice the follow-up question, the curveball, or the domain-specific scenario.
- **No JD-tailoring** — students use one resume for 50 applications. Recruiters who spend 7 seconds per resume notice immediately.
- **Price exclusion** — premium tools cost $20–$40/month. For a student in India, Southeast Asia, or a Tier 2 US college, this is a real barrier.

</details>

<details>
<summary><strong>🎯 The Solution & North Star Vision</strong></summary>

<br>

**AI Resume + Interview Coach** is a freemium, AI-powered career tool built specifically for students and early-career job seekers. It closes three critical gaps simultaneously:

1. Tailors your resume to a **specific job description**
2. Coaches you through **role-specific mock interviews**
3. Delivers feedback that is **actionable** — not just a score out of 10

> **North Star Vision:** A student pastes a job description on Monday. By Friday, they have a polished, JD-tailored resume and have completed three mock interviews with real feedback. They walk into the interview confident. That transformation — in under a week, at near-zero cost — is the product we are building.

**In one line:** A single AI tool that takes a job description, rebuilds your resume around it, and then interviews you for that exact role — for free.

</details>

---

## 2. Goals & Success Metrics

<details>
<summary><strong>⭐ North Star Metric — Resumes Improved / Week</strong></summary>

<br>

Success for this product is unambiguous: **are we actually improving resumes at scale?**

The primary KPI is the number of resumes meaningfully improved per week — not sessions opened, not accounts created. A resume "improved" is defined as: at least one AI-suggested bullet point, restructure, or JD-alignment change that the user **accepted and saved**.

> Vanity metrics like page views or sign-ups will not appear on any executive dashboard.

</details>

<details>
<summary><strong>📊 OKR Table — 6-Month Targets</strong></summary>

<br>

| Objective / Key Result | Metric | Target (6 mo) |
|------------------------|--------|---------------|
| **O1: Drive weekly resume improvement at scale** | Resumes improved / week (meaningful edit accepted) | **10,000 / week** |
| → KR1: High activation from new users | % of signups who improve ≥1 resume in first session | 60% |
| → KR2: Strong return rate | Weekly active users / Monthly active users | 45% |
| **O2: Deliver credible mock interview experience** | Mock interviews completed / week | **5,000 / week** |
| → KR1: Completion rate | % of started interviews that finish all questions | 70% |
| → KR2: Perceived quality | Post-session rating (1–5 stars) | ≥ 4.2 avg |
| **O3: Convert free users to paid sustainably** | Free → Paid conversion rate | **8%** |
| → KR1: Paywall engagement | % of free users who hit a paywall and return next day | 30% |
| **O4: Student accessibility** | % of user base from students / fresh grads | ≥ 75% |

</details>

---

## 3. Target Users

<details>
<summary><strong>👩‍💻 Primary Persona — Priya, The Anxious Applicant</strong></summary>

<br>

| Attribute | Details |
|-----------|---------|
| **Name** | Priya, 22 |
| **Background** | Final year CS student, Tier-2 college, India |
| **Goal** | Land a product or SWE role at a tech company |
| **Frustration** | *"I don't know if my resume is good. I've applied to 40 places and heard back from none."* |
| **Budget** | ₹0–₹500/month for tools. Won't pay upfront without proof of value. |
| **Tech comfort** | High — uses LinkedIn, GitHub, ChatGPT. But doesn't know how to prompt effectively for resume help. |
| **Success looks like** | An interview call within 2 weeks of using the tool. |

**Why she's our primary user:** Priya represents the largest, most underserved segment — digitally native, budget-constrained, and deeply anxious about the gap between her resume and the job she wants. She is the beachhead.

</details>

<details>
<summary><strong>👨‍💼 Secondary Persona — Marcus, The Career Switcher</strong></summary>

<br>

| Attribute | Details |
|-----------|---------|
| **Name** | Marcus, 26 |
| **Background** | 2 years in marketing, pivoting to product management |
| **Goal** | Reframe his marketing experience to look relevant for a PM role |
| **Frustration** | *"My resume reads like a marketer's. I don't know how to make it look like a PM's."* |
| **Key value prop** | JD-to-resume alignment that rewrites his bullets through a PM lens |

</details>

<details>
<summary><strong>🚫 Out of Scope Users (v1)</strong></summary>

<br>

- Senior professionals (10+ years) requiring executive resume services
- Recruiters or hiring managers — this is a candidate-side tool only
- Non-English language support — English only in v1

</details>

---

## 4. Feature Requirements

<details>
<summary><strong>🗂️ Priority Matrix — All Features at a Glance</strong></summary>

<br>

| Feature | Description | Priority | Phase |
|---------|-------------|----------|-------|
| Resume Upload & Parse | Upload PDF/DOCX; AI extracts structured content | 🔴 P0 | Phase 1 |
| JD Paste & Alignment Score | Paste a job description; get a 0–100 match score | 🔴 P0 | Phase 1 |
| AI Bullet Point Rewriter | Suggests stronger, quantified, JD-aligned bullet points | 🔴 P0 | Phase 1 |
| Resume Section Feedback | Section-by-section critique: Summary, Experience, Skills | 🔴 P0 | Phase 1 |
| Text-Based Mock Interview | AI asks role-specific questions; scores answers | 🔴 P0 | Phase 1 |
| Role-Specific Question Bank | Curated Q banks: SWE, PM, Design, Finance, Marketing | 🔴 P0 | Phase 1 |
| Voice Interview Simulation | Audio-based interview with real-time AI feedback | 🟡 P1 | Phase 2 |
| Resume Version Manager | Save, compare, and manage multiple resume versions | 🟡 P1 | Phase 2 |
| ATS Optimisation Checker | Flag keywords missing vs. ATS systems | 🟡 P1 | Phase 2 |
| Progress Dashboard | Track improvement scores, interviews done, streak | 🟡 P1 | Phase 2 |
| Cover Letter Generator | Generate JD-tailored cover letters from resume | 🟢 P2 | Phase 3 |
| LinkedIn Profile Reviewer | Analyse and suggest LinkedIn headline/about improvements | 🟢 P2 | Phase 3 |

</details>

<details>
<summary><strong>📝 Pillar 1 — Resume Intelligence (detailed)</strong></summary>

<br>

### 1.1 Resume Upload & JD Alignment
The entry point of the product. Users upload their resume (PDF or DOCX) and paste the target job description. The AI parses both and produces:

- A **JD Match Score (0–100)** with a visual breakdown by category (skills, experience, tone, keywords)
- A list of **missing keywords** critical to ATS screening for that role
- An **overall resume health score** based on structure, clarity, and impact

> ⚠️ **Design Principle:** The match score must feel earned, not inflated. If a resume genuinely has a 34/100 match, the tool must say 34. False positivity destroys user trust.

---

### 1.2 AI Bullet Point Rewriter
The highest-value feature of the resume pillar. For each bullet point in the user's experience section, the AI will:

- Identify if the bullet is weak (vague, no metric, passive voice)
- Suggest **2–3 rewritten alternatives** using the XYZ framework *(Accomplished X by doing Y, as measured by Z)*
- Highlight which rewrite is best aligned with the target JD

Users can accept, reject, or further edit suggestions inline. All accepted edits are tracked to compute the 'resumes improved' metric.

---

### 1.3 Resume Section Feedback
Beyond bullet points, the AI reviews:

- **Summary / Objective** — is it generic or role-specific? Does it open strong?
- **Skills section** — are the skills listed matching what the JD asks for?
- **Education** — formatting, relevance of coursework, GPA display conventions
- **Overall formatting** — one page vs. two, white space, section ordering

</details>

<details>
<summary><strong>🎤 Pillar 2 — Interview Coaching (detailed)</strong></summary>

<br>

### 2.1 Text-Based Mock Interview
The user selects a role type and interview round type. The AI then:

- Draws questions from the role-specific question bank
- **Dynamically follows up** based on the user's answer (no scripted linear flow)
- Scores each answer on: **Relevance, Structure (STAR), Depth, and Communication clarity**
- Provides a detailed debrief at the end with a per-answer breakdown

---

### 2.2 Voice Interview Simulation *(Phase 2)*
Users speak their answers aloud. The AI transcribes in real time and evaluates for all text-based criteria plus:

- **Pacing** — too fast, too slow, appropriate pauses
- **Filler word frequency** — 'um', 'like', 'you know'
- **Answer length** — too brief, too rambling

> 🔧 **Phase 2 Dependency:** Requires integration with a speech-to-text API (e.g., Whisper / Deepgram) and a latency budget under 2 seconds for transcription to feel real-time.

---

### 2.3 Role-Specific Question Banks
Launch domains:

| Domain | Sub-categories |
|--------|---------------|
| Software Engineering (SWE) | DSA, System Design, Behavioural |
| Product Management (PM) | Product Sense, Execution, Metrics, Estimation |
| Business Analyst / Finance | Case-style, Excel, Communication |
| Marketing / Growth | Campaign, Analytics, Brand, GTM |
| UI/UX Design | Portfolio Critique, Process, Design Challenge |

</details>

---

## 5. Freemium Business Model

<details>
<summary><strong>💳 Free vs. Pro — Feature Tier Table</strong></summary>

<br>

| Feature | Free | Pro (₹299 / $4.99 /mo) |
|---------|------|------------------------|
| Resume uploads | 1 active resume | Unlimited |
| JD alignment scans | 3 / month | Unlimited |
| Bullet point rewrites | 5 suggestions / session | Unlimited |
| Mock interviews | 2 / month (text only) | Unlimited (text + voice) |
| Question bank access | 1 domain | All 5 domains |
| Progress dashboard | Basic (7-day) | Full history + trends |
| Resume version history | ❌ | ✅ Up to 10 versions |
| Voice interview mode | ❌ | ✅ |
| ATS keyword checker | Preview only | Full report |

</details>

<details>
<summary><strong>💡 Pricing Philosophy & Conversion Strategy</strong></summary>

<br>

**Why ₹299?**

Pro is priced at ₹299/month (~$3.60) — deliberately affordable for the Indian student market, which is our primary beachhead. The goal is **volume of paid users**, not high ARPU. A student who pays ₹299 and gets a job will tell 10 friends.

**How we convert free → paid:**

1. The free tier is designed to create an "aha moment" in the first session — the JD match score and 5 bullet rewrites are **always free**. This hooks users before they hit a limit.
2. Paywalls are placed at the moment of **highest intent**: when a user tries to run their 3rd JD scan or 3rd mock interview in a month.
3. A **student discount page** will offer 3 months Pro for free with a valid `.edu` email — seeding virality through college networks.

</details>

---

## 6. Non-Functional Requirements

<details>
<summary><strong>⚡ Performance Requirements</strong></summary>

<br>

- JD alignment scan must return results in under **8 seconds** on a standard connection
- Bullet point suggestions must appear within **4 seconds** of user requesting a rewrite
- Voice transcription latency must be under **2 seconds** end-to-end (Phase 2)
- System uptime SLA: **99.5%** monthly

</details>

<details>
<summary><strong>🔒 Privacy & Data Security</strong></summary>

<br>

- Resumes contain PII. All uploaded documents are encrypted at rest **(AES-256)** and in transit **(TLS 1.3)**
- Users own their data. Resumes are **never used to train AI models** without explicit opt-in consent
- **GDPR** and **India DPDP Act** compliance from day one
- Resume data is auto-deleted **90 days** after account closure

</details>

<details>
<summary><strong>♿ Accessibility</strong></summary>

<br>

- WCAG 2.1 AA compliance for all UI components
- Screen reader support for the resume editor
- Mobile-responsive web app — many students in India will use on Android, not desktop

</details>

---

## 7. Assumptions & Risks

<details>
<summary><strong>⚠️ Risk Register</strong></summary>

<br>

| Risk | Likelihood | Mitigation |
|------|-----------|------------|
| AI feedback quality is perceived as generic — the exact problem we're solving for | 🔴 High | Invest heavily in prompt engineering; use JD context in every single AI call; A/B test feedback copy |
| Low free-to-paid conversion — users get enough from free tier and never upgrade | 🟡 Medium | Monitor paywall touch rate; adjust limits based on cohort data; introduce time-based trials |
| Resume parsing fails for non-standard formats | 🟡 Medium | Support top 3 resume templates; provide a structured form as fallback |
| Voice interview latency too high on slow mobile connections | 🟡 Medium | Phase 2 only; pre-validate with load tests on 3G; offer text fallback |
| Competition from well-funded players (LinkedIn, Google) copying core features | 🔴 High | Win on price, student-focus, and JD personalisation depth. Build community moat early. |

</details>

<details>
<summary><strong>📌 Key Assumptions</strong></summary>

<br>

- Students will share their resume with an AI tool if they trust it is private and won't be sold
- The Indian student market (English-speaking) is large enough as a beachhead to hit 10,000 weekly active users within 6 months
- A freemium model with a ₹299 price point will convert at ≥ 8% within 6 months
- Text-based mock interviews, done well, deliver enough value to justify the product before voice simulation ships

</details>

---

## 8. Product Roadmap

<details>
<summary><strong>🗓️ 3-Phase Delivery Plan</strong></summary>

<br>

| Phase | Timeline | Key Deliverables | Exit Criteria |
|-------|----------|-----------------|---------------|
| **Phase 1** | Months 1–3 | Resume upload & parse, JD alignment score, bullet rewriter, text mock interview, 5 role question banks | 500 resumes improved / week; NPS ≥ 35 |
| **Phase 2** | Months 4–6 | Voice interview simulation, ATS checker, resume version manager, progress dashboard | 5,000 mock interviews / week; 8% paid conversion |
| **Phase 3** | Months 7–12 | Cover letter generator, LinkedIn reviewer, B2B college partnerships, referral programme | 50,000 resumes improved / week; B2B pilot with 3 colleges |

> 🚀 **Phase 1 is the Proof.** Phase 1 must be built lean and fast — 3 months maximum. The goal is not a polished product; it is proof that AI feedback on resumes drives measurable improvement.

</details>

<details>
<summary><strong>🚫 Out of Scope (v1 & v2)</strong></summary>

<br>

- Job application tracking / ATS integration (Greenhouse, Lever)
- Recruiter-side features or employer dashboard
- Non-English language support
- AI-generated resume from scratch (user must supply base resume)
- Native mobile app — web-first, mobile-responsive only

</details>

---

*AI Resume + Interview Coach · PRD v1.0 · March 2026 · Confidential*
