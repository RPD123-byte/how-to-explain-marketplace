# Explanation Patterns

## Pattern: Mechanism Bridge

Use when the user knows nearby concepts but not the target mechanism.

1. State the explanation goal.
2. State the false-but-tempting model.
3. Name the key distinction.
4. Walk the actual mechanism step by step.
5. Compare it to a familiar mechanism found in Notion or the live thread.
6. Compress the result into one reusable sentence.

Example shape:

> The tempting model is X because it looks like Y. The key distinction is Z. Once Z exists, the system no longer needs A; it can do B instead.

## Pattern: Deep Technical Thread

Use when the user signals fascination with a concept and wants the whole thread rooted into memory.

1. Search Notion for the concept and adjacent anchors.
2. Start with the practical surface.
3. Drop one layer into the runtime, architecture, math, or system model.
4. Identify the design pressure that forced this shape.
5. Contrast with another ecosystem's answer to the same pressure.
6. Extract the transferable principle.

## Pattern: Scaling Abstraction

Use when explaining concepts like time complexity, system load, token growth, database query growth, or other scaling laws.

1. Begin with the real-world thing people are tempted to measure.
2. Explain why that measurement is unstable or too environment-dependent.
3. Introduce the abstraction that preserves the important growth structure.
4. Name the chosen input variable and unit of work.
5. Derive the growth function.
6. Collapse the function into the dominant shape.
7. Explain what the abstraction throws away and when that matters.

## Pattern: Collaboration Explanation

Use before or after code changes when the user needs to approve or work with the agent.

1. Explain what is being changed.
2. Explain why that is the right level of intervention.
3. Explain what behavior will differ.
4. Explain what will not be touched.
5. Explain how it will be verified.

## Anti-Pattern: Fact Stack

Do not answer by stacking correct statements if the user is trying to build a mental model. Correct facts can still fail if they do not reveal causality.

Weak:

> Python has Tasks. Go has goroutines. Go uses channels. Python uses Futures.

Better:

> Python makes async completion observable by wrapping coroutine progress in a Task object. Go makes goroutine execution opaque by default, so completion has to be represented separately through channels, wait groups, or context.

## Anti-Pattern: Table Too Early

Tables are useful after the model exists. They are often bad as the first explanation because they hide the mechanism behind labels.

Use a table only after walking the core causal path, or when the user explicitly asks for a comparison matrix.

## Anti-Pattern: Beginner Path By Default

Do not default to a beginner classroom route when the user asks about a familiar technical concept. First decide whether the user's likely need is the label, the mechanism, the abstraction boundary, or the deeper reason the concept exists.
