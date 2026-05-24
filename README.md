# SEO Stax Skill Lab

Public artifact for the Project Pezzos lab:

> Does Stax improve an already established Codex workflow?

The lab compared four Codex variants on the same repository and the same exported SEO
data pack:

- `clear`: no Stax, no SEO skill
- `skill`: no Stax, with a repo-local SEO skill
- `st+clear`: with Stax, no SEO skill
- `st+skill`: with Stax and the SEO skill

The task was deliberately bounded: read exported GA/GSC files, produce a quick-wins SEO
report, then make a small homepage change. Live GA/GSC access was not used during the
four benchmark runs.

## Result Summary

Two blind Codex scorings ranked the anonymized reports in the same order:

| Rank | Report | Revealed Variant | Score 1 | Score 2 | Mean |
| ---: | --- | --- | ---: | ---: | ---: |
| 1 | C | `st+clear` | 92 | 93 | 92.5 |
| 2 | A | `clear` | 91 | 92 | 91.5 |
| 3 | D | `st+skill` | 88 | 84 | 86 |
| 4 | B | `skill` | 84 | 83 | 83.5 |

The result is a small positive signal for Stax on this task, not a general conclusion.
The SEO skill helped formalize the workflow, but did not win by itself.

## What Is Included

- `prompts/`: prompts used for reading, report generation, skill creation, skill
  execution, homepage modification, scoring, and final synthesis.
- `reports/`: anonymized reports `A/B/C/D` and `variants-map.json`.
- `scoring/`: Codex scorings, the final synthesis, and the Claude timeout note.
- `traces/`: run traces and Stax init summaries.
- `diffs/`: captured homepage diffs for each variant.
- `RESULTATS.md`: factual execution summary and limits.

## What Is Not Included

- Raw GA/GSC CSV exports.
- Raw Codex JSONL logs.
- Worktrees.
- Live credentials, tokens, or private account identifiers.

## Read First

1. `RESULTATS.md`
2. `scoring/scoring-final.md`
3. `reports/variants-map.json`
4. `reports/report-A.md` through `reports/report-D.md`
5. `prompts/scoring.md`

## Related Article

The Project Pezzos article is preview-visible as:

<https://preview.projectpezzoscom.pages.dev/journal/stax-agent-baseline-lab/>

The stable production URL should be added here after production publication is approved.
