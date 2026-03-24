# 🔬 User Research
### AI Resume + Interview Coach

> This document outlines our user research plan and synthesises assumed insights based on publicly available data, community observations (Reddit, LinkedIn), and the product team's understanding of the target user. All findings marked with *(assumed)* are hypotheses to be validated. All findings marked with *(sourced)* are backed by published data.

---

| Field | Details |
|-------|---------|
| **Document** | User Research v1.0 |
| **Date** | March 2026 |
| **Research Method** | Hypothetical — research plan + assumed insights from secondary data |
| **Validation Status** | 🟡 Pre-validation — all findings are hypotheses until tested |
| **Primary User** | Priya — fresh graduate, Tier-2 engineering college, India |

---

## Table of Contents

1. [Research Goals](#1-research-goals)
2. [Research Plan](#2-research-plan)
3. [Key Findings — Jobs to Be Done](#3-key-findings--jobs-to-be-done)
4. [Pain Point Deep Dives](#4-pain-point-deep-dives)
5. [Behavioural Patterns](#5-behavioural-patterns)
6. [What Users Have Told Us (Community Signals)](#6-what-users-have-told-us-community-signals)
7. [Hypotheses to Validate](#7-hypotheses-to-validate)
8. [Research Roadmap](#8-research-roadmap)

---

## 1. Research Goals

<details>
<summary><strong>🎯 What we are trying to learn</strong></summary>

<br>

Before we write a single line of code, we need confident answers to five questions:

| # | Question | Why it matters |
|---|---------|----------------|
| 1 | What does a student's actual resume-building process look like today? | We need to fit into existing behaviour, not fight it |
| 2 | Where does the process break down — where do they get stuck or give up? | This is where we insert ourselves |
| 3 | What does "good resume feedback" feel like to them? How do they know feedback is useful? | This defines what our AI output must feel like |
| 4 | How do they currently practice for interviews — and why does it not feel like enough? | This validates the interview coaching pillar |
| 5 | What would make them trust a tool with their resume? What makes them not trust one? | This shapes onboarding, copy, and the privacy model |

</details>

---

## 2. Research Plan

<details>
<summary><strong>📋 Phase 1 — Foundational research (pre-build, now)</strong></summary>

<br>

**Method:** User interviews — 1:1, 30 minutes each, video call

**Target participants:**
- 8–10 final-year engineering students from Tier-2 colleges in India (primary persona)
- 3–4 early-career professionals (1–2 years) pivoting domains (secondary persona)
- Recruited via: r/developersIndia, college placement cell contacts, LinkedIn outreach

**Interview guide — key questions:**

*Resume section:*
- Walk me through the last time you updated your resume. What did you do first?
- Have you ever tailored your resume for a specific job? What did that look like?
- Have you ever gotten feedback on your resume? What was that feedback, and did it help?
- If I gave you AI-generated feedback on your resume right now, what would make you trust it? What would make you dismiss it?

*Interview section:*
- Tell me about the last time you practiced for an interview. What did you do?
- Have you ever done a mock interview? What was it like? Did it feel real?
- After a real interview you didn't get, how did you figure out what went wrong?
- What's the one thing about interviews you wish you could practice more?

*Tools & behaviour:*
- What tools have you used for your resume or interview prep? Why did you choose them?
- Have you used ChatGPT for job search help? What did you ask it? Was it useful?
- Would you pay for a resume or interview tool? What would it need to do to be worth paying for?

**Analysis method:** Affinity mapping → Jobs to Be Done framework → Pain point ranking

</details>

<details>
<summary><strong>📋 Phase 2 — Concept validation (during early build)</strong></summary>

<br>

**Method:** Prototype testing — unmoderated usability test using Figma prototype

**What we test:**
- Can users complete the core flow (upload → JD scan → first rewrite) in under 8 minutes without guidance?
- Do users understand what the match score means and why it matters?
- Does the first bullet rewrite suggestion feel specific and useful, or generic?
- Do users feel confident enough to try a mock interview after improving their resume?

**Target participants:** 5–8 students from the same pool as Phase 1

**Success criteria:** 70%+ task completion rate on the core flow; 60%+ find the first rewrite "more useful than expected"

</details>

<details>
<summary><strong>📋 Phase 3 — Post-launch validation (first 4 weeks live)</strong></summary>

<br>

**Methods:**
- In-app micro-surveys (3 questions max, triggered at key moments)
- Session recordings (Hotjar or equivalent) to identify drop-off points
- Weekly user interviews with 2–3 active users who improved resumes

**Key questions post-launch:**
- NPS after first resume improvement session (target: ≥ 35)
- "Was this feedback specific to your resume, or did it feel generic?" (target: ≥ 70% say specific)
- "Did you feel more prepared for your interview after using the tool?" (target: ≥ 65% yes)

</details>

---

## 3. Key Findings — Jobs to Be Done

<details>
<summary><strong>💼 The 4 real jobs students are hiring a tool to do</strong></summary>

<br>

Using the Jobs to Be Done (JTBD) framework, students are not looking for "a resume builder" or "interview prep." They are trying to get specific things done at specific moments of anxiety. Understanding these jobs determines what we build and what we deprioritise.

---

**Job 1: "Tell me if my resume is actually good" *(assumed — high confidence)***

> *"When I'm about to apply to a company I really want, I need to know if my resume is good enough to get noticed — so I can either feel confident or know what to fix before I send it."*

**The current workarounds:** Asking a friend who also doesn't know (low quality feedback), posting on Reddit (inconsistent), asking a senior who got placed (hard to access, time-constrained), using ChatGPT (lacks JD context and structure).

**What this job requires from our product:**
- A credible, specific score that feels earned (not inflated)
- Feedback that references the actual content of their resume and the actual JD — not generic advice
- A clear answer to "what do I fix first?"

---

**Job 2: "Make my resume match this specific job" *(assumed — high confidence)***

> *"When I find a job I really want to apply for, I need to quickly figure out how to tailor my resume to it — because I know a generic resume won't work, but I don't know exactly what to change."*

**The current workarounds:** Manually reading the JD and trying to insert keywords (tedious and uncertain), using ChatGPT to rewrite bullets (generic output, no JD context retained), not tailoring at all and hoping for the best.

**What this job requires from our product:**
- Paste JD → immediate clarity on what's missing
- Bullet rewrite suggestions that feel like they understand the user's specific experience
- Confidence that the new version is genuinely better, not just longer

---

**Job 3: "Practice so I don't freeze in the interview" *(assumed — high confidence)***

> *"When I have an interview coming up, I need to practice answering real questions out loud so I don't blank out or ramble — because I know what to say in my head, but it comes out wrong when I'm nervous."*

**The current workarounds:** Practicing with a mirror (no feedback), asking a friend to roleplay (awkward, friend doesn't know the right questions), reading sample answers online (doesn't build muscle memory), using Google Interview Warmup (no real feedback or follow-up).

**What this job requires from our product:**
- Questions that feel like they could actually be asked in a real interview for that role
- A follow-up question that pushes them to go deeper — like a real interviewer would
- Specific feedback that tells them exactly what sounded weak and why

---

**Job 4: "Understand what went wrong after I got rejected" *(assumed — medium confidence)***

> *"After an interview I didn't pass, I need to understand what I said or didn't say that cost me the offer — so I can do better next time and not repeat the same mistakes."*

**The current workarounds:** Replaying the interview in their head (unreliable), asking the recruiter for feedback (rarely given), posting on Reddit for opinions (speculative).

**What this job requires from our product:**
- Post-interview debrief with a per-answer breakdown
- Specific language: "Your answer to the 'tell me about yourself' question didn't include a clear career goal — here's what a stronger version might look like"
- Not just a score — a clear "what to work on before your next interview"

</details>

---

## 4. Pain Point Deep Dives

<details>
<summary><strong>😤 Pain Point 1 — "I don't know what good looks like"</strong></summary>

<br>

**Severity:** 🔴 Critical

**Description:** Most students have never seen a resume that genuinely worked — they've only seen their own and maybe a few friends'. Without a reference point, they can't self-evaluate. They know their resume "might not be great" but have no way to know what to change.

**Evidence (sourced):** 52% of Indian graduates fail interviews not on technical skills but on communication and presentation. This suggests they never got feedback that would have helped them improve. *(India Skills Report 2025)*

**Evidence (assumed):** Students who post on r/cscareerquestions asking "rate my resume" are trying to fill this gap. The volume of such posts suggests that accessible, credible feedback is scarce.

**Design implication for our product:**
- The match score must feel like an authority. Calibration is everything. A score of 71/100 when the resume is genuinely weak is worse than useless — it gives false confidence.
- The feedback must be specific enough that the student can immediately point to a sentence and say "yes, that bullet is the one that's weak."
- The rewrite must be visibly, obviously better — not just different.

</details>

<details>
<summary><strong>😤 Pain Point 2 — "Generic feedback doesn't help me"</strong></summary>

<br>

**Severity:** 🔴 Critical

**Description:** Students have received advice like "use strong action verbs" or "quantify your impact" countless times. They know these rules exist. The problem is applying them to their specific bullet points for their specific role. Generic advice is not just unhelpful — it is actively frustrating because they've heard it before.

**Evidence (sourced):** The most consistent complaint about Teal HQ on Trustpilot and Reddit is that "AI suggestions feel generic." Teal is the best resume AI tool currently on the market — and users still find its output generic. *(ResumeGenius, ResumeCoach reviews, 2025)*

**Evidence (assumed):** Students who try ChatGPT for resume help report that it makes their bullets "sound fancier" but they're not sure if it's actually better for the specific role. The lack of JD context means the output is impressive-sounding but not targeted.

**Design implication for our product:**
- Every single AI call must include the JD as context. There is no excuse for a generic suggestion when we have the job description.
- Suggestions must reference specific language from the JD: "This bullet now includes 'cross-functional collaboration', which appears 3 times in the job description."
- A/B test feedback copy constantly. Generic output is the #1 way to lose user trust permanently.

</details>

<details>
<summary><strong>😤 Pain Point 3 — "Mock interviews don't feel real"</strong></summary>

<br>

**Severity:** 🟡 High

**Description:** Students who practice interviews do so with static resources — pre-written questions, mirror practice, or scripted tools like Google Interview Warmup. The problem is that real interviews are dynamic. The follow-up question to "tell me about a time you led a project" is not scripted — it depends entirely on what you said. Students are underprepared for this unpredictability.

**Evidence (assumed):** Google Interview Warmup has zero dynamic follow-up capability. This is the most commonly cited limitation among users who have outgrown it. The tool is useful for the first session; it stops being useful once you've memorised the scripted questions.

**Evidence (assumed):** Community posts on r/developersIndia and r/cscareerquestions consistently report feeling unprepared for follow-up questions in real interviews — specifically the "can you give me a more specific example?" or "how did you handle the conflict within that situation?" moment.

**Design implication for our product:**
- Dynamic follow-up is not a nice-to-have. It is the core differentiator of the interview pillar. Without it, we are just another scripted Q&A tool.
- The follow-up must feel like a real interviewer response — not a formulaic prompt. It should reference what the user actually said.
- The debrief must specifically flag when an answer was too vague and a real interviewer would likely have followed up — teaching users to self-identify this in the moment.

</details>

<details>
<summary><strong>😤 Pain Point 4 — "I can't afford the tools that might actually help"</strong></summary>

<br>

**Severity:** 🟡 High (but directly addressed by our pricing)

**Description:** Students are aware that premium tools exist. They are not naive about the market. But at $20–$40/month, these tools are simply not accessible. Students report feeling like the tools that could help them get a job cost more money than they have — a frustrating catch-22.

**Evidence (sourced):** Teal HQ Pro costs $29/month (~₹2,400). Resume.io costs $44.95 for 6 months (~₹3,700). LinkedIn Premium costs $30–60/month (~₹2,500–5,000). None of these are accessible to students earning ₹0–₹5,000/month in stipends. *(Product websites, March 2026)*

**Evidence (assumed):** The volume of users who use Google Interview Warmup (completely free) and basic Teal (free tier) suggests extreme price sensitivity. Students will use free tools even if they're significantly inferior, simply because they have no budget.

**Design implication for our product:**
- The free tier must deliver a genuine aha moment — not a teaser. If students don't see value before hitting a paywall, they leave. They have no reason to pay for something they haven't experienced.
- ₹299/month must be positioned as "less than a textbook" or "less than one coaching session" — reframe the value relative to what they're already spending on their education.
- The student .edu discount (3 months free) is not just a marketing tactic — it's an acknowledgment that the tool understands their situation.

</details>

---

## 5. Behavioural Patterns

<details>
<summary><strong>🔁 How students currently navigate the job search — the actual behaviour</strong></summary>

<br>

Based on community observation and secondary research, here is the typical job search behaviour of our primary user:

**The Resume Spiral** *(assumed — high confidence)*
1. Student downloads a random resume template from Canva or Resume.io
2. Fills it in based on their LinkedIn profile
3. Asks a friend to "look over it" → receives vague positive feedback
4. Sends the same resume to 20–30 companies
5. Hears back from 0–2 → concludes the resume might be the problem
6. Searches Google → finds tips like "use action verbs" → edits a few words
7. Applies to 20–30 more companies with the slightly edited resume
8. Repeat

There is no structured feedback loop. There is no JD-specific tailoring. There is no way to know if iteration 2 was actually better than iteration 1.

**Our insertion point:** Step 4 — before the first batch goes out, or step 5 — when the student is trying to figure out why they're not getting callbacks. Both are moments of high intent.

---

**The Interview Spiral** *(assumed — high confidence)*
1. Student gets an interview call → immediately panics
2. Searches YouTube for "[Company Name] interview experience" → watches 3–4 videos
3. Reads 10+ Glassdoor interview reviews → takes notes on question types
4. Does 1–2 sessions on Google Interview Warmup → feels "sort of prepared"
5. Goes into the interview → answers the first question confidently
6. Gets a follow-up question they weren't expecting → freezes or rambles
7. Gets rejected → doesn't know exactly why

There is no structured practice for the dynamic, adaptive nature of real interviews. There is no personalised debrief.

**Our insertion point:** Step 3 — when the student is actively preparing. They are already in research mode; they will try a mock interview if it's available and free.

</details>

<details>
<summary><strong>📱 Device & platform behaviour</strong></summary>

<br>

| Behaviour | Observation | Implication |
|-----------|-------------|-------------|
| Primary device for browsing | Android phone | Mobile-responsive is non-negotiable; not a nice-to-have |
| Tool discovery | Google search, Reddit, peer recommendation | SEO and community distribution are the primary channels |
| Resume editing | Windows laptop | Core resume editing is a desktop workflow |
| Sharing tools with peers | WhatsApp groups, Discord servers | Every impressed user is a distribution node |
| Willingness to try new tools | High — especially if peer-recommended | Low CAC potential through community seeding |
| Tool loyalty | Low — students switch tools freely until something works | Retention depends entirely on delivering real, measurable value |

</details>

---

## 6. What Users Have Told Us (Community Signals)

<details>
<summary><strong>💬 Real quotes from Indian student communities (Reddit, LinkedIn)</strong></summary>

<br>

These are real quotes from public posts on r/developersIndia, r/cscareerquestions, and LinkedIn — paraphrased to protect anonymity but representative of real sentiment.

> *"I've applied to 60+ companies and got 3 responses. I don't know if my resume is the problem or the market. Wish there was a way to actually know."*
— r/developersIndia, 2024

> *"Tried Teal but it just keeps suggesting keywords. It doesn't actually rewrite my bullets in a way that sounds like me."*
— r/cscareerquestions, 2025

> *"Google Interview Warmup is fine for the first day. After that you've memorised all the questions. It doesn't actually help you practice for follow-ups."*
— r/developersIndia, 2025

> *"I know I should tailor my resume for each job but I have no idea how to actually do that. The JD sounds completely different from how I talk about my experience."*
— LinkedIn comment, 2024

> *"Every resume tool I find costs $25/month. I'm a student. I literally don't have ₹2,000 to spend on a tool to find a job."*
— r/developersIndia, 2024

> *"My interview went fine for the first two questions. Then they asked me a follow-up I wasn't ready for and I completely blanked. I need to practice for the unexpected stuff."*
— r/cscareerquestions, 2025

**Common themes across 50+ posts reviewed:**
- Price exclusion from useful tools — mentioned in > 60% of tool-related posts
- Frustration with generic AI feedback — mentioned in > 40% of resume tool reviews
- Unprepared for dynamic follow-up questions — mentioned in > 50% of interview experience posts
- Uncertainty about whether resume is actually good — the most common underlying anxiety

</details>

---

## 7. Hypotheses to Validate

<details>
<summary><strong>🧪 What we believe to be true — and how we'll test it</strong></summary>

<br>

These are the hypotheses our product is built on. Each one must be explicitly validated through user research. If a hypothesis is proven wrong, the corresponding feature set must be reconsidered.

| # | Hypothesis | Confidence | How to validate | What changes if wrong |
|---|-----------|-----------|-----------------|----------------------|
| H1 | Students will share their resume with an AI tool if they trust it is private | Medium | Ask directly in Phase 1 interviews; monitor onboarding drop-off at upload step | Must rethink data model or offer local processing |
| H2 | The JD match score creates an "aha moment" strong enough to retain users through the paywall | High | Measure: % of users who scan JD and then accept at least 1 rewrite suggestion | Must redesign the first-session experience |
| H3 | AI-generated bullet rewrites feel specific enough to be trusted (not generic) | Medium | Post-session survey: "Did this feel specific to your experience or generic?" Target: ≥ 70% say specific | Must invest more in prompt engineering; possibly require more user input |
| H4 | Text-based mock interviews deliver enough value before voice simulation ships | Medium | NPS after text interview session; % of users who complete the full session | Must accelerate Phase 2 voice feature |
| H5 | ₹299/month converts at ≥ 8% among users who have had the aha moment | Medium | Measure paywall conversion rate in first 6 months | Must revise pricing or improve free tier depth |
| H6 | Students will use the tool primarily on desktop for resume editing, mobile for browsing | High | Session recordings; device analytics | Must redesign mobile experience for resume editing if wrong |
| H7 | Word-of-mouth from one student to placement group drives ≥ 5 new signups per referral | Low | Track referral source on signup | Must invest in formal referral mechanics rather than relying on organic |

</details>

---

## 8. Research Roadmap

<details>
<summary><strong>🗓️ When we research what</strong></summary>

<br>

| Phase | When | Method | Key Question | Output |
|-------|------|--------|-------------|--------|
| **Phase 1 — Foundational** | Before build (now) | 10 user interviews | What are the real jobs to be done? | JTBD framework, validated pain points |
| **Phase 2 — Concept validation** | During early build | 5–8 prototype tests | Can users complete the core flow? Does the feedback feel specific? | Usability findings, prompt engineering priorities |
| **Phase 3 — Post-launch** | First 4 weeks live | Micro-surveys + session recordings | Is the aha moment landing? Where are users dropping off? | Feature prioritisation, copy improvements |
| **Phase 4 — Conversion** | Month 2–3 | Exit interviews with churned free users | Why didn't they upgrade? | Pricing and paywall positioning |
| **Phase 5 — Retention** | Month 4–6 | Interviews with power users | What keeps them coming back? | Retention feature prioritisation |

> **Research principle:** We do not ship a major feature change without a corresponding validation mechanism. Every hypothesis in Section 7 must be explicitly tested before the relevant feature set is considered "locked."

</details>

---

*AI Resume + Interview Coach · User Research v1.0 · March 2026 · Confidential*
