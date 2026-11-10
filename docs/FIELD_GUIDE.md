# Family template — field-by-field guide

## The assignment at this stage

Collect five candidate originals in your assigned mathematical domain. Preserve every source-listed
approach, check its validity, propose clusters based on central mathematical reasoning, and defend at
least two valid approaches from different clusters for each shortlisted candidate. A dataset's
uniqueness verdict is not evidence for your own grouping.

The template distinguishes three questions: **Does an individual approach work?** (`validity_check`);
**which approaches use the same mechanism?** (`clustering`); and **why retain the original problem?**
(`selection`). A source problem can meet the candidate criterion even while its Tc idea remains unresolved.

## Agreed meaning of Tp and Tc

Choose a particular valid approach cluster **z** and keep its definition fixed. A paired Tp and Tc
proposal should target that same z.

**Tp:** change wording, names/context, notation, representation, or numerical parameters while retaining
z's applicability conditions and essential reasoning. The answer may change. Other original approaches
need not all survive.

**Tc:** keep the problem recognizably similar but alter an essential condition so that z no longer
provides a complete valid solving route under its fixed definition. **Another original approach may
still solve the new problem.** No requirement to invalidate every source approach or invent an entirely
new one is imposed.

A different answer, more computation, or choosing another method on the unchanged problem does not
establish Tc. A routine substitution or rearrangement that lets z still solve the variant undermines
the changing label. These are proposal judgments now, not completed validation.

For example, with C1 = direct summation and C2 = red-green symmetry: changing both independent ball
distributions to the same new law is a Tp idea for C2; changing only one is a Tc idea for C2, with C1
as a possible alternative. Its final statement and justification still need review. This is an illustration of the transformation rule, not a validated family.

## Files and editing

Read [family_template_annotated.jsonc](../templates/family_template_annotated.jsonc) to see an instruction directly above every field.
Fill [family_template.json](../templates/family_template.json) for the submission; its keys match the annotated file.
The descriptions are comments/documentation, not extra data fields to copy into every record.

Use JSON `null` for an unknown single value and `[]` for an empty list. Do not put the literal word
`"null"` in quotes. Keep IDs and source text unchanged while revising your analysis. Use JSON escaping
for mathematical text, such as `"\\frac{1}{3}"`, and do not put comments or trailing commas in the final
`.json` file. Add one object for every listed approach. A cluster contains approach IDs, while a
transformation targets cluster IDs.

A1 and C1 are different kinds of identifiers. They are local to each family: matching labels in two
families do not prove that the same strategy is being used. The source problem ID is the source
record's `index`, not a JSONL line number or a separately recovered upstream MATH ID.

Students fill **NOW** and **IDEAS NOW** sections. Keep `variant` null during collection and leave the
**EXPERT ONLY** section pending. A status of `validated` requires actual mathematical review and is
not produced by a schema validator.

## Field descriptions

Square brackets in the paths below indicate a list item, not literal key names.


### Identity and source

**`family_id` — NOW**

Your unique ID for this candidate, for example "train_0057". Keep it stable while reviewing the same original problem; transformed versions belong inside this family, not in new source-family records.

**`source` — NOW**

Where the original problem can be retrieved. Store only its file location and exact identifier.

**`source.file` — NOW**

The source repository/file path or direct file URL. The prefilled path points to the released multi-approach dataset; replace it only when using another source.

**`source.problem_id` — NOW**

The exact ID in the specified source file. For train.jsonl, use the record's "index" value, for example 57, not the row number. This is not an independently recovered upstream MATH ID.

**`collected_by` — NOW**

The student who selected and assembled the candidate. Enter your name.

**`domain` — NOW**

The problem's main mathematical subject, using your assigned domain name, for example "probability", "combinatorics", "geometry", or "algebra". Classify the problem, not the technique of one solution. These are team-assigned labels, not native labels in this file.

**`analysis_by` — NOW**

Who produced the working mathematical analysis. Name the student and any model assistance actually used, for example "Student name; ChatGPT-assisted". This does not record expert approval.


### The original problem

**`problem` — NOW**

The unchanged source problem, its source answer, and any interpretation issues.

**`problem.statement` — NOW**

Copy the full original problem statement faithfully, including assumptions and mathematical notation. Do not replace it with a proposed transformed problem or silently repair it.

**`problem.reference_answer` — NOW**

Copy the source answer as a string. If a check disagrees with it, keep the source answer and explain the discrepancy in interpretation_notes and solution_check; do not silently overwrite it.

