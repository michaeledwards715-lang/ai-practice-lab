# Learning Log

A running record of what I'm learning on the way to becoming an AI business practitioner.

## 2026-11-18 · Level 0: Foundations

**Covered today**
- Chatbot vs workflow vs agent, and the one question that separates them: *who decides the next step?*
- Core vocabulary: model, prompt, system prompt, token, context window, tool, human-in-the-loop
- Next layer: hallucination, RAG, memory, MCP, guardrails, prompt injection, evals
- Drafted 3 business use cases (see [use-cases.md](use-cases.md))

**3 things I learned**
1. **Most "agent" requests are really workflows.** If you can draw the flowchart before it runs, it's a workflow, and that's usually cheaper and safer to sell. Save agents for messy, unpredictable work.
2. **Instructions and guardrails are different.** An instruction tells the AI what to do ("offer other times"). A guardrail is a hard limit on what it can never do ("never spend over $100," "read-only access").
3. **Any step that involves money or a relationship needs a human in the loop.** Approving deals, sending quotes, and emailing partners as me should all go past a person first.

**In my own words: context window**
> The context window is chat or agents background material you provide is. It's like a local map. If you go past it, you are in a different town and different subject.

**What I'm working on**
- Keep explanations to 1 to 2 sentences: what it is, an everyday comparison, why a business cares
- Always include the everyday comparison, since that's what makes non-technical people get it
- Name the concept out loud (e.g. "that's RAG") when I'm using it

**Next:** Level 0 checkpoint, a role-play explaining AI to an office manager.
