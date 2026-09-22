---
name: topic-learning-site
description: Design and maintain a topic-oriented learning website that organizes knowledge as interconnected pages rather than linear lessons. Use when building a focused technical wiki, concept site, or learning hub around one topic.
---

# Topic Learning Site

Build a learning website around one topic.

The site should behave like a small knowledge space, not a course syllabus.

The goal is to help the reader:

- understand the big picture;
- discover the important concepts;
- follow a sensible learning path;
- jump directly to a specific concept;
- understand how pages relate to each other.

## Core principle

Organize by concept relationships, not lesson numbers.

Prefer:

Topic
-> Concept Map
-> Pages
-> Cross-links
-> Suggested Paths

over:

Lesson 1
-> Lesson 2
-> Lesson 3
-> Lesson 4

A topic may have a recommended reading order, but the site itself should remain navigable non-linearly.

## Workspace model

Treat the site files as the long-term source of truth.

A topic workspace should normally contain:

```text
topic-site/
├── MISSION.md
├── MAP.md
├── RESOURCES.md
├── docs/
│   ├── index.md
│   ├── concepts/
│   ├── glossary.md
│   └── sources.md
└── site configuration
```

The exact site generator is optional.

Markdown-first static site generators such as VitePress, Starlight, or similar tools are usually preferable to maintaining raw HTML by hand.

## MISSION.md

Define why the site exists before creating pages.

Keep it short.

Include:

- Topic
- Reader goal
- Reader's assumed knowledge
- Important unknowns
- Desired depth
- Scope boundaries

Example:

```markdown
# Mission

Topic: PyTorch Distributed

Goal:
Understand the distributed communication concepts needed before reading Megatron-LM.

Assumed knowledge:
- Python
- basic PyTorch
- Transformer basics

Out of scope by default:
- production deployment
- exhaustive API reference
- low-level NCCL implementation
```

Use the mission to reject content that is relevant to the topic but irrelevant to the reader's goal.

## RESOURCES.md

Build a small source base for the topic.

Prefer:

1. official documentation;
2. original papers;
3. authoritative source code;
4. strong technical articles or talks;
5. community material when useful for practical context.

Record enough information to revisit the source later.

Do not turn RESOURCES.md into an indiscriminate link dump.

## MAP.md

Create the topic map before creating many pages.

The map should identify:

- core concepts;
- prerequisites;
- related concepts;
- major branches of the topic;
- optional deeper areas.

Example:

```text
Distributed Training
├── Process Model
│   ├── process
│   ├── rank
│   └── process group
├── Communication
│   ├── point-to-point
│   └── collectives
│       ├── broadcast
│       ├── all-reduce
│       ├── all-gather
│       └── reduce-scatter
└── Parallelism
    ├── data parallelism
    ├── tensor parallelism
    └── pipeline parallelism
```

The map is not merely navigation.

It is the conceptual model of the site.

Update it when the understanding of the topic changes.

## Page design

Each concept page should have one clear conceptual responsibility.

A page should normally explain one concept, mechanism, distinction, or relationship.

Prefer pages such as:

- `all-reduce.md`
- `process-group.md`
- `data-parallelism.md`

over pages such as:

- `distributed-training-part-3.md`
- `misc-notes.md`
- `advanced-topics-2.md`

Use the `ai-infra-learning-note` skill or an equivalent concept-first writing approach when writing an individual technical concept page.

## Page metadata

When useful, give each concept page lightweight metadata.

Example:

```yaml
---
title: AllReduce
summary: Aggregate values across processes and return the result to every process.
prerequisites:
  - collective-communication
related:
  - reduce
  - all-gather
  - reduce-scatter
---
```

Keep metadata minimal.

Only add fields that support navigation, validation, or generation.

## Page structure

A concept page should usually answer:

1. What is this?
2. Why does it exist?
3. What is the simplest mental model?
4. How does it work?
5. What does it depend on?
6. What is it related to?
7. What should the reader explore next?

Do not force every page to use identical headings when another structure is clearer.

## Home page

The home page should orient the reader.

It should normally contain:

- what the topic is;
- why it matters;
- the big picture;
- the topic map;
- a suggested learning path;
- direct entry points into major concept groups.

Avoid generic welcome text that adds no information.

## Learning paths

Support recommended paths without turning the whole site into a course.

For example:

```text
Suggested path for first-time readers:

Process
-> Rank
-> Process Group
-> Collective Communication
-> AllReduce
-> Data Parallelism
```

Different paths may exist for different goals.

For example:

- conceptual foundation;
- source-code reading;
- performance optimization.

Learning paths are views over the knowledge graph, not the primary storage structure.

## Cross-linking

Pages should connect to each other deliberately.

Use links for:

- prerequisites;
- concepts used by the current mechanism;
- closely related alternatives;
- natural next topics.

Avoid excessive linking merely because two pages share terminology.

A reader should understand why a linked page matters.

## Navigation

Navigation should reflect conceptual structure.

Prefer:

```text
Foundations
Communication
Parallelism
Memory
Runtime
```

over:

```text
Chapter 1
Chapter 2
Chapter 3
```

Keep navigation shallow enough that the reader can form a mental model of the whole topic.

## Content growth

Grow the site from the map outward.

A good order is:

1. define the mission;
2. collect core resources;
3. create the topic map;
4. identify the minimum useful page set;
5. write core concept pages;
6. add cross-links;
7. add optional deeper branches.

Do not begin by generating dozens of pages.

A small coherent site is better than a large disconnected one.

## Optional site implementation

The content architecture should not depend heavily on a specific framework.

When implementation is required, prefer a static documentation stack with:

- Markdown or MDX source;
- file-based routing;
- sidebar navigation;
- full-text search;
- code highlighting;
- reusable layout and styles;
- static HTML output.

VitePress or Starlight are good defaults for a personal technical learning site.

Raw HTML is acceptable when the site is intentionally very small or highly custom.

## Review

Before considering the site coherent, check:

- Does the home page explain the whole topic at a glance?
- Does every core page have a clear responsibility?
- Are prerequisites introduced before dependent concepts?
- Does MAP.md still match the actual pages?
- Are there important orphan pages?
- Are related concepts cross-linked?
- Can a new reader follow a sensible path?
- Can an experienced reader jump directly to a concept?
- Are implementation details overwhelming conceptual pages?
- Are there pages that should be merged or split?

## Output priority

Prioritize:

1. coherent concept structure;
2. clear page boundaries;
3. useful navigation;
4. conceptual cross-links;
5. visual polish.

A beautiful site with a poor knowledge structure is still a poor learning site.
