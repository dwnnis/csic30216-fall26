# Week 3 Self-Paced Module — How Engineering Teams Work with AI
### Slide Outline (8 slides)

---

## Slide 1 — Title slide

- Week 3 Self-Paced Module: How Engineering Teams Work with AI
- Complete before Week 4 (Sep 28) — ideally within two days of this week's class

**Say:** This module deepens everything from today's lab. You wrote guidelines and an evaluation plan under time pressure — the readings show you what those artifacts look like when they are done well, and the reflection prompt asks you to compare.

---

## Slide 2 — What this module is for

- Today's lecture introduced team norms and evaluation methodology at a conceptual level
- The lab asked you to apply them immediately — which means the drafts you produced are exactly that: first drafts
- This module gives you the real-world evidence to calibrate against: how do actual engineering teams do this?

**Say:** The most useful thing you can do after this module is read your team's draft guidelines and evaluation plan and ask: are these specific enough to follow? The case studies in the readings will give you a much clearer answer than you had before you did them.

---

## Slide 3 — Evaluation approaches in depth

- The lecture introduced three approaches: structured observation, pre/post survey, brief interview
- The key question for each: what does it actually look like to run this within a semester project?
- Structured observation: two people, a task, a note-taker — 30 minutes produces more data than a week of surveys
- Pre/post survey: five questions before the tool exists (about the pain point) and the same five questions after — the delta is your evidence
- Brief interview: not a usability test, not a focus group — five specific questions, recorded (with permission), transcribed

**Say:** You do not need to run all three — but you need to run at least one with people outside your team. The readings go deeper on each approach.

---

## Slide 4 — How real teams adopt AI tooling

- DORA's 2025 State of AI-assisted Software Development report (this week's required reading) found something directly relevant here: teams with a "clear and communicated AI stance" — meaning developers actually know what AI use is expected and permitted — see AI's benefits amplified across individual effectiveness, organizational performance, and even reduced friction, compared to teams without one
- Teams that formalise AI usage norms early (even imperfect ones) have fewer conflicts and more consistent output quality
- Teams that leave AI use to individual discretion accumulate invisible technical debt — undocumented prompts, unreviewed AI commits, inconsistent output quality
- The specific form of the norm matters less than the fact of having one — and this is now a measured finding, not just an intuition

**Say:** This is why today's lab exists, and you don't have to take our word for it anymore — it's in the data. A specific, imperfect guideline that the team agreed to is more valuable than a perfect guideline one person wrote, and if this report is right, having any clear, communicated stance at all is worth more than most teams assume.

---

## Slide 5 — What the case studies show

- DORA's report includes two real, named case studies worth reading closely:
- **Adidas** (nearly 1,000 developers): teams with loosely coupled architecture and fast feedback loops saw 20–30% productivity gains from AI adoption; teams tightly coupled to legacy ERP systems saw little or no benefit at all — the AI didn't fail, the surrounding system did
- **Booking.com** (3,000+ developers): AI coding tool adoption was uneven until they invested specifically in training developers to give the AI more explicit instructions and context — after that, merge requests increased by up to 30%
- The pattern across both: AI's benefit is not automatic — it depends on the team's existing practices and how deliberately the tool is introduced
- This matches the report's central finding: AI is an amplifier, not a fix. It magnifies the strengths of high-performing teams and the dysfunctions of struggling ones

**Say:** Notice that neither case study is really about the AI tool itself — Adidas's story is about architecture, and Booking.com's is about training. That's the report's whole argument in miniature: the tool is rarely the actual bottleneck. As you read, map these back to your own team: are you closer to the loosely-coupled Adidas teams, or the tightly-coupled ones?

---

## Slide 6 — Disclosure and liability: the Air Canada case

- Air Canada's chatbot provided a customer with incorrect information about bereavement fare policy
- When the customer relied on that information and was denied the fare, they sued
- Air Canada argued the chatbot was a "separate legal entity" responsible for its own actions
- The court rejected this: the company was responsible for what its system told customers
- The engineer who built the system is not legally liable — the company is. But the engineer who documented their decisions is in a much better position than one who did not.

**Say:** This case is referenced again in Week 15's ethics lecture. For now: understand that "the AI said it" is not a defence, and documentation of your design decisions is your primary protection.

---

## Slide 7 — Reflection prompt

- Open your team's draft guidelines from today's lab
- Read them as if you are a new engineer joining the team in Week 10
- Ask yourself: can I follow these without asking anyone a question?
- Then ask: after reading today's case studies, which of our guidelines is most likely to fail us under pressure?
- You do not need to submit your answer — but you should discuss it with your team before CP1

**Say:** Teams that do this reflection and revise their guidelines before CP1 consistently submit stronger checkpoints. It takes 20 minutes and it is the highest-return activity you can do this week.

---

## Slide 8 — What to do now

