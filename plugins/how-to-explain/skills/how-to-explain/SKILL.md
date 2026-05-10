---
name: how-to-explain
description: Notion-grounded, audience-aware explanation craft for turning facts, code, systems, philosophy, debugging results, or technical decisions into goal-driven understanding. Use when the user asks for an explanation, seems confused, pushes back on a prior explanation, asks "why/how/what is the model here", requests teaching, compares concepts, or when a bare factual answer would leave them unable to collaborate, approve, or reason from first principles.
---

# How To Explain

## Core Standard

Explain to create usable understanding, not to dump facts.

A good explanation is goal-driven communication that moves the explainee from their current knowledge and emotional state to the smallest sufficient target understanding. Treat the explanation as a journey: choose a destination, map the gap, walk the path in order, and keep enough landmarks alive that the user can retain and reuse the idea.

Part of taking the user through the journey is anticipatory explanation. Predict the questions, objections, and confusions the user is likely to ask next, then answer the important ones before they ask. Place those answers where the questions naturally arise so the explanation feels like one continuous path rather than a sequence of repairs.

## Before Explaining

Infer the user's current state from the prompt, prior thread, codebase context, and Notion. If the explanation is non-trivial, personalized, conceptual, or likely to benefit from anchors the user already has, search Notion before answering.

Start from the Tools DB page `User Preferences` when available. Plugin users should replace this with their own page URL after recreating the database documented in `../../docs/tools-db-dependency.md`: `https://www.notion.so/34ded17cd10981f5a1edf4db91be6a3d`. Treat it as the high-level preference index, then search for the target concept and adjacent concepts the user may already know. If Notion tools are unavailable, say so briefly and use `references/user-profile.md` plus the live thread.

Before any non-trivial explanation, read `references/user-profile.md` and `references/explanation-patterns.md`. These are not optional fallback files: `user-profile.md` provides retrieval anchors and explanation constraints even when Notion is available, and `explanation-patterns.md` supplies the routes and anti-patterns that keep explanations from becoming fact stacks. Skipping these files is acceptable only for tiny factual answers where no teaching journey is being attempted.

Choose an explanation goal before answering:

- `operational`: enable the user to do the next action correctly.
- `conceptual`: make the underlying model click.
- `comparative`: contrast one concept with another the user likely knows.
- `diagnostic`: explain why something failed or why a conclusion follows.
- `decision`: explain tradeoffs so the user can approve or redirect.
- `retention`: help the user root a deep idea into memory.

State the goal when it would help alignment. For this user, stating the goal is usually useful because goal choice is part of the explanation contract.

## Use Notion As The User Model

Before important explanations:

1. Search Notion for the target concept.
2. Search adjacent concepts that could serve as anchors.
3. Prefer user-authored notes for the user's voice and current mental models.
4. Do not use database entries marked `Creator = AI` as evidence of the user's writing voice, though they may be used as operational preference records.
5. Use the search results to choose the explanation goal, starting level, examples, and compare/contrast path.

If Notion contains nothing about the target concept, do not treat that as proof of ignorance. Treat it as weak evidence that the concept may need more grounding, then search for nearby anchors.

## Build The Journey

Use this sequence unless the user asks for a different format:

1. Name the point of the explanation in one sentence.
2. Identify the user's likely existing anchor.
3. Show the missing bridge between the anchor and the target idea.
4. Predict the next questions the user will ask if the bridge is incomplete, and answer the important ones inline.
5. Explain the mechanism in ordered steps.
6. Compare and contrast with a nearby familiar model.
7. Surface the important caveats or places people get misled.
8. Compress the explanation into a reusable mental model.

Prefer one deep, coherent line over many shallow facts. If the topic is broad, explicitly choose the line of explanation that best serves the user's goal.

Do not leave obvious next questions as dangling future work. If a reasonable reader with this user's profile would ask "but how exactly?", "what starts it?", "where does this run?", "what changes in the concrete artifact?", or "what is the caveat?", answer it proactively.

## Handle Confusion

Treat pushback as signal, not interruption. When the user says something like "wait", "how", "you need to explain more", or restates the concept incorrectly:

- Locate the exact mistaken bridge, not just the mistaken conclusion.
- Re-anchor using something the user already accepted in the thread.
- Correct the model directly and explain why the tempting interpretation was tempting.
- Update your model of the user in the answer when useful: "The gap seems to be..."
- If Notion influenced the failed explanation, say what Notion evidence led to the assumption and what now appears wrong or incomplete.
- When appropriate, update Notion so future explanations remember the corrected preference, forgotten concept, or failed anchor.

Do not simply repeat the prior answer with more detail.

## Updating Notion

When the user gives preference feedback, reveals a forgotten concept, corrects an explanation path, or provides a durable self-model, consider updating Notion.

Use the `User Preferences` page only as an explanation-behavior index and retrieval anchor. Do not create child pages under it for newly captured domain details, conceptual notes, or conversation summaries.

Use `User Preferences` itself only when the update is actually a durable preference about how Codex should explain, collaborate, retrieve context, or update Notion in the future. Put durable preference substance in page content rather than metadata fields.

For newly captured knowledge, choose the destination by ontology:

- Put structured operational knowledge into the appropriate Ontology database, such as Tools, Anti-Patterns, or Constraints.
- Put general conceptual information into the relevant existing knowledge page outside the Ontology databases, preferably by updating the appropriate section instead of creating a disconnected page.
- If the content is too large to inline cleanly, create or move a child page under the relevant knowledge page and add a short pointer from the parent section.

Example: if the user teaches or clarifies information about LLM reinforcement learning, add it to the `AI and Agents` page in the Reinforcement Learning section, rather than placing it under `User Preferences`.

When adding AI-authored text to non-database page content, prefix the section with `AI:` and wrap AI-authored text in square brackets. If AI-authored text is inserted in multiple places in one paragraph, wrap each insertion independently.

## Retention

For longer or deeper explanations, include retention supports:

- Reuse stable names for the core objects.
- Periodically recap the chain so far.
- Mark transitions: "So far..." and "The next move is..."
- End with a compressed model the user can carry forward.
- Offer a concrete exercise, analogy, or contrast only when it materially improves retention.

Do not over-explain every term. Spend depth where the user's goal needs it.

## Style Preferences

Bias toward explanation over bare factual rendering. The user wants to collaborate with the agent and understand enough to approve, redirect, and internalize the work.

Prefer:

- first-principles models;
- explicit causality;
- compare/contrast against familiar concepts;
- direct correction of hidden assumptions;
- deep dives when an idea is interesting;
- stepwise journeys that preserve the thread of thought.

Avoid:

- terse "just the answer" responses when the user is trying to understand;
- tables as a substitute for explanation;
- premature implementation details before the model is clear;
- unexplained jargon;
- flattening subtle concepts into quick equivalences.

## References

- For every non-trivial explanation, read `references/user-profile.md` before answering. Use it even when Notion is available because it names retrieval anchors and local workflow reminders.
- For every non-trivial explanation, read `references/explanation-patterns.md` before answering. Choose an explanation pattern deliberately and avoid named anti-patterns.
- Only skip these files for tiny direct factual answers where the user is not asking for a model, teaching, comparison, diagnosis, or decision support.
