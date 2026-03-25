# 🧩 Feature Breakdown
### AI Resume + Interview Coach

> Complete feature specifications, user stories & acceptance criteria for all product capabilities.

---

| Field | Details |
|-------|---------|
| **Document** | Feature Breakdown v1.0 |
| **Version** | 1.0 |
| **Date** | March 2026 |
| **Total Features** | 12 |
| **Phase 1 (Launch)** | 6 core features |
| **Phase 2 & 3 (Roadmap)** | 6 features |

---

## How to Read This Document

| Element | Value | Meaning |
|---------|-------|---------|
| Priority | 🔴 P0 | Must ship at launch — product does not function without this |
| Priority | 🟡 P1 | Ships shortly after launch — core experience enhancement |
| Priority | 🟢 P2 | Roadmap — ships in Phase 3 or later |
| Phase | 🔵 Phase 1 | Months 1–3: Core resume + text interview loop |
| Phase | 🟣 Phase 2 | Months 4–6: Voice, ATS, dashboard |
| Phase | ⚪ Phase 3 | Months 7–12: Growth & B2B features |

---

## Pillar 1 — Resume Intelligence

<details>
<summary><strong>RI-01 · Resume Upload & Parse · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

Users can upload their existing resume in PDF or DOCX format. The AI parses the document and extracts structured data: contact info, work experience, education, skills, and summary. This structured data powers all downstream AI features.

---

**User Story**

> As a student, I want to upload my existing resume so that the tool can analyse it and give me personalised feedback — without me having to re-type everything.

---

**Acceptance Criteria**

- [ ] PDF and DOCX uploads accepted; max file size 5MB
- [ ] Parsing completes within 10 seconds for a standard 1–2 page resume
- [ ] Extracted data displays in a structured preview before user confirms
- [ ] User can manually edit any parsed field if extraction is incorrect
- [ ] Unsupported file types (PNG, TXT) show a clear error with guidance
- [ ] Parsing success rate ≥ 90% on the top 10 common resume templates

> 📌 **Note:** A plain-text fallback entry form must be available for users whose resume format fails to parse.

</details>

---

<details>
<summary><strong>RI-02 · JD Paste & Alignment Score · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

Users paste a target job description into a text field. The AI compares the resume against the JD and returns a 0–100 alignment score with a breakdown by category: keywords, experience match, skills overlap, and tone. This is the "aha moment" that hooks first-time users.

---

**User Story**

> As a job seeker, I want to paste a job description and see how well my resume matches it, so I know exactly what I need to fix before applying.

---

**Acceptance Criteria**

- [ ] JD text input supports up to 5,000 characters
- [ ] Alignment score (0–100) displays within 8 seconds of submission
- [ ] Score breakdown shows at least 3 sub-categories (keywords, skills, experience)
- [ ] Missing keywords are listed explicitly, ranked by importance
- [ ] Score is deterministic — same resume + JD always returns same score (±2 tolerance for AI variance)
- [ ] Free users can run 3 JD scans/month; paywall shown on attempt 4

> ⚠️ **Design Note:** The score must never be inflated. Internal calibration: a resume with 0 keyword overlap must score below 20.

</details>

---

<details>
<summary><strong>RI-03 · AI Bullet Point Rewriter · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

For each bullet point in the work experience section, the AI evaluates its strength and offers 2–3 improved alternatives. Rewrites are tailored to the target JD (if scanned). Suggestions follow the XYZ framework: *Accomplished X, by doing Y, as measured by Z.*

---

**User Story**

> As a student with weak bullet points, I want the AI to suggest stronger versions so that my experience sounds more impactful and relevant to the role I'm applying for.

---

**Acceptance Criteria**

- [ ] Every experience bullet point has an "Improve" button
- [ ] Clicking "Improve" returns 2–3 rewrite suggestions within 4 seconds
- [ ] Each suggestion is labelled with what it improves (e.g., "Added metric", "Stronger verb", "JD-aligned")
- [ ] User can accept one suggestion, reject all, or manually edit inline
- [ ] Accepted suggestions are tracked and count toward the "resumes improved" KPI
- [ ] Free users get 5 rewrites per session; Pro users get unlimited
- [ ] If no JD has been scanned, rewrites are general best-practice; if JD exists, rewrites are JD-specific

</details>

---