- Watch the assigned video
- Read the required reading
- Optional readings if you want to go deeper
- Answer the four multiple choice questions on the course portal
- Do the reflection prompt — open your draft guidelines and evaluate them against what you read

**Say:** Do the reflection prompt last — it requires the readings to be useful.

---

## Required Reading

**DORA — "State of AI-assisted Software Development" (2025)**
Full report: [dora.dev/dora-report-2025](https://dora.dev/dora-report-2025) (also available via [Google Cloud](https://cloud.google.com/resources/content/2025-dora-ai-assisted-software-development-report))

Read: **Executive summary** (pp. 3–7), **"AI adoption and use"** chapter (pp. 23–32), and the **"Clear and communicated AI stance"** section of the DORA AI Capabilities Model chapter (pp. 50–53).

Why this reading: This is the source of the adoption/trust statistics and the Adidas/Booking.com case studies referenced on Slides 4 and 5, and it's built on genuinely substantial research — over 100 hours of qualitative interviews and survey responses from nearly 5,000 technology professionals, run by DORA in collaboration with Google Cloud, GitHub, GitLab, and IT Revolution. It's a public report, not paywalled, and no account or download form is required to access the full PDF.

## Optional Readings

- **Spotify Engineering — "AI Changed How Spotify Builds: What We Learned (and Fixed) About Quality at Higher Velocity"** [engineering.atspotify.com/2026/9/ai-changed-how-spotify-builds-what-we-learned-and-fixed-about-quality-at-higher-velocity](https://engineering.atspotify.com/2026/9/ai-changed-how-spotify-builds-what-we-learned-and-fixed-about-quality-at-higher-velocity) — Spotify sharing their own experience of adopting AI in software engineering. This article was released only less than a week ago, with some really good insights
- **Travis Media — "AI Code Is Cheap. Open Source Maintainers Pay the Bill"** [travis.media/blog/ai-assisted-open-source-contributions](https://travis.media/blog/ai-assisted-open-source-contributions/) — an overview of how open source maintainers are struggling with AI-generated contributions
- **open-source-ai-contribution-policies** (GitHub repository) [github.com/melissawm/open-source-ai-contribution-policies](https://github.com/melissawm/open-source-ai-contribution-policies) — a list of policies by different open source projects on how they engage with AI-generated contributions

## Multiple Choice Questions

**Question 1**

According to the DORA 2025 report, what is described as AI's primary role in software development?

A) A replacement for weak engineering practices
B) An amplifier that magnifies existing organizational strengths and weaknesses
C) A tool that produces uniform improvements regardless of team maturity
D) A cost-cutting measure with no effect on team performance

**Correct answer:** B
**Explanation:** The report's central finding, repeated throughout, is that AI functions as an amplifier — it makes high-performing organizations even stronger and struggling organizations' dysfunctions more visible, rather than fixing underlying problems on its own.

**Question 2**

The DORA 2025 report found that AI adoption is now nearly universal (90% of respondents use it at work). What did the report find about developers' trust in AI-generated output?

A) Trust is just as universal as adoption — nearly all developers fully trust AI output
B) Most developers report no trust at all in AI-generated code
C) A majority report some degree of confidence in AI output, while a meaningful minority remain more reserved or skeptical
D) Trust could not be measured because too few developers use AI regularly

**Correct answer:** C
**Explanation:** The report found a nuanced trust landscape: a majority expressed some degree of confidence in AI output, while roughly 30% reported more reserved or skeptical views. High adoption and measured trust coexist — the report describes this "trust but verify" pattern as a sign of mature adoption, not a contradiction.

**Question 3**

What did the DORA 2025 report find about how often AI users turn to AI by default when facing a problem or task ("reflexive use")?

A) Nearly all AI users (over 90%) always default to AI first
B) Only 7% report always using AI by default, while most use it "about half the time" or more, but not automatically every time
C) AI users never turn to AI reflexively — it is always a deliberate, planned choice
D) Reflexive AI use was not something the report measured

**Correct answer:** B
**Explanation:** The report distinguishes broad adoption from "reflexive use" — the default habit of reaching for AI. Only 7% of AI users report always defaulting to AI, while a majority use it about half the time or more, suggesting AI has become a frequent habit but not a universal reflex.

**Question 4**

According to the DORA AI Capabilities Model, what effect does a "clear and communicated AI stance" have on a team?

A) It has no measurable effect on outcomes — policies are symbolic only
B) It only matters for large enterprises, not small teams
C) It amplifies AI's positive effects on individual effectiveness and organizational performance, and can even reduce friction
D) It primarily works by restricting how much AI developers are allowed to use

**Correct answer:** C
**Explanation:** DORA's research found that when developers know what AI use is expected and permitted, AI's positive effects on individual effectiveness and organizational performance are amplified, and AI's otherwise neutral effect on friction becomes a reduction in friction. This is the direct empirical reason this week's lab has you write down and agree on a team AI usage guideline — it's not just good practice, it's a factor shown to improve outcomes.
