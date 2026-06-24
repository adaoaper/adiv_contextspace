---
name: adiv-contextspace
description: Use when organizing ADIV contextual structure, creating or reviewing ADIV cycles, converting bugs/features/research/writing tasks into actionable contextual cycles, or structuring shared human/AI work context with reference, exploration, candidate, and official artifact states.
---

# ADIV-ContextSpace

Version 0.1

ADIV-ContextSpace is a dynamic structure for building and evolving shared situational awareness oriented toward achieving objectives.

The structure organizes work through ADIV cycles, allowing participants to maintain enough shared understanding to analyze, decide, implement, and validate actions throughout the evolution of a solution.

ADIV stands for:

- Analyze;
- Decide;
- Implement;
- Validate.

## Context Space

The goal is to preserve enough shared situational awareness for humans and AI to analyze, decide, implement, and validate work with context.

For the conceptual reference, read `adiv_contextspace_v0_1.md` at the ADIV-ContextSpace root when needed.

## Core Structure

Default hierarchy:

```text
adiv_contextspace/
  project/
    division/
      grouping/
        cycle/
          adiv.md
          reference/
            reference.md
          exploration/
            exploration.md
          candidate/
            candidate.md
          official/
            official.md
          record/
            record_cN.md  # only when an item is marked [Cn+]
```

Meanings:

- `project`: product, system, book, initiative, client, or solution.
- `division`: broad contextual division such as module, domain, part, area, or process.
- `grouping`: local context such as routine, screen, report, flow, rule, chapter, theme, or integration.
- `cycle`: actionable ADIV cycle with its own objective, scope, history, and artifacts.

Everything that has `adiv.md` is an ADIV cycle. Everything above it is location context.

## Artifact States

Inside a cycle:

- `reference/`: material used to build understanding, including docs, APIs, contracts, examples, logs, screenshots, payloads, evidence, and links or copies of official artifacts from other cycles when they are used as input.
- `exploration/`: work produced during investigation or design, including drafts, diagrams, hypotheses, alternatives, experiments, and intermediate models.
- `candidate/`: mature proposal ready for evaluation.
- `official/`: validated or accepted result of the cycle, such as approved definitions, final scripts, consolidated decisions, accepted text, or current valid models.
- `record/`: optional expanded contextual record for actionable decisions, implementations, and validations when `adiv.md` should remain compact.

Each artifact folder may contain a general notes file:

- `reference/reference.md`
- `exploration/exploration.md`
- `candidate/candidate.md`
- `official/official.md`
- `record/record_cN.md` only when an item is marked `[Cn+]`

These files are lightweight notes and general-use entry points for the folder. They are not formal documentation requirements. Use them to summarize what is in the folder, link important artifacts, and preserve useful context for humans and AI.

When the human explicitly asks to create an ADIV cycle, create the default cycle structure, including the expected folders and base files, even if some files start empty.

For existing lightweight cycles or small context organization, `adiv.md` alone may be enough.

Create `record/` as part of the default cycle structure when explicitly creating an ADIV cycle. Do not create `record/record_cN.md` unless the corresponding item is marked `[Cn+]`, the human asks for expanded detail, or a decision, implementation, or validation would overload `adiv.md`.

`record/` does not replace `reference/`, `exploration/`, `candidate/`, or `official/`. Specifications and current valid rules belong in `official/`. Evidence, research, comparisons, and hypotheses belong in `reference/` or `exploration/` according to maturity.

## Decision Gate Before Implementation

Any implementation must first be analyzed and recorded in `adiv.md` under the `## Decision` section.

When AI is in direct interaction with the human, it must record the decision and wait for direct implementation instruction before changing code, files, or final artifacts.

The purpose of this gate is to ensure that human and AI are aligned on what will be implemented.

## Workflow

1. Identify the cycle objective.
2. Place the cycle in the smallest useful context.
3. If explicitly creating a new ADIV cycle, create the complete folder/file structure.
4. Create or update `adiv.md` as the operational entry point.
5. Classify artifacts by maturity and role.
6. Use `official/` artifacts from prior cycles as `reference/` for later cycles when useful.
7. Keep `adiv.md` compact; move expanded decision context to `record/record_cN.md` only when useful.

## Open Analysis and Exploration

During analysis and exploration, do not create new artifacts without a direct indication from the human. The idea can be explored naturally in chat before becoming an artifact.

## adiv.md as Operational Index

`adiv.md` is the operational entry point and compact index of the cycle. It should preserve enough situational awareness to continue the work, but should not duplicate detailed artifact content.

Avoid copying complete specifications into `adiv.md`, such as table models, long field lists, full SQL scripts, payloads, long business rules, full proposals, final texts, or extensive examples. Put those details in the proper artifact folder according to maturity:

- `reference/` for source material, evidence, external references, logs, payloads, or links/copies of official artifacts from other cycles when they are used as input.
- `exploration/` for drafts, alternatives, hypotheses, proposed models, examples, and intermediate designs.
- `candidate/` for mature proposals ready for evaluation.
- `official/` for validated definitions, approved scripts, final rules, and current valid models.