<details>
<summary><strong>RI-04 · Resume Section Feedback · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

Beyond individual bullets, the AI reviews the resume at a section level: Summary/Objective, Skills, Education, and overall formatting. Each section gets a score and 2–4 specific, actionable suggestions.

---

**User Story**

> As a fresh graduate, I want feedback on every part of my resume — not just the bullet points — so I know if my summary is compelling and my skills section is complete.

---

**Acceptance Criteria**

- [ ] At least 4 sections reviewed: Summary, Experience, Skills, Education
- [ ] Each section receives an individual score (e.g., "Skills: 6/10") and a label (Weak / Fair / Strong)
- [ ] Each section has at minimum 2 specific, actionable suggestions — not generic tips
- [ ] Suggestions reference the target JD if one has been scanned
- [ ] Formatting feedback flags: resume length, font consistency, section ordering, white space
- [ ] Section feedback loads within 10 seconds of requesting a full review

</details>

---

<details>
<summary><strong>RI-05 · ATS Optimisation Checker · 🟡 P1 · 🟣 Phase 2</strong></summary>

<br>

**Description**

Applicant Tracking Systems filter resumes before a human ever reads them. This feature analyses the resume for ATS compatibility: keyword density, formatting red flags (tables, headers, images), and file type compliance.

---

**User Story**

> As an applicant, I want to know if my resume will survive an ATS filter, so that my application actually reaches a recruiter.

---

**Acceptance Criteria**

- [ ] ATS check flags: tables in resume, headers/footers with key info, image-based content, missing keywords vs JD
- [ ] Output is a pass/fail per category with fix instructions
- [ ] Keyword gap list shows the top 10 missing terms from the JD ordered by frequency
- [ ] Free users see a preview ("3 ATS issues found"); full report is Pro-only
- [ ] Check completes within 6 seconds

> 📌 **Note:** Phase 2 delivery. Requires JD to have been scanned for keyword gap analysis.

</details>

---

<details>
<summary><strong>RI-06 · Resume Version Manager · 🟡 P1 · 🟣 Phase 2</strong></summary>

<br>

**Description**

Users can save multiple versions of their resume (e.g., one tailored for SWE, one for PM). They can compare two versions side by side and see how alignment scores differ across JDs.

---

**User Story**

> As someone applying to multiple role types, I want to save different resume versions so I can quickly switch between them without losing my original.

---

**Acceptance Criteria**

- [ ] Free users: 1 active resume saved; Pro users: up to 10 versions
- [ ] Each version shows: date saved, user-defined label, last JD alignment score
- [ ] Side-by-side diff view highlights what changed between two versions
- [ ] Deleting a version requires a confirmation step
- [ ] Restore previous version with one click

</details>

---

## Pillar 2 — Interview Coaching

<details>
<summary><strong>IC-01 · Text-Based Mock Interview · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

Users select a role type and interview round, then enter a text-based mock interview. The AI asks questions, dynamically follows up on answers, and scores responses across four dimensions: Relevance, Structure, Depth, and Clarity. A full debrief is provided at the end.

---

**User Story**

> As a student preparing for an interview, I want to practice answering real interview questions with an AI that responds like an interviewer — not just a quiz — so I can build confidence before the real thing.

---

**Acceptance Criteria**

- [ ] User selects: role category (5 options), round type (HR / Technical / Behavioural / Final)
- [ ] Interview runs for 5–8 questions with at least 1 dynamic follow-up per answer
- [ ] Each answer is scored on: Relevance (0–10), Structure (0–10), Depth (0–10), Clarity (0–10)
- [ ] Post-interview debrief shows per-question scores with specific written feedback
- [ ] Overall session score and a "what to work on" summary is provided
- [ ] Free users: 2 mock interviews/month; Pro: unlimited
- [ ] User can end the interview early and still receive partial debrief
- [ ] Interview session auto-saves if the user closes the browser accidentally

> ⚠️ **Note:** The AI must not ask the same question twice in a single session.

</details>

---

<details>
<summary><strong>IC-02 · Role-Specific Question Banks · 🔴 P0 · 🔵 Phase 1</strong></summary>

<br>

**Description**

A curated library of interview questions organised by domain and sub-type. Questions are reviewed and updated quarterly by domain experts. The question bank powers both the mock interview AI and a browsable "practice mode" where users can self-quiz.

---

**User Story**

