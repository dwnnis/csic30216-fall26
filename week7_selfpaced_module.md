# Week 7 Self-Paced Module — Evolution of Tool Use
## ~60 minutes | Framing video (~12 min, 15 slides) + required reading (~38 min) + 4 MCQs (~10 min)

**Module format:** short framing video (this slide deck) + required reading + optional readings + 4 multiple-choice questions on E3.
**Complete by:** Sunday, October 25. Week 8 is a holiday, so use it if you need to.
This module deepens the Week 7 lecture. The lecture covered *how* tool use works and how to design it. This module covers *where it came from* and why each design choice exists.

**Time budget**

| Part | Time |
|---|---|
| Framing video | ~12 min |
| Required reading (3 items) | ~38 min |
| Four multiple-choice questions | ~10 min |
| **Total** | **~60 min** |

---

### Slide 1 — Title slide

- Week 7 Self-Paced Module: Evolution of Tool Use
- Estimated time: 60 minutes (video + reading + questions)
- Complete by Sunday, October 25

**Say:** The lecture showed you how tool use works today. This module answers a different question: why does it look the way it does? Tool use went from a research idea to a standard protocol in about three years. Understanding that arc helps you read new announcements critically and anticipate what comes next.

---

### Slide 2 — Learning objectives

By the end of this module, you should be able to:

1. **Describe** the main steps in the evolution of tool use (early tool-using systems, ReAct, Toolformer, function calling, MCP) and the problem each one solved
2. **Explain** what the ReAct pattern contributes (interleaved reasoning and acting) and why it matters for reliability and debugging
3. **Contrast** training a model to use specific tools (Toolformer) with defining tools at request time (function calling)
4. **Explain** the integration problem that MCP addresses, and identify its host, client and server roles
5. **Apply** the design guidance from Anthropic's tool documentation to judge which of several tool descriptions is best
6. **Recognise** that the standards are still changing, and what that means for your own work

**Say:** Objectives 4 and 5 line up with the required reading, and the multiple-choice questions at the end are based on the reading and on this video. Keep these in view as you go.

---

### Slide 3 — Why the history matters

- Tool use did not appear fully formed. Each step fixed a specific weakness in the one before
- Knowing the problem each step solved tells you **what is still your job**
- It also helps you judge new claims: is this a new idea, or a new packaging of an old one?
- Practical payoff: if you understand *why* function calling moved tool definitions out of training and into the request, you understand why your descriptions matter so much

**Say:** The history is short. Most of it fits between late 2021 and 2025. But it moved quickly, and the pattern repeats: something that needed custom work becomes a feature, then becomes a standard.

---

### Slide 4 — Before tool use: hand-built systems (2021–2022)

- Language models were good at text and poor at **arithmetic, fresh facts, and anything outside their training data**
- Early approaches made the model work with outside systems, but the connections were **built by hand for each system**:
  - **WebGPT** (OpenAI, 2021): a GPT-3 model fine-tuned to use a text-based web browser to answer questions, trained with human feedback
  - **MRKL systems** (AI21 Labs, 2022): a language model that routes requests to separate expert modules (calculators, databases, APIs) in a modular architecture
- Common limit: each integration was **specific to one system and one task**

**Say:** These systems proved the idea, which is that a language model plus outside tools beats a language model alone. But each was a one-off design. Think of them as the early web before HTTP: each site had its own way of doing things. (These two systems are included for context and are not in the reading.)

---

### Slide 5 — ReAct (2022): reasoning and acting together

- **Paper:** "ReAct: Synergizing Reasoning and Acting in Language Models," Yao et al., arXiv October 2022 (ICLR version)
- **The gap:** reasoning methods like chain-of-thought and "acting" methods (producing action plans) had been studied separately
- **The idea:** **interleave** reasoning traces and actions. Reason about what to do, act (for example, query an external source), observe, reason again
- **Reported results** (from the abstract):
  - On HotpotQA and Fever (question answering and fact checking), ReAct **reduced hallucination and error propagation** compared with chain-of-thought alone, by querying a simple Wikipedia API
  - On ALFWorld and WebShop (interactive decision-making), it beat imitation and reinforcement-learning methods by 34% and 10% in absolute success rate, using only one or two in-context examples
  - The authors also report that the reasoning traces make behaviour **more interpretable**

**Say:** Here is the idea in one line: chain-of-thought alone can reason itself into a confident wrong answer, because nothing outside the model checks it. Interleaving actions gives the reasoning something to check against. You will read the abstract and introduction in the reading list.

---

### Slide 6 — Why ReAct matters to an engineer

- It **named the pattern**: Reason → Act → Observe → repeat. That is the loop you wrote in the Week 7 lecture
- **Auditability:** when the model's reasoning is in the transcript, you can read *why* it made a call, not only *what* it called
- **Grounding:** observations from tools can correct the model's own guesses
- **Caveats:**
  - Written reasoning is not proof of the model's actual process; it can look plausible and still be wrong
  - More steps mean more tokens, more latency, and more chances for a wrong step
  - The benchmarks are research tasks, not your product

