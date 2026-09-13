# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-09-13

### Added
- Initial release of `/grill-me` skill
- Three diagnostic levels: default, critical, deep
- Auto-detection logic for level selection
- Structured survey system using `ask_user_input_v0`
- Comprehensive documentation in English and Spanish
- Examples for each use case
- Integration guide for step-by-step workflows
- Full SKILL.md specification

### Features
- `/grill-me` (default) — Ambiguity and trade-off resolution
- `/grill-me critical` — Irreversible action confirmation
- `/grill-me deep` — Technical complexity exploration
- Auto-trigger based on request characteristics
- Case-insensitive parameter parsing
- Multiple decision handling in single survey

---

## [Unreleased]

### Planned
- Video walkthrough of usage patterns
- Integration examples with specific Claude workflows
- Community examples repository
- Multi-language support expansion (Portuguese, French)
- Advanced triggering logic with project context
- History tracking for repeated decisions

---

## Notes

### Semantic Versioning

- **MAJOR** (x.0.0) — Breaking changes to API or behavior
- **MINOR** (0.x.0) — New features, backward compatible
- **PATCH** (0.0.x) — Bug fixes, documentation

### Release Cadence

Releases happen as needed. No fixed schedule.
