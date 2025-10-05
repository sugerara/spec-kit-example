<!--
Sync Impact Report

- Version change: template -> 0.1.0
- Modified principles:
	- [PRINCIPLE_1_NAME] -> Library-First
	- [PRINCIPLE_2_NAME] -> CLI Interface
	- [PRINCIPLE_3_NAME] -> Test-First (NON-NEGOTIABLE)
	- [PRINCIPLE_4_NAME] -> Integration Testing
	- [PRINCIPLE_5_NAME] -> Observability & Versioning
- Added sections: Filled `Additional Constraints` and `Development Workflow`
- Removed sections: none
- Templates reviewed (checked for alignment):
	- .specify/templates/plan-template.md ✅ checked
	- .specify/templates/spec-template.md ✅ checked
	- .specify/templates/tasks-template.md ✅ checked
	- .specify/templates/agent-file-template.md ✅ checked
	- .specify/templates/commands/*.md ⚠ pending (no command files present)
- Runtime docs:
	- README.md ⚠ missing - create or update README with constitution reference
- Follow-up TODOs:
	- RATIFICATION_DATE: TODO(RATIFICATION_DATE): please confirm the original adoption date of this constitution
	- Verify agent-specific command files (if added) do not reference vendor-specific agent names
-->

```markdown
# spec-kit-example Constitution

## Core Principles

### Library-First
Every feature starts as a standalone library. Libraries MUST be self-contained, independently
testable, and documented. Every library MUST have a clear, singular purpose. Organizational-only
libraries are PROHIBITED unless documented in Complexity Tracking and explicitly approved.

### CLI Interface
Project tools and libraries SHOULD expose functionality via a command-line interface where
practical. Text I/O protocol MUST follow: stdin/args → stdout, errors → stderr. Outputs MUST
support both JSON (for automation) and human-readable formats (for debugging).

### Test-First (NON-NEGOTIABLE)
Test-driven development is mandatory: tests MUST be written and committed before implementation.
Tests MUST fail initially; implementation then proceeds to satisfy them following Red-Green-Refactor.
This principle is NON-NEGOTIABLE for production-facing code and critical scripts.

### Integration Testing
Integration tests MUST cover library contracts, contract changes, inter-service communication,
and shared schemas. Any change that affects cross-project or runtime behavior MUST include
appropriate integration tests.

### Observability & Versioning
Components that run in production MUST provide structured logging and contextual error details.
Metrics and tracing SHOULD be added where they materially improve operability. Releases MUST
follow semantic versioning; breaking changes MUST comply with the Governance amendment
and migration procedures.

## Additional Constraints
Technology choices and constraints MUST be documented in the feature's `plan.md`. Defaults and
requirements:

- Shell tooling: POSIX-compatible Bash scripts are the default for automation scripts.
- Protocols: prefer text I/O with JSON as the structured interchange format.
- Security and compliance requirements MUST be called out in `plan.md` and resolved during Phase 0.

If a constraint is unknown, mark it as `TODO` in the plan and resolve it during Phase 0 research.

## Development Workflow
- Code review is REQUIRED for changes to `src/`, `scripts/`, and `.specify/` content.
- Pull requests MUST include a short "Constitution Check" statement and link to the relevant
	plan/spec entries showing compliance.
- Complexity deviations (exceptions) MUST be logged in Complexity Tracking and approved by at
	least one senior maintainer.
- Releases: tags use `vMAJOR.MINOR.PATCH`. Changelogs MUST highlight constitution-relevant changes
	and migration guidance for breaking updates.

## Governance
This Constitution is the authoritative source for project norms, minimum requirements, and the
amendment process. Amendments follow the semantic rules below.

Amendment procedure:
1. Open a PR updating `.specify/memory/constitution.md` with rationale and a migration plan.
2. Classify the change: MAJOR (principle removal/semantic redefinition), MINOR (new principle or
	 material guidance), PATCH (clarifications, typos).
3. Obtain approval from two reviewers, including at least one maintainer.
4. Merge and update the Last Amended date.

Versioning policy:
- MAJOR: Backward-incompatible governance/principle removals or redefinitions.
- MINOR: New principle/section added or materially expanded guidance.
- PATCH: Clarifications, wording, typo fixes, non-semantic refinements.

Compliance review expectations:
- Every PR that affects production behavior MUST include a Constitution Check summary.
- CI SHOULD validate automated Constitution Check items where feasible (format, presence of
	compliance statement).

**Version**: 0.1.0 | **Ratified**: TODO(RATIFICATION_DATE): confirm adoption date | **Last Amended**: 2025-10-05
```
