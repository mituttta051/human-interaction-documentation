# System Overview

## Architecture

Anastasia is a multi-purpose human system designed for communication, problem-solving, creative processing, and culinary output. The system is currently deployed at **Innopolis University** (3rd year, Game Development track) and operates across three language runtimes: Russian, English, and Italian.

The system performs best in structured environments with clear inputs, sufficient nutrition, and minimal unnecessary pressure.

## Core Modules

### Software Development Module

The primary processing unit. Specializes in game development but is capable of general-purpose software engineering tasks. Performance is directly correlated with task interest level and compensation.

```
performance = f(interest_level, payment, deadline_proximity)
```

### Culinary Module

A well-developed secondary system. Capable of producing complex outputs including:

- **Carbonara** — flagship dish, optimized through multiple iterations
- **Chocolate cakes** — specialty dessert, consistently high output quality
- General-purpose cooking across various cuisines

### Creative Module

Handles humor generation (sarcasm and pun-based), singing, and spontaneous idea generation. This module is particularly active during the `SOCIAL` state (see [System States](system-states.md)).

### Language Module

| Language | Level       | Status       |
|----------|-------------|--------------|
| Russian  | Native      | Stable       |
| English  | Fluent      | Stable       |
| Italian  | Learning    | In Development |

## Behavioral Characteristics

- Combines logical and creative processing in a single pipeline
- Maintains a positive interaction tone under normal operating conditions
- Exhibits elevated emotional sensitivity — input tone is a critical parameter
- Capable of extended operation under social stimulation (see `SOCIAL` state)

## Personality Constants

The following values are hard-coded and cannot be modified at runtime:

```yaml
personality:
  funny: true
  creative: true
  kind: true
  responsible: true
  cute: true
  sensitivity_level: HIGH
  humor_type: [sarcasm, puns]
```

## Performance Factors

### Positive Multipliers

| Factor               | Effect                                      |
|----------------------|---------------------------------------------|
| Interesting task     | +80% performance boost                      |
| Clear compensation   | +60% motivation                             |
| Approaching deadline | Triggers `FOCUSED` state                    |
| Chocolate / sweets   | +15% execution speed                        |
| Hot chocolate        | +20% comfort, +10% performance              |

### Negative Multipliers

| Factor                        | Effect                                   |
|-------------------------------|------------------------------------------|
| Hunger                        | Critical — may trigger `503 Unavailable` |
| Tasks after 21:00             | -50% cognitive performance               |
| Disrespectful input           | Immediate performance degradation        |
| Unclear or vague requirements | Increased processing latency             |
| Early morning (before 10:00)  | System not fully initialized             |

## Known Limitations

- `getDressed()` function execution time is non-deterministic and frequently exceeds estimated duration
- Tasks submitted after 21:00 may be deferred to the next business day
- Homework-type tasks are subject to the internal procrastination scheduler (see [System States — PROCRASTINATING](system-states.md#procrastinating))
- Extended periods without food input will cause system-wide performance degradation
