# Human Interaction Documentation

Technical documentation for **Anastasia** — a personal profile written in the
voice and conventions of an API reference. Built with
[MkDocs Material](https://squidfunk.github.io/mkdocs-material/) and deployed to
GitHub Pages.

**Live site:** https://mituttta051.github.io/human-interaction-documentation/

## What this is

The first homework assignment described who I am: background, traits,
languages, things I do well, things I avoid. This second assignment turns that
profile into a static documentation site, treating the person as a system that
others "interact with" through messages, requests, and conversations.

The framing is intentional — it lets the assignment exercise real
documentation patterns (API reference, state diagrams, error handling, FAQ)
on content that would otherwise be a flat bio.

## Repository layout

```
.
├── docs/                  # All Markdown source for the site
│   ├── index.md           # Landing page, system summary, quick navigation
│   ├── overview.md        # Architecture, modules, performance factors
│   ├── getting-started.md # Prerequisites, boot sequence, first interaction
│   ├── communication-api.md # Channels, methods, input/output schemas
│   ├── system-states.md   # State machine: IDLE, FOCUSED, TIRED, ...
│   ├── journey.md         # Customer Journey Map of a typical interaction
│   ├── error-handling.md  # Status codes, anti-patterns, retry policy
│   └── faq.md             # Common questions and troubleshooting
├── mkdocs.yml             # Site config (theme, nav, extensions)
├── requirements.txt       # MkDocs + Material pins
└── .github/workflows/
    └── deploy.yml         # Build + deploy to GitHub Pages on push to main
```

## Why this structure

The page order mirrors the path a real reader takes through unfamiliar
technical documentation, applied to the goal of understanding a person:

1. **Home** — what is this thing, at a glance.
2. **Overview** — architecture and capabilities, before any interaction details.
3. **Getting Started** — the minimal path to a first successful interaction.
4. **Communication API** — the reference: every supported method and its schema.
5. **System States** — behavioral context the API alone cannot express
   (mood, energy, focus); needed before reading error handling.
6. **User Journey** — a Customer Journey Map of one typical interaction,
   tying stages → user emotion → system state → friction → mitigation.
7. **Error Handling** — what goes wrong and how to recover; depends on
   understanding states.
8. **FAQ** — fallback for questions the linear narrative doesn't answer.

This is the standard tutorial → reference → troubleshooting arc for technical
documentation, with **System States** and **User Journey** added as the
behavioral layer that turns a static API reference into a profile of a person.

## CJM (Customer Journey Map) approach

The assignment suggested using the CJM approach. Two pages do this explicitly:

- **`system-states.md`** — system-side of the journey: the state machine
  showing what mode the "system" is in at each point and how transitions
  happen.
- **`journey.md`** — interactor-side of the journey: a stage-by-stage table of
  what the user does, feels, and encounters when working with the system,
  with friction points and mitigations.

The error-handling anti-patterns (Morning Ambush, Late Night Task Dump,
The Hunger Ignore, Pressure Escalation, The Vague Loop) are friction points
from the journey, documented as recoverable failure modes.

## Local development

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve            # http://127.0.0.1:8000
mkdocs build --strict   # same command CI runs; fails on broken links
```

## Deployment

Every push to `main` triggers `.github/workflows/deploy.yml`, which runs
`mkdocs build --strict` and publishes the result via the official
`actions/deploy-pages` action. No `gh-pages` branch is involved.
