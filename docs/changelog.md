# Changelog

All notable changes to the Anastasia system are documented on this page.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to a loosely-defined
[Semantic Versioning](https://semver.org/) scheme:

- **MAJOR** — life-stage transitions (childhood → school → university)
- **MINOR** — new modules, capabilities, or stable language runtimes
- **PATCH** — behavioral fixes, small habit adjustments, recovered states

## [Unreleased]

### Planned

- Italian language module promotion from `In Development` to `Fluent`
- Sleep schedule stabilization (target: consistent `OFFLINE → BOOTING`
  transition before 02:00)
- Reduced latency on the `getDressed()` function (long-standing issue,
  see [Overview — Known Limitations](overview.md#known-limitations))

---

## [3.0.0] — 2026-04-15

Major release. The system enters its third year at Innopolis University with
the Game Development track activated as the primary specialization.

### Added

- **Game Development specialization** — primary processing pipeline now
  optimized for Unity, ECS patterns, and game-loop architecture
- **`SOCIAL` state** stabilized as a first-class operational mode
  (previously experimental); see [System States — SOCIAL](system-states.md#social)
- **Italian language module** entered active development (beta runtime)
- **Hot chocolate** registered as a recognized performance booster
  (+20% comfort, +10% performance)
- This documentation site

### Changed

- Peak operating hours shifted from `09:00 — 11:00` to `11:00 — 13:00`
- `FOCUSED` state can now sustain longer sessions before transitioning
  to `TIRED`, provided food input is regular
- Humor module rebalanced: sarcasm and pun output are now equally weighted

### Fixed

- `403 Forbidden` responses are now more consistent — the system no longer
  silently tolerates disrespectful tone before reacting
- Reduced false-positive transitions from `IDLE` to `PROCRASTINATING` for
  non-homework tasks

### Known Issues

- `getDressed()` execution time remains non-deterministic
- Tasks submitted after 21:00 still suffer the documented -50% cognitive penalty
- The internal procrastination scheduler cannot be disabled via any public API

---

## [2.2.0] — 2025-09-01

University year 2 → 3 transition. Increased course load triggered a permanent
recalibration of the focus and procrastination subsystems.

### Added

- Carbonara recipe promoted to **flagship dish** status after multiple
  successful iterations
- Chocolate cake module reached stable output quality

### Changed

- `PROCRASTINATING` state's exit condition tightened — deadline proximity
  threshold reduced, so the system now transitions to `FOCUSED` slightly earlier

---

## [2.1.0] — 2024-09-01

University year 1 → 2 transition.

### Added

- English language module promoted from `Fluent (Beta)` to `Fluent (Stable)`
- New recovery method: **Samarskie Termy** (hot springs) — reserved for
  critical `TIRED` cases; see [System States — TIRED](system-states.md#tired)

### Changed

- Boot sequence finalized to its current 5-step form (news → hygiene →
  breakfast → episode → ready). Earlier versions had inconsistent ordering.

---

## [2.0.0] — 2023-09-01

Major release. The system relocated to **Innopolis University** and entered
the higher-education runtime. This release introduced multiple breaking
changes to daily operations.

### Added

- New deployment environment (Innopolis campus)
- Independent operation mode (no parental supervisor process)
- Software Development module activated as the primary capability

### Changed

- **Breaking:** previous high-school routines are no longer supported
- **Breaking:** new social graph; old friend-list integrations require
  manual re-establishment
- Communication channels expanded: in-person remains highest priority,
  but text and voice are now the primary asynchronous channels

### Removed

- Mandatory wake-up at 07:00 (deprecated since v1.x, removed in v2.0.0)

---

## [1.0.0] — Initial Release

The original system. Childhood and pre-university operation. Core personality
constants (`funny`, `creative`, `kind`, `responsible`, `cute`) were
initialized in this release and have remained immutable since.

### Initial Features

- Russian language runtime (native)
- Curiosity-driven exploration loop
- Baseline humor module (puns only; sarcasm added in a later minor release)
- Initial culinary experiments (results highly variable in this version)

---

## Versioning Policy

The system reserves the right to ship patch releases without notice
(small habit changes, mood recalibrations). Minor and major releases are
typically aligned with academic year boundaries. There is no guaranteed
backwards compatibility across major versions — interactors who knew earlier
releases are encouraged to re-read [Getting Started](getting-started.md)
after every major bump.