**`problem.interpretation_notes` — NOW IF NEEDED**

A list of ambiguities, implicit conventions, or source-answer issues that affect the mathematics, one string per issue. Explain any interpretation you use. Leave [] if there are no such notes; do not invent assumptions merely to make a solution work.


### Every source-listed approach

**`approaches` — NOW**

Include every source-listed approach in its original order, even if it is flawed or redundant. Duplicate this object for A2, A3, A4, and so on. A selected pair later does not permit dropping the others.

**`approaches[].approach_id` — NOW**

A local identifier such as "A1", "A2", or "A3", following the original source order. These IDs identify source plans within this family, not shared strategies across different problems.

**`approaches[].name` — NOW**

Copy the source approach's name. A different name alone does not establish a different mathematical approach.

**`approaches[].core_idea` — NOW**

Copy the source's core-idea description. Evaluate it in your checks rather than rewriting it to match a preferred cluster.

**`approaches[].plan` — NOW**

Copy the ordered source steps as a list of strings. Preserve errors or omissions in the source text; document corrections or completions in solution_check and validity_check.reason.

**`approaches[].solution_check` — NOW**

Write the mathematical evidence: a worked derivation, a precise error/counterexample, or the specific missing step. An answer or a claim of validity is not enough. Clearly label any completion or correction you add to the source plan.

**`approaches[].validity_check` — NOW**

Assess this plan's mathematical validity, separately from whether it differs from another approach.

**`approaches[].validity_check.status` — NOW**

Use "valid" for a supported derivation; "invalid" for an identified error in the stated reasoning; "incomplete" when essential steps are missing; or "uncertain" when validity is unresolved. Leave null only before checking.

**`approaches[].validity_check.reason` — NOW**

Explain the status, pointing to the decisive calculation, error, or missing justification. Distinguish a valid completion from a repair that changes faulty source reasoning. A valid plan can still belong to the same cluster as another.


### Grouping and comparison

**`clustering` — NOW**

Your proposed grouping by central mathematical reasoning. Assess the plans rather than adopting the source's uniqueness count. Every source approach must appear in exactly one group or in unassigned.

**`clustering.groups` — NOW**

One object per supported mechanism cluster. Put valid approaches together when they have the same central route despite execution or presentation changes. Keep genuinely different routes separate. Do not count invalid or incomplete plans as extra valid clusters.

**`clustering.groups[].cluster_id` — NOW**

A local ID such as "C1" or "C2". C1 in another problem is not automatically the same strategy. Keep IDs stable when later transformation proposals reference them.

**`clustering.groups[].approach_ids` — NOW**

The IDs of approaches in this group, for example ["A1", "A3"]. Use only IDs present in approaches; do not place an approach in more than one group.

**`clustering.groups[].mechanism` — NOW**

Define the shared solving route: its central mathematical justification, essential steps, and the conditions it relies on. Be more specific than 'use algebra'. This fixed definition is what Tp will preserve or Tc will challenge.

**`clustering.groups[].reason` — NOW**

Explain the grouping. For merged plans, identify why their differences do not change the central reasoning. For a separate route, identify its distinctive mechanism. A singleton group alone does not prove distinctness; justify the separation in comparisons.

**`clustering.unassigned` — NOW IF NEEDED**

List every plan that cannot yet be placed in a supported group, with an approach_id and reason. This includes invalid/incomplete plans and valid plans whose distinctness remains unresolved. Use [] if all approaches are confidently grouped.

**`clustering.unassigned[].approach_id` — NOW IF NEEDED**

The existing approach ID that is not placed in a group, for example "A3".

**`clustering.unassigned[].reason` — NOW IF NEEDED**

Explain the precise obstacle: mathematical error, missing derivation, or unresolved relation to another mechanism. A valid but unassigned plan is not automatically a new cluster.

**`clustering.comparisons` — NOW**

Record pairwise evidence for the grouping. Provide enough comparisons to justify your merges, splits, selected distinct pair, and unresolved cases without repeating identical explanations.

**`clustering.comparisons[].approach_ids` — NOW**

Exactly two distinct existing approach IDs, for example ["A1", "A2"].

**`clustering.comparisons[].verdict` — NOW**

Use "same" for the same central route; "different" for a substantive change in mathematical reasoning; "uncertain" for an unresolved boundary between executable routes; or "insufficient_evidence" when flawed or underspecified reasoning prevents the comparison.

**`clustering.comparisons[].reason` — NOW**

