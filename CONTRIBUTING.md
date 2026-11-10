# Contributing a candidate family

## 1. Claim the original problem

Search `families/` and open/closed Issues for the source file and problem ID. If already claimed, coordinate on that same record rather than creating a duplicate. Otherwise open a **Claim a family** issue, name the owner, and include the proposed domain. Claiming a problem does not certify it as a good candidate.

## 2. Prepare one JSON file

Create a working branch such as `families/your-name-train-0123`. Copy `templates/family_template.json` to `families/train_0123.json`, adjusting the ID for the actual source. Read the annotated template and field guide. Keep the existing JSON structure; do not add new metadata fields ad hoc.

Preserve every source approach and document any errors or completions in your checks. Identify at least two valid, genuinely different approaches for a shortlist recommendation. Record tentative Tp/Tc ideas for the same selected cluster; leave `variant` null during collection. A held candidate belongs in the repository as a clearly held record, not counted among five qualifying submissions.

Use your actual name for `collected_by`. Expert review stays pending until it is actually performed. No automatic check certifies the mathematics.

## 3. Check the submission

Confirm that the file is valid JSON with no comments or trailing commas, and the filename agrees with `family_id`. Check that source text is faithful, each source approach is grouped or explicitly unassigned, referenced approach/cluster IDs exist, and the two selected approaches are valid and supported as different. Keep unresolved cases visible.

The JSON Schema is in `schema/family.schema.json`. This repository does not yet configure automatic CI validation; the schema is available for a later validation workflow.

## 4. Request review

Open a pull request to `main`, link the claim issue, and use the supplied checklist. Prefer one family per pull request. Describe the strongest approach distinction and the remaining uncertainty. Request Mayssa's mathematical review; respond to comments by updating the same branch and file.

A merge can archive a pending candidate without approving its mathematics. Keep the issue open while substantive review work remains, and record the actual expert decision in the family JSON. Never infer expert approval from a merge, a shortlist recommendation, or the collector's name.

## Commits

Keep commits short, simple, and meaningful. Use one clear change per commit, with messages such as `Add train_0123 family`, `Fix probability calculation`, or `Clarify cluster definitions`. Avoid vague messages such as `Update files` or `Changes`.

## Team convention

Agree on a domain split before browsing; classify candidates as you go because the source file is not labeled by domain. Use source IDs to avoid overlap, including mixed-domain cases. Each contributor should collect five qualifying families. Do not create a separate folder per student or an independent copy of a family for each stage. Use the JSON for the current mathematical record, Issues for ownership/discussion, and pull requests for change review.