**Say:** Be careful about the word "auditable". A reasoning trace helps you debug. It is not a guarantee that the trace reflects what really drove the decision. Treat it as evidence, not as a verdict. And remember the compounding point from the lecture: every extra step is another place to go wrong.

---

### Slide 7 — Toolformer (2023): the model teaches itself

- **Paper:** "Toolformer: Language Models Can Teach Themselves to Use Tools," Schick et al., Meta AI, arXiv February 2023
- **The idea:** train a model to decide **which APIs to call, when, with what arguments, and how to use the results**, in a **self-supervised** way, from only a handful of demonstrations per API
- **Tools:** a calculator, a question-answering system, two search engines, a translation system, and a calendar
- **Result:** better zero-shot performance on many tasks, often matching much larger models, without losing core language ability
- **The method, in outline:** the model proposes possible tool calls in text, and the calls that actually help it predict what comes next are kept for training

**Say:** The striking thing about Toolformer is that the decision to use a tool was learned, not hard-coded. The trade-off is that the tool use is baked into the weights. If you want it to use a new tool, you have to train again. Hold that thought for two slides.

---

### Slide 8 — What Toolformer could not do

- The authors discuss limits of this approach. Among them:
  - It **cannot chain tools**: it cannot use the output of one tool call as the input to another
  - It **cannot interact with a tool** over several turns (for example, refine a search after seeing results)
  - It is **sensitive to the exact wording** of the input
- And a practical limit that matters for engineers: **tools are learned in training**. A new tool means more training
- Compare with ReAct: ReAct supports multi-step interaction, but through prompting examples, not trained-in tool use

**Say:** Put the two papers side by side. ReAct gave you the multi-step loop. Toolformer gave you learned tool decisions. Neither gave you what a developer actually wants: add a new tool by writing a definition, with no retraining, and have the model use it across many turns. That was the next step. (Check the Toolformer paper's limitations section if you want the authors' exact wording; I summarise it here.)

---

### Slide 9 — Function calling (2023): tools move into the request

- **June 2023:** OpenAI introduced **function calling**. Anthropic followed with its own **tool use** feature, which became widely available in 2024
- **The key change:** you **describe your tools in the API request**. The model has been trained, once and in general, to read tool definitions and decide whether to call them. No tool-specific training
- **What you do now** (from the lecture):
  - Define tools with a **name, description, and input schema**
  - The model returns a structured **tool call**
  - **Your code** runs the tool and returns the **result**
- **Result:** tool use became a normal feature that any developer could add by writing a schema

**Say:** This is the pivot, and it explains why description quality matters so much. Because the model was trained to read schemas in general, your definition is the only thing telling it what your tool is for. Toolformer put the knowledge in the weights. Function calling puts it in your text.

---

### Slide 10 — Contrast: three ways to tell a model about a tool

| | Hand-built (2021–22) | Toolformer (2023) | Function calling (2023→) |
|---|---|---|---|
| Where tool knowledge lives | in the application code | in the model's weights | in the **request** (your schema) |
| Adding a new tool | write new integration | **retrain** | **write a schema** |
| Multi-step use | by design of the system | limited | supported through the loop |
| Who executes the tool | the application | the application | **your code** |
| Main risk | brittle, one-off | frozen, hard to extend | **vague schemas** → wrong calls |

- Everything you did in the Week 7 lab sits in the right-hand column

**Say:** Pause the video here and see whether you can explain each row without looking. The last row is the practical one. Once tool knowledge lives in a schema that you write, the quality of the schema becomes your responsibility.

---

### Slide 11 — The next problem: every app defines tools its own way

- With function calling, each application writes **its own** tool definitions and glue code, for its own model
- If you want the same GitHub or database integration in three applications, you write it three times, or you copy it and let the copies drift
- With N applications and M integrations, that is **N × M** pieces of work
- This is an integration problem, not a model problem. It is the problem standards solve

**Say:** The same thing happened with editors and programming languages. Each editor built its own support for each language, until the Language Server Protocol let you write the language support once. The tool problem looked the same.

---

### Slide 12 — MCP (2024): a standard for tools and context

- **Model Context Protocol:** introduced by Anthropic in **late 2024** as an open protocol for connecting AI applications to tools and data
- **Roles:** a **host** (the AI app) uses one **client** per **server**; servers expose **tools, resources and prompts** over **JSON-RPC**, via **stdio** (local) or **Streamable HTTP** (remote)
- **What it changes:** write an integration once as a server; any compatible host can use it. N × M becomes N + M
- **What it does not change:** the model still uses ordinary tool definitions. The host translates between the two. **Schema quality, boundaries and safety are still your job**

**Say:** Keep the layering clear from the lecture. Function calling is between the model and the host. MCP is between the host and the tool servers. MCP adds reuse, not intelligence.

---

### Slide 13 — MCP in 2025–2026: adoption, governance, and change