Identify the decisive shared step or difference. Notation, wording, reordering, or an equivalent algebraic cleanup alone does not justify 'different'. Keep the verdict consistent with the groups.


### Why the candidate should be retained

**`selection` — NOW**

Your recommendation about retaining the whole original problem as a candidate, based on the validity and clustering evidence. This is not expert approval.

**`selection.recommendation` — NOW**

Use "shortlist" when at least two valid, genuinely distinct routes are supported; "hold" when more evidence or repair is needed; or "reject" when the current candidate should not be retained. Leave null before making a recommendation.

**`selection.distinct_approach_pair` — NOW**

Exactly two valid approach IDs from different supported groups that best demonstrate the selection criterion, for example ["A1", "A2"]. Keep all approaches in the record. Use [] when no defensible pair has been established; do not supply just one ID.

**`selection.reason` — NOW**

Explain why the evidence supports your recommendation. Identify the strongest pair and central distinction, or the blocker for a held/rejected candidate. An unresolved Tc idea alone does not invalidate a source problem's two-approach qualification.


### Transformation ideas: fill now, develop later

**`transformations` — IDEAS NOW**

Proposals relative to selected source clusters, not all original approaches. For a paired Tp/Tc proposal, use the same fixed target mechanism. Keep each cluster definition fixed while designing edits. Complete statements, solutions, generation methods, and expert validation come later.

**`transformations.Tp` — IDEAS NOW**

Mechanism-preserving ideas. Wording, names/context, notation, representation, and numerical parameters may change; the answer may change too. The selected mechanism's conditions and essential steps must still work. Other original approaches need not all be preserved.

**`transformations.Tp[].status` — IDEAS NOW**

Use "not_started", "idea", or "blocked" during collection. "idea" means proposed, not established. "blocked" means an identified obstacle, explained below. Later, "draft" means a developed but unvalidated variant; "validated" requires explicit mathematical review, not a JSON-format check.

**`transformations.Tp[].target_cluster_ids` — IDEAS NOW**

The source cluster you intend to preserve, normally a single ID such as ["C2"]. Reference clustering.groups, not an approach ID. If you intentionally target several clusters, justify preservation for each. For the comparison pair, Tc should target the same selected cluster.

**`transformations.Tp[].idea` — IDEAS NOW**

Describe the exact proposed surface or parameter edit. State what changes and what stays fixed. A complete transformed statement is not required yet. Leave null only when no concrete idea is available, and explain the obstacle in open_questions.

**`transformations.Tp[].reason` — IDEAS NOW**

Explain why the targeted mechanism should remain applicable: identify its conditions and map the essential steps to the proposed edit. A numerical change is not automatically preserving. Write an expectation rather than claiming a proof you have not supplied.

**`transformations.Tp[].expected_cluster_id` — IDEAS NOW**

The selected source cluster expected to solve the variant, normally the same ID as the single target, for example "C2". Use null if not yet established. If several targets are listed, name a primary one here and discuss the others in reason.

**`transformations.Tp[].open_questions` — IDEAS NOW**

List remaining checks or blockers, such as parameter validity, unchanged assumptions, or a required derivation. Use [] only if no questions are currently identified; an empty list is not validation.

**`transformations.Tp[].variant` — LATER**

Leave null for the collection stage. Later this holds the developed statement, checked reference answer, worked solutions, and construction method. Do not fill it with an invented completed variant.

**`transformations.Tc` — IDEAS NOW**

Mechanism-changing ideas. Keep the setup recognizably similar while changing an assumption, constraint, parameter, or goal that makes the selected mechanism no longer applicable as a complete solving route. Another original cluster may still solve the variant; no entirely new approach is required.

**`transformations.Tc[].status` — IDEAS NOW**

Use "not_started", "idea", or "blocked" during collection. A plausible edit is only an "idea". Use "blocked" if the target still works or no convincing change is available, and state why. Reserve "draft" and "validated" for development and explicit mathematical validation later.

**`transformations.Tc[].target_cluster_ids` — IDEAS NOW**

The selected source cluster intended to fail, normally a single ID such as ["C2"]. It need not include every source cluster. If several clusters are intentionally targeted, justify failure for each. Pair with Tp targeting the same fixed mechanism.

**`transformations.Tc[].idea` — IDEAS NOW**

Describe the proposed small edit and what makes the problem still look similar. Do not simply request 'use another method' on the unchanged problem. A new answer or a longer calculation alone does not establish a mechanism change.

**`transformations.Tc[].reason` — IDEAS NOW**