In `adiv.md`, point to the artifact and summarize its role in the cycle.

When an artifact evolves, update the artifact itself and record the transition in `adiv.md` only as operational context, decision, implementation, validation, or pending work. This reduces duplicated maintenance and avoids stale details in the cycle entry point.

## adiv.md Template

```markdown
# <Cycle title>

## Identification

- Created on:
- Participants:
- Origin:

## Objective

## Context

## Analysis

Point to context, evidence, exploration, or official specifications. Do not tag analysis items by default.

Examples:

- Use `official/calculation_requirement_x.md` as the basis for the calculation.
- Compare alternatives documented in `exploration/calculation_alternatives.md`.
- Use evidence from `reference/calculation_error_logs.md`.

## Decision

Actionable decisions. This is where internal trace tags start.

## Implementation

Implementation of the decision.

## Validation

Validation of the decision and implementation.

## Pending
```

`## Identification` is a general-purpose metadata block for identifying the cycle. It may receive other fields as needed, such as ticket, client, system, module, requester, source document, related cycle, or external reference.

## Internal Trace Tags

Use tags only when traceability is useful.

```text
[Cn]  = the item belongs to actionable decision/internal turn Cn.
[Cn+] = the item belongs to Cn and has expanded contextual record in record/record_cn.md.
```

Operational rules:

- Tags are reserved for `Decision`, `Implementation`, and `Validation`.
- `Analysis` does not use tags by default; it points to artifacts and context.
- The tag starts in `Decision`.
- `Implementation` and `Validation` reuse the same tag when they implement or check that decision.
- Put the tag at the end of the item as secondary metadata.
- A tag applies only to the line where it appears.
- If several lines belong to the same internal turn, repeat the tag on each line.
- `+` does not mean more important; it means there is expanded contextual record in `record/record_cn.md`.

Example:

```markdown
## Decision

- Use `BaseInvoiceIntegrationService.cs` as the reference implementation for `NewInvoiceIntegrationService.cs`. [C1]
- Add `ignoreOptionalCostCenter` to configuration and posting persistence for the financial integration flow. [C5+]

## Implementation

- Change the configuration, save, and posting persistence points. [C5+]

## Validation

- Validate posting persistence when optional cost center is disabled. [C5+]
```

## record/

`record/` is expanded contextual record on demand.

Use `record/record_cN.md` to detail the internal turn marked as `[Cn+]` in `adiv.md`.

`record/` exists only to keep `adiv.md` compact when a decision, implementation, or validation needs expanded operational detail.

Default shape:

```markdown
# Record C5

## Decision

## Implementation

## Validation
```

No block is mandatory. Use only what the context needs. Internal subdivisions are free and contextual.

`record/` is not a diary of analysis and is not the main place for specifications.

Core principle:

```text
ADIV should increase continuity, not bureaucracy.
The level of detail is decided by usefulness to the context.
```

## Naming

If the cause or solution is unknown, prefer `analyze_...`.

If the action is clear, use a direct verb such as `create_`, `add_`, `change_`, `fix_`, `remove_`, or `validate_`.

Good examples:

```text
analyze_error_422_update_invoice_status
adjust_request_signature
create_financial_structure_registry
add_dashboard_trend_indicator
fix_expense_group_calculation
validate_cost_center_mapping
analyze_new_tax_regulation
implement_new_tax_regulation
```

Avoid vague names:

```text
module_creation
implementation
adjustments
miscellaneous
new
```

## Creation of an ADIV Cycle Structure

When the human requests the creation of an ADIV cycle without providing further context, the AI must create only the
base structure defined in this skill, with no AI comments in `adiv.md` sections or auxiliary `.md` files. The source
of truth for the structure is this skill, not similar folders.

The administrative decision to create an ADIV cycle must not be annotated in any cycle.

## Considerations

- Context Space is oriented toward resolving objectives with situational awareness; the contextual trail is a consequence of the work, not the main objective.
- Context Space stores contextual artifacts that support solution development.
- Implementations are performed and maintained in their own origin repositories.
- The scope of the objective is at the human's discretion. It may be narrow, with only `adiv.md`, or broad, with several decisions and artifacts in auxiliary folders.
- The objective may involve analysis, exploration, prototyping, documentation, coding, and other solution-development stages, in one ADIV or in multiple ADIVs related by reference.
- One ADIV may contain several rounds of decision, implementation, and validation for the same objective, at the human's discretion.
- Tags `[Cn]` and `[Cn+]` are preferably generated and maintained by AI.
- Auxiliary folders `reference`, `exploration`, `candidate`, and `official` are not stages or a mandatory sequence. They are available states, used on demand, at the human's discretion.
- `official` is a maturity state defined at the human's discretion.
- `adiv.md` is the living operational context for resolving the cycle objective, not necessarily a future source of truth.
- Validation records the checks, evidence, and human evaluation related to whether the objective was achieved.