- **December 9, 2025:** Anthropic **donated MCP to the Agentic AI Foundation**, a directed fund under the Linux Foundation, co-founded by Anthropic, Block and OpenAI. The announcement reported about 10,000 active servers and first-class support across ChatGPT, Claude, Cursor, Gemini, Microsoft Copilot, VS Code and others
- **The specification keeps evolving.** The most recent published version (2026-07-28) is **stateless** and adds a `server/discover` request. **Sampling** and server-side logging are **deprecated**. An older HTTP+SSE transport was replaced by Streamable HTTP
- **Security has become a first-class topic:** the project publishes best practices on confused-deputy attacks, token passthrough, local server compromise, and scope minimisation

**Say:** Two lessons. First, a standard under neutral governance with several large companies behind it is more likely to last than one owned by a single vendor. Second, notice how much changed in under two years. Anything you build on this should pin versions and expect to update.

---

### Slide 14 — Timeline and pattern

| Year | Step | Problem it addressed |
|---|---|---|
| 2021–22 | WebGPT, MRKL | show that tools help; each hand-built |
| Oct 2022 | **ReAct** | combine reasoning with acting; reduce error propagation |
| Feb 2023 | **Toolformer** | model learns when to call tools; but tied to training |
| Jun 2023 | **Function calling** | define tools at request time; no retraining |
| 2024 | Provider tool-use APIs | tool use becomes a standard feature |
| Late 2024 | **MCP** | one integration reusable across hosts |
| Dec 2025 | MCP → Agentic AI Foundation | neutral governance for a shared standard |

- **The pattern:** each step moved something **out of one-off code or model weights and into a shared interface**
- **What never moved:** designing the interface well, evaluating the trajectory, and deciding what the system is allowed to do. Those remain **engineering responsibilities**

**Say:** If you only remember one slide from this video, make it this one. Notice the last line. Standards make tools easier to connect. They do not make a poorly described tool work, and they do not decide what your agent should be allowed to do.

---

### Slide 15 — What to do now

- Watch this framing video (~12 min). You just finished it
- Read the **three required readings** (~38 min). Links on E3
- Explore the optional readings if you want to go deeper
- Answer the **four multiple-choice questions** on E3 (~10 min)
- Total estimated time: ~60 minutes

**Say:** The questions are based on the readings and this video, so doing the readings first will make them straightforward. Two of the readings are practical documentation you will use again in your project. If a page has changed since this module was written, use the version on the site.

---

## Reading List

### Required Reading (~38 min)

**1. Anthropic — "Define tools" (tool use documentation)** (~15 min)
https://platform.claude.com/docs/en/agents-and-tools/tool-use/define-tools

Read the sections on **descriptions, naming, input schema, input examples, and tool choice**. Skim the rest.

*Why this reading:* this is the official guidance on what makes a tool definition work: how detailed a description should be, how to name and group tools, and when to use examples. It is the practical version of the lecture's design slides and the reference you will use for your project.

**2. Model Context Protocol — "Architecture overview"** (~15 min)
https://modelcontextprotocol.io/docs/learn/architecture

Read **Participants**, **Layers**, and **Primitives**. You can skim the JSON examples.

*Why this reading:* it explains the host, client and server roles, the data and transport layers, and the three server primitives, in the project's own words. Pay attention to how many clients a host creates.

**3. The two research papers, abstract and introduction only** (~8 min)
- Yao et al. (2022), "ReAct: Synergizing Reasoning and Acting in Language Models," https://arxiv.org/abs/2210.03629
- Schick et al. (2023), "Toolformer: Language Models Can Teach Themselves to Use Tools," https://arxiv.org/abs/2302.04761

*Why this reading:* the two primary sources for slides 5–8. The abstracts are short and readable without a machine-learning background. Notice what each paper claims, and what it does not.

### Optional Readings

1. **Anthropic Engineering — "Writing effective tools for agents — with agents"** (Sept 2025)
https://www.anthropic.com/engineering/writing-tools-for-agents
How Anthropic's team builds and evaluates tools: prototype, build evaluations from realistic multi-step tasks, consolidate tools, namespace them, return high-signal results, and write clear descriptions and actionable error messages. Highly recommended for your project.

2. **Anthropic Engineering — "Building effective agents"** (Dec 2024)
https://www.anthropic.com/engineering/building-effective-agents
Distinguishes workflows (predefined code paths) from agents (the model directs its own process), and argues for the simplest solution that works. A preview of Week 13. The page notes that some of the tooling described has since changed.

3. **Model Context Protocol — "Security best practices"**
https://modelcontextprotocol.io/specification/draft/basic/security_best_practices
The project's own account of the main attacks and mitigations. Read the introductions to *Local MCP Server Compromise*, *Confused Deputy*, and *Scope Minimization*.

4. **Model Context Protocol — "Understanding MCP servers"**
https://modelcontextprotocol.io/docs/learn/server-concepts
A fuller treatment of tools, resources and prompts, including who controls each.

---

## Multiple Choice Questions

*4 questions. Submitted on E3. Graded on completion. Correct answers and explanations shown after submission.*

