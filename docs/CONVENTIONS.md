# Repository Conventions

## Repository layout

```text
maverick-skills/
├── skills/
├── templates/
├── examples/
└── docs/
```

## Skill layout

A skill should normally use:

```text
skills/<skill-name>/
├── SKILL.md
├── references/
└── assets/            # optional
```

Only add files that improve reuse or maintainability.

## Naming

Use lowercase kebab-case for skill directories.

Examples:

- `ai-infra-learning-note`
- `paper-reading`
- `source-code-walkthrough`

Prefer names that describe a reusable capability rather than a one-off task.

## Design principle

A skill should encode behavior that is worth reusing.

Do not turn every long prompt into a skill. A useful skill normally captures one or more of:

- a stable workflow;
- domain-specific reasoning structure;
- output quality constraints;
- tool-use conventions;
- repeatable review criteria.

## Maintenance

When changing a skill, test it against existing examples.

Prefer small behavioral changes over repeatedly expanding `SKILL.md` with unrelated rules.

If the skill starts serving multiple unrelated purposes, split it.
