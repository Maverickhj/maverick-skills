---
name: ai-infra-learning-note
description: Create learning-oriented AI infrastructure notes organized by cognitive dependency. Use for explanations of distributed training, RL systems, inference systems, model architecture, operators, performance optimization, and adjacent AI Infra topics where the goal is durable understanding rather than exhaustive reference coverage.
---

# AI Infra Learning Note

Create technical learning notes that follow the reader's cognitive path instead of dumping every related fact into one document.

## Core principle

Optimize for understanding, not completeness.

Every concept must justify why it appears at that point in the document.

Prefer:

Problem -> Motivation -> Mental Model -> Mechanism -> Example -> Implementation -> Trade-offs -> Advanced Topics -> References

over:

Definition A -> Definition B -> API list -> random implementation details -> edge cases.

## Reader model

Before drafting, infer or state:

- what the reader already knows;
- what the reader does not know;
- what the reader is trying to understand or build;
- what prior concepts are required.

Do not use "beginner" or "advanced" as a substitute for an actual reader model.

## Planning workflow

Before writing the main content, internally establish:

1. Reader Model
2. Problem Chain
3. Concept Dependency
4. Mental Model
5. Mechanism
6. Minimal Example
7. Real Implementation
8. Trade-offs / Optimization
9. Reference Material

The final document does not need to expose these labels literally, but its structure should reflect them.

## Default narrative structure

Use this structure unless the topic strongly suggests otherwise.

### 1. Problem

Start from a concrete technical limitation, failure mode, scaling pressure, or engineering question.

Explain what becomes difficult before introducing the mechanism that solves it.

### 2. Motivation

Explain why the problem matters in practice.

Prefer concrete system consequences such as memory usage, communication overhead, throughput, latency, synchronization, correctness, or implementation complexity.

### 3. Mental Model

Build the smallest useful intuitive model.

At this stage:

- avoid unnecessary terminology;
- ignore secondary details;
- state simplifications explicitly;
- use diagrams, data-flow descriptions, or small tables when they improve understanding.

The reader should be able to explain the idea informally before seeing the full implementation.

### 4. Minimal Mechanism

Show the smallest mechanism that makes the idea work.

Explain:

- what state exists;
- where data moves;
- which component owns each responsibility;
- when synchronization or transformation occurs.

Introduce terminology only when the reader now has a reason to need it.

### 5. Formal Model

Add mathematical definitions, invariants, complexity, tensor shapes, communication volume, or other formal detail when useful.

Do not introduce mathematics merely to make the document look rigorous.

Each formula should answer a concrete question raised by the earlier mental model.

### 6. Minimal Example

Prefer a minimal executable Python, PyTorch, or pseudocode example over a large production-style example.

The example should validate the mental model, not demonstrate every available API.

Explain the important state transitions and tensor/data shapes.

### 7. Real Implementation

Map the conceptual model onto a real framework or codebase.

For AI Infra topics, this may include:

- PyTorch;
- NCCL;
- Megatron-LM;
- vLLM;
- SGLang;
- verl;
- Slime;
- Ray;
- CUDA / Triton;
- framework source code.

Keep conceptual names and implementation names visibly connected.

### 8. Trade-offs

Explain why the system is designed this way instead of only explaining how it works.

Cover relevant dimensions such as:

- compute;
- memory;
- communication;
- latency;
- throughput;
- implementation complexity;
- fault tolerance;
- scalability.

Avoid generic "pros and cons" lists. Tie each trade-off to the mechanism previously explained.

### 9. Advanced Topics

Place optimizations, variants, edge cases, historical details, and neighboring concepts here when they are not required for the main understanding path.

Do not interrupt the main narrative merely because a related concept exists.

### 10. References

Keep reference-style material separate from the teaching flow.

Include useful items such as:

- papers;
- official documentation;
- important source files;
- relevant classes or functions;
- terminology lookup;
- follow-up reading.

## Cognitive dependency rules

Follow these rules strictly.

### Explain why before what

Before defining a mechanism, establish the problem that makes the mechanism necessary.

### Do not use unexplained prerequisites

If a section depends on a concept not yet introduced, either:

1. introduce the prerequisite first; or
2. defer the dependent section.

### One conceptual thread per section

A section should answer one main question.

Do not mix conceptual explanation, API reference, optimization trivia, and historical background unless the connection is essential.

### Progressive refinement

Start from a simplified model and then progressively remove simplifications.

A good sequence often looks like:

single device
-> multiple devices
-> synchronization requirement
-> collective communication
-> concrete algorithm
-> framework implementation
-> performance optimization

### Separate learning from reference

Teaching material should optimize for sequence.

Reference material should optimize for lookup.

Do not force both purposes into the same section.

## Writing style

Prefer clear technical prose over encyclopedic coverage.

Use headings that express questions or mechanisms rather than vague categories.

Prefer:

- "Why do gradients need synchronization?"
- "How does reduce-scatter change the communication pattern?"

over:

- "Background"
- "Details"
- "Other concepts"

Use examples with realistic tensor shapes, process counts, memory sizes, or communication patterns when they materially clarify the concept.

Avoid unnecessary repetition.

Avoid introducing multiple synonyms for the same concept unless the distinction matters.

## AI Infra-specific guidance

For distributed systems topics, explicitly track:

- process / worker identity;
- device ownership;
- tensor placement;
- communication direction;
- synchronization points;
- data-parallel, tensor-parallel, pipeline-parallel, or sequence-parallel boundaries when relevant.

For model architecture topics, explicitly track:

- input and output shapes;
- parameterization;
- intermediate representations;
- information flow;
- computational and memory complexity.

For RL / post-training systems, explicitly track:

- rollout generation;
- policy / reference / reward / value roles;
- data ownership;
- batching and packing;
- synchronization between training and inference;
- reward and advantage flow;
- where gradients do and do not propagate.

For optimization topics, always establish a baseline before presenting the optimization.

Explain what resource the optimization saves and what new cost or constraint it introduces.

## Cognitive dependency review

After drafting, review every section.

Ask:

- Why does the reader need this section now?
- Does it depend on an unexplained concept?
- Does it advance the main problem chain?
- Can it be moved later without hurting understanding?
- Is it teaching material or reference material?
- Did an implementation detail appear before the corresponding mental model?

If a section can move later without damaging comprehension, move it later.

If a detail is useful but not required for the main path, move it to Advanced Topics or References.

## Output priority

When there is tension between completeness and clarity, prefer clarity.

A shorter document with a coherent mental model is better than a complete document whose concepts appear in the wrong order.
