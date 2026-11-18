# CP2 Grading Overview

*For the "Rubrics" section of the CP2 page. The full rubric, with level descriptions for each criterion, will be published after grading.*

---

**Weight:** 15% of the course grade · **Due:** Monday, November 23, end of day, on E3 · **Submission:** one zip per team, named `GroupXX_CP2`

### How CP2 is graded

CP2 is worth **100 points**, split equally between **the product (50)** and **how your team built it (50)**. How you built it matters as much as what you built. A modest prototype built by all four of you, with real review conversations and a decision log, can score well. An impressive prototype built mostly by one person will not.

Each criterion is graded on **four levels** (Strong, Solid, Developing, Not yet) according to the evidence we can find in your submission and your repository.

### Product (50 points)

| Criterion | Points | What we look for | Evidence we check |
|---|---|---|---|
| **Working prototype** | 15 | Two people can use it together; the core interaction works well enough for a real user to try the main task. Polish is not required | Your demo in the Week 12 lab, the repository, README run instructions |
| **Design rationale and user testing** | 10 | Your main design decisions and what shaped them, including findings from **at least two sessions with real users outside your team** | Design rationale document; `DECISIONS.md` entries that cite the findings |
| **AI components** | 15 | **Prompt test suite** (6): at least 10 cases, typical and edge inputs, and at least one cycle of failure found, fix, re-run. **System prompt (`CLAUDE.md`) and prompt documentation card** (5): a new engineer can see what the AI does, what it was told to do and how it fails. **AI usage guidelines** (4): updated from your Week 3 draft to match how your team really worked | Test file and results, the card, the history of your guidelines |
| **Updated evaluation report** | 10 | An interim summary of your evidence so far, honest about what you have **not** tested yet | The report |

*If your tool does not use AI, say so in your submission; the 15 points for AI components then move to the working prototype (+8) and the evaluation report (+7).*

### Collaboration (50 points)

| Criterion | Points | What we look for | Evidence we check |
|---|---|---|---|
| **Everyone contributes to the code** | 15 | Substantive code from **all four** members, not only documentation or configuration | GitHub contributor graph, PR history |
| **Review quality and the code steward role** | 15 | Stewards read the PR and say something real: a question, a concern or a specific suggestion. "Looks good to me" on its own does not count | PR comments, steward records and handoff notes in `DECISIONS.md` |
| **`DECISIONS.md`** | 10 | A log of real decisions: what was chosen, what was rejected, who led it, kept up as you went | `DECISIONS.md` compared with the PR history and commit dates |
| **Team sessions** | 10 | The walking skeleton and merge day happened, all four took part, and you recorded what you learned. We grade that the sessions took place and how honestly you reflected, not how impressive the output was | Walking skeleton worksheet and merged PR; merge-plan entry in `DECISIONS.md`; a clean, running `main` |

### Minimums for every student

Each of you, individually, needs by CP2:
- at least **2 merged pull requests with substantive code**
- at least **2 pull-request approvals as code steward**, each with at least one substantive comment
- to have been the **code steward at least once**, recorded in `DECISIONS.md`

These are checked for each person against the contributor graph, PR history and `DECISIONS.md`. **[Instructor: state here what happens if a student falls short, for example "a TA will contact you and your team; the instructor may adjust that student's CP2 grade".]**

### What to keep in mind

- **We grade evidence, not claims.** If something happened but left no trace (a review done out loud, a decision made in a chat), write it down in the PR or `DECISIONS.md`.
- **Small and shared beats big and solo.** A smaller prototype that all four of you understand is a better CP2 than a bigger one only one person can explain.
- **Be honest about gaps.** Saying clearly what is untested, unfinished or not working costs you nothing, and is part of what we look for in the evaluation report.