> As a PM job seeker, I want access to questions that are actually asked in PM interviews — product sense, metrics, and estimation — not generic HR questions.

---

**Acceptance Criteria**

- [ ] Minimum 5 domains at launch: SWE, PM, Business Analyst, Marketing, UI/UX Design
- [ ] Each domain has minimum 50 questions across sub-categories
- [ ] Sub-categories are labelled and filterable (e.g., SWE: DSA / System Design / Behavioural)
- [ ] Questions are tagged by difficulty: Entry / Mid / Senior
- [ ] Free users access 1 domain; Pro users access all 5
- [ ] Browse mode allows users to see questions and ideal answer frameworks without entering a full interview
- [ ] Question bank is audited and refreshed quarterly

> 📌 **Note:** Questions must be sourced from real interview reports (Glassdoor, Blind, company engineering blogs) and anonymised.

</details>

---

<details>
<summary><strong>IC-03 · Voice Interview Simulation · 🟡 P1 · 🟣 Phase 2</strong></summary>

<br>

**Description**

An audio-based interview mode where users speak their answers aloud. The AI transcribes responses in real time, evaluates all text-based criteria, and additionally analyses pacing, filler word usage, and answer length appropriateness.

---

**User Story**

> As someone who gets nervous speaking in interviews, I want to practice answering out loud so I can work on how I sound — not just what I say.

---

**Acceptance Criteria**

- [ ] User can switch to voice mode from any active mock interview
- [ ] Microphone access requested with clear permission explanation
- [ ] Transcription appears on screen in real time with latency under 2 seconds
- [ ] Filler word count (um, uh, like, you know) tracked and shown in debrief
- [ ] Pacing rated as: Too Fast / Good / Too Slow based on words-per-minute benchmarks
- [ ] Answer length rated as: Too Brief / Appropriate / Too Long
- [ ] Voice mode is Pro-only
- [ ] Text fallback always available if microphone access is denied

> 🔧 **Phase 2 only.** Requires Whisper API or equivalent. Must pass latency validation on 3G connection before shipping.

</details>

---

<details>
<summary><strong>IC-04 · Progress Dashboard · 🟡 P1 · 🟣 Phase 2</strong></summary>

<br>

**Description**

A visual dashboard showing the user's improvement over time across both pillars: resume alignment scores, interview performance trends, domains practised, and a streak tracker to encourage daily use.

---

**User Story**

> As a job seeker doing regular practice, I want to see my improvement over time so I know the tool is actually helping and I stay motivated to keep going.

---

**Acceptance Criteria**

- [ ] Resume pillar shows: score history chart (last 30 days), number of bullets improved, number of JD scans
- [ ] Interview pillar shows: mock interviews completed, average score by dimension, domains covered
- [ ] Streak tracker shows consecutive days of activity with visual indicator
- [ ] Free users: last 7 days of data; Pro users: full history
- [ ] Dashboard loads within 3 seconds
- [ ] Data exports to PDF available for Pro users

</details>

---

## Phase 3 — Growth & Expansion Features

<details>
<summary><strong>📋 Phase 3 Roadmap Overview</strong></summary>

<br>

> ⏳ **Phase 3 Start Criteria:** Phase 3 work begins only after Phase 2 exit criteria are met — 5,000 mock interviews/week and 8% paid conversion. No Phase 3 feature enters development until these are confirmed.

| ID | Feature | Priority | Description |
|----|---------|----------|-------------|
| GR-01 | Cover Letter Generator | 🟢 P2 | Generate a JD-tailored cover letter from the user's resume in one click |
| GR-02 | LinkedIn Profile Reviewer | 🟢 P2 | Analyse headline, About section, and experience for completeness and keyword alignment |
| GR-03 | Referral Programme | 🟢 P2 | Users earn free Pro days for every friend who signs up and improves a resume |
| GR-04 | College / Bootcamp B2B Portal | 🟢 P2 | Institutional dashboard for career advisors to track student resume improvement progress |
| GR-05 | Interview Question Submission | 🟢 P2 | Users can submit real interview questions they received; moderated and added to question bank |
| GR-06 | Salary Negotiation Coach | 🟢 P2 | AI-guided practice for negotiating offers; role-play based on role and location |

</details>

---

*AI Resume + Interview Coach · Feature Breakdown v1.0 · March 2026 · Confidential*