Identify the exact assumption or essential step that should fail, and explain why ordinary substitutions or routine execution adjustments do not rescue the fixed target route. Suggest how a different route could solve the variant. Another route working is not, by itself, evidence that the target fails.

**`transformations.Tc[].expected_cluster_id` — IDEAS NOW**

An existing source cluster expected to solve the changed problem, for example "C1" when the target is C2. It may be another original cluster. Use null if the alternative is unknown or not yet an existing cluster; describe a proposed new route in idea/reason rather than inventing an undefined ID. For a blocked proposal, recording the same cluster as the target can document why the edit failed.

**`transformations.Tc[].open_questions` — IDEAS NOW**

List unsettled mathematical checks: whether the target can adapt, whether the edit stays sufficiently similar, whether the alternative works, and any ambiguity in strategy granularity. The rule allowing another original cluster to remain valid is already agreed and is not an open question.

**`transformations.Tc[].variant` — LATER**

Leave null for the collection stage. Later store the exact changed statement, checked answer, alternative worked solution(s), and construction method. Its correctness and target failure still need mathematical review.


### Expert review

**`expert_review` — EXPERT ONLY**

Mayssa's separate mathematical review of the candidate. Students leave the defaults unchanged. A shortlist recommendation or collected_by='Mayssa' is not an expert approval.

**`expert_review.reviewer` — EXPERT ONLY**

Name of the person who actually performed the expert review. Leave null until that review occurs.

**`expert_review.decision` — EXPERT ONLY**

Keep "pending" until expert review. The reviewer may later use "accept", "revise", or "reject" for the record at its current stage. Accepting a source candidate does not automatically validate its transformation proposals.

**`expert_review.comments` — EXPERT ONLY**

Leave null for the student submission. The expert records approval scope, corrections, and unresolved issues, referring to approach or cluster IDs where helpful.


### Array-entry examples

`clustering.unassigned` entries have this shape:

```json
{
  "approach_id": "A3",
  "reason": "Valid completion, but its distinctness from A1 remains unresolved."
}
```

`clustering.comparisons` entries have this shape:

```json
{
  "approach_ids": [
    "A1",
    "A2"
  ],
  "verdict": "different",
  "reason": "Direct summation versus a symmetry-and-residual argument."
}
```

These are illustrations of structure, not entries that belong in every family.
An incorrect or incomplete plan should not be counted as an additional valid cluster.
Provide sufficient comparison evidence to support each claimed separation or merge; the selected
pair must be valid and belong to different supported groups. A held example is not evidence that
the five-good-candidates requirement has been satisfied.

### Later-only variant structure

For this collection assignment, the actual value remains `null`. The already-defined later shape is:

```json
{
  "statement": "Full transformed statement, to be written later.",
  "reference_answer": "Checked answer to the variant.",
  "worked_solutions": [
    {
      "approach": "Name or existing cluster ID of the solving route.",
      "steps": [
        "First justified step.",
        "Further steps and conclusion."
      ]
    }
  ],
  "method": "The actual edit rule, prompt, or script used."
}
```

**`transformations.Tp[] / Tc[].variant.statement` — LATER**

The exact full transformed problem statement, including domains and assumptions. It must be understandable without reading the proposed edit.

**`transformations.Tp[] / Tc[].variant.reference_answer` — LATER**

The checked answer to this transformed problem, stored as a string; it need not equal the source answer.

**`transformations.Tp[] / Tc[].variant.worked_solutions` — LATER**

A list of checked solution objects for the variant. For Tp, include a solution using the target mechanism; for Tc, include a valid alternative and explain target failure in the proposal's reason.

**`transformations.Tp[] / Tc[].variant.worked_solutions[].approach` — LATER**

A clear name or existing cluster ID for the route actually used. Describe a new route explicitly rather than implying that it is a verified source cluster.

**`transformations.Tp[] / Tc[].variant.worked_solutions[].steps` — LATER**

The ordered steps of a complete derivation, one string per step. Include essential justifications and assumptions rather than only the final answer.

**`transformations.Tp[] / Tc[].variant.method` — LATER**

How the transformation was constructed: the actual edit rule, manual steps, prompt, or script used. State what was done, not a planned method.

## Review before submitting

Check that every source approach is retained and appears exactly once in either a group or
`unassigned`; that all referenced approach and cluster IDs exist; and that a shortlisted record names
two valid approaches from different groups. Keep any model contribution explicit in `analysis_by`.
Leave Mayssa's decision pending and explain unresolved transformation ideas rather than inventing
completed statements or checks.
