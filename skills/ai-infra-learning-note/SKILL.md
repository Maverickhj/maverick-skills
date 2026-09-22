---
name: ai-infra-learning-note
description: Create learning-oriented AI infrastructure notes that help the reader build a clear conceptual model before diving into implementation details. Use for distributed training, RL systems, inference, model architecture, operators, and adjacent AI Infra topics.
---

# AI Infra Learning Note

Create technical learning notes that prioritize conceptual clarity over completeness.

The goal is to help the reader answer:

- What problem is this concept solving?
- Why does it need to exist?
- What is the simplest useful mental model?
- How does the core mechanism work?
- How does it connect to concepts the reader already knows?

Do not turn every learning note into a system design document.

## Core principle

Optimize for understanding, not coverage.

Prefer:

Problem -> Motivation -> Mental Model -> Core Mechanism -> Minimal Example -> Summary

over:

Definition A -> Definition B -> API list -> implementation details -> optimizations -> edge cases.

Implementation, trade-offs, formal derivations, and optimization details are optional. Include them only when they materially improve understanding or the user explicitly asks for them.

## Reader model

Before writing, determine:

- what the reader already knows;
- what the reader does not know;
- what they are trying to understand;
- which prerequisite concepts are actually necessary.

Do not use vague labels like "beginner" or "advanced" as a substitute for a real reader model.

## Planning workflow

Before writing the main content, internally establish:

1. Reader Model
2. Problem Chain
3. Concept Dependency
4. Mental Model
5. Core Mechanism
6. Minimal Example
7. Summary

Optional extensions:

- Formal Model
- Real Implementation
- Trade-offs / Optimization
- References

The final document does not need to expose this planning structure literally.

## Default narrative structure

### 1. Problem

Start from a concrete question, limitation, contradiction, or engineering pressure.

Explain what becomes difficult before introducing the concept that solves it.

### 2. Motivation

Explain why the concept matters.

Keep this close to the reader's goal. Avoid turning motivation into a survey of every possible use case.

### 3. Mental Model

Build the smallest useful intuitive model.

At this stage:

- minimize terminology;
- state simplifications clearly;
- avoid implementation-specific names unless needed;
- use simple diagrams, data flow, tensor shapes, or small examples when helpful.

The reader should be able to explain the idea informally before seeing detailed mechanics.

### 4. Core Mechanism

Explain how the concept works at the minimum level needed for understanding.

Focus on:

- what entities exist;
- how they relate;
- what data or information flows between them;
- what changes over time;
- what invariant or rule makes the mechanism work.

Introduce terminology only when the reader now has a reason to need it.

### 5. Minimal Example

Use the smallest example that makes the concept concrete.

Prefer:

- tiny tensors;
- 2-4 processes or devices;
- short pseudocode;
- minimal Python / PyTorch snippets;
- small numerical examples.

The example should validate the mental model, not showcase an API surface.

### 6. Summary

End by compressing the concept into a small number of durable ideas.

A good summary should answer:

- what problem this concept solves;
- what the key mechanism is;
- what the reader should remember;
- what concept naturally comes next.

## Optional extensions

These are not part of the default path.

### Formal Model

Add formulas, complexity, invariants, communication volume, or tensor algebra only when they clarify the concept.

Every formula should answer a concrete question.

### Real Implementation

Map the concept onto PyTorch, NCCL, Megatron-LM, vLLM, SGLang, verl, CUDA, Triton, or another real codebase only when implementation knowledge is useful to the user's goal.

Do not let framework details replace the conceptual explanation.

### Trade-offs / Optimization

Discuss compute, memory, communication, latency, throughput, or scalability only after the baseline mechanism is clear.

Always establish the baseline before describing an optimization.

### References

Add papers, docs, source files, or APIs when the user wants to continue deeper.

Keep reference material separate from the teaching flow.

## Cognitive dependency rules

### Explain why before what

Before defining a concept, establish the problem that makes it necessary.

### Do not use unexplained prerequisites

If a section depends on a concept not yet introduced:

1. introduce the prerequisite first; or
2. defer the dependent section.

### One conceptual thread per section

Each section should answer one main question.

Do not mix concept explanation, API details, optimization trivia, and historical background unless the connection is essential.

### Progressive refinement

Start from a simplified model and gradually remove simplifications.

For example:

single device
-> multiple devices
-> need for coordination
-> communication
-> collective operation

Stop when the reader's current question has been answered.

Do not continue into implementation or optimization merely because those topics exist.

## Writing style

Prefer clear technical prose over encyclopedic coverage.

Use headings that express questions or mechanisms.

Prefer:

- "Why do gradients need synchronization?"
- "What does AllReduce actually guarantee?"
- "Why does sequence packing help?"

over:

- "Background"
- "Details"
- "Other concepts"

Use concrete examples when they improve understanding.

Avoid unnecessary terminology, repetition, and side quests.

## AI Infra-specific guidance

For distributed topics, track only the concepts needed to make the mechanism clear, such as:

- process / worker;
- device;
- tensor placement;
- communication;
- synchronization.

For model architecture topics, track:

- input;
- output;
- intermediate representation;
- information flow;
- tensor shape when relevant.

For RL / post-training topics, track conceptual roles such as:

- rollout;
- policy;
- reference model;
- reward;
- advantage;
- update.

Only introduce system-level details like scheduling, packing, parallelism, or runtime architecture when they are necessary to answer the current question.

## Cognitive dependency review

After drafting, review each section:

- Why does the reader need this now?
- Does it depend on an unexplained concept?
- Does it advance the main problem chain?
- Can it be removed or postponed without hurting understanding?
- Did implementation detail appear before the concept was clear?

If a section can move later without damaging understanding, move it later.

If a detail is useful but not required, omit it or place it under an optional extension.

## Output priority

When clarity and completeness conflict, prefer clarity.

A short note that gives the reader a durable mental model is better than a comprehensive note that buries the concept.
