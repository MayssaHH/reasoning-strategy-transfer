# Reasoning Strategy Transfer

**When does a reasoning strategy transfer to a new mathematical problem?**

We study whether a generic strategy cue helps an LLM solve a transformed problem because the underlying solving mechanism still applies, or simply because the new problem looks similar to the original.

The project starts with mathematical problems that admit at least two valid, genuinely different approaches. For a selected strategy, we compare transformations that preserve its mechanism with transformations that keep the problem superficially similar but make that strategy insufficient.

**Current stage: collecting and reviewing candidate problem families.** This repository contains candidate family records, templates, a schema, and the contribution workflow. Experiments and results will be added as the work progresses.

## Research questions

1. If a strategy **z** solves an original problem **x**, does a generic cue for **z** still help on a transformed version of **x**?
2. Can we learn to choose an appropriate strategy cue for a new problem while keeping the solver fixed?

Our hypothesis is that a cue transfers positively when its solving mechanism is preserved, but provides little benefit or may hurt when that mechanism no longer applies. This is a hypothesis to test, not an established result.

## What counts as a different approach?

Different wording, notation, equation order, or algebraic rearrangements can express the same reasoning. We group approaches by their central mathematical justification, essential steps, and applicability conditions.

Meaningful differences may involve the mathematical tool, structural setup, or representational viewpoint—for example, a counting argument versus algebraic coefficient extraction, or synthetic geometry versus coordinate projection. These labels guide review; they do not establish distinctness by themselves.

Each shortlisted original must have at least two checked approaches from different supported clusters. We assess the supplied plans independently rather than accepting a source dataset's uniqueness labels.

## Problem families and transformations

A family contains one original problem, all its supplied approaches, validity checks, proposed clusters, a selection argument, transformation proposals, and a separate expert review. Later, it will also contain the developed and checked variants.

Choose a valid approach cluster **z** and keep its definition fixed. A paired proposal targets that same cluster in both tracks:

| Track | What changes? | What must hold? |
| --- | --- | --- |
| **Tᴾ: mechanism preserving** | Wording, context, notation, representation, or numerical parameters. The answer may change. | The selected strategy's conditions and essential reasoning remain valid. |
| **Tᶜ: mechanism changing** | An assumption, constraint, parameter, or goal, while the setup remains recognizably similar. | The selected strategy no longer provides a complete valid solving route under its fixed definition. |

These requirements concern the **selected cluster**, not every original approach. Another original cluster may still solve Tᶜ. Choosing a different method, changing the answer, or making the calculation longer does not by itself establish a mechanism change.

During collection, propose ideas and explain their justification and open questions. Leave `variant` as `null`; mark a blocked idea explicitly instead of forcing a transformation label.

## Planned study

The [research slides](https://docs.google.com/presentation/d/1zNKemX7_j4ED8ktBLKQrCUK36iiH021Zr55aEyusraY/edit?usp=sharing) outline the following study:

- **Build a collection targeting 300 original families**, each with multiple valid approaches and tailored preserving/changing variants.
- **Validate the mathematics and transformation labels**, using executable answer checks where applicable and independent review by two mathematically trained reviewers. Keep ambiguous cases identifiable for separate analysis.
- **Split by family**, keeping each original and its related variants together across training, development, and test sets.
- **Compare cue conditions**: the selected strategy cue, a non-matching strategy cue, a style-only cue, and no cue. Keep the solver and settings fixed and randomize cue assignment.
- **Measure accuracy gains** relative to no cue on each transformation track:

$$
\Delta_z^P = P(\mathrm{correct}\mid T^P(x),\text{cue for }z)-P(\mathrm{correct}\mid T^P(x),\text{no cue})
$$

$$
\Delta_z^C = P(\mathrm{correct}\mid T^C(x),\text{cue for }z)-P(\mathrm{correct}\mid T^C(x),\text{no cue})
$$

The hypothesized pattern is positive transfer under Tᴾ and little benefit or harm under Tᶜ. The other cue conditions help distinguish strategy-specific effects from generic prompting effects. A later stage will investigate a strategy router that selects cues for unseen problems while keeping the solver frozen.

These are planned stages. The current collection template records a working analysis and Mayssa's review; the later independent-review protocol and experiment implementation remain to be developed. Prior-work results discussed in the slides are background, not results of this project.

## Repository structure

| Path | Purpose |
| --- | --- |
| [`families/`](families/) | One JSON file per original problem, including its review status. |
| [`templates/family_template.json`](templates/family_template.json) | Clean template to copy and fill. |
| [`templates/family_template_annotated.jsonc`](templates/family_template_annotated.jsonc) | Field-by-field instructions, with comments. |
| [`schema/family.schema.json`](schema/family.schema.json) | JSON Schema for structural checks. |
| [`docs/FIELD_GUIDE.md`](docs/FIELD_GUIDE.md) | Readable guide to the fields and review criteria. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Claiming, preparing, and submitting a family. |
| [`.github/`](.github/) | Family-claim issue and pull-request templates. |

## Start contributing

1. Agree on a domain split, then search existing files and open/closed issues before claiming a source problem. Domain labels are assigned by the team; source IDs prevent overlap, including mixed-domain cases.
2. Open a **Claim a family** issue and record the source, exact problem ID, and collector.
3. Read the [annotated template](templates/family_template_annotated.jsonc), then copy the [clean template](templates/family_template.json) to `families/<family_id>.json`.
4. Preserve and check every supplied approach, justify the clustering, and propose Tᴾ/Tᶜ ideas for the same fixed cluster.
5. Submit a pull request for review. Use short, meaningful commits, such as `Add train_0123 family` or `Clarify symmetry check`.

The initial assignment is **five qualifying candidate families per contributor**. Held candidates may be tracked, but do not count toward that requirement.

**A merge or schema check is not mathematical approval.** Record the actual decision in `expert_review`; accepting an original problem does not validate its proposed transformations.

## Source conventions

The initial source is [`helmsman12/LLM_reasoning_diversity`](https://github.com/helmsman12/LLM_reasoning_diversity), using `data/train.jsonl`. Store the source path and exact record `index` in `source`; this is not a line number or an independently recovered upstream MATH identifier.

Use a stable filename matching `family_id`, such as `train_0123.json`. Keep one record per `(source.file, source.problem_id)` pair. Use a different prefix for another dataset or split. Approach IDs (`A1`, `A2`, …) and cluster IDs (`C1`, `C2`, …) are local to each family.

The full source dataset is not bundled. This repository does not assign a new license to upstream material.
