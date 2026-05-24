# RESULTATS

## Status

`complete-with-limits`

The four requested benchmark variants ran sequentially from the same base commit and
produced reports, diffs, traces, and blind scoring. The Claude scoring path did not
complete; the usable scoring evidence is two Codex scorings.

## Lab Question

Does Stax improve an already established Codex workflow?

Secondary question: does a repo-local SEO skill improve or stabilize the same workflow?

## Method

- Target repo: `pezzoslabscom`
- Base commit: `f5c62e3646c8ef17974fc84ad3d0bca0cb86a000`
- Data source: exported GA/GSC data pack already present in the target repo.
- Runs: four detached worktrees.
- Execution order: sequential.
- Live GA/GSC after data export: not used.
- Public artifact scope: reports, prompts, scoring, traces, and diffs. Raw logs and raw
  exported data are intentionally not published here.

## Test Matrix

| Variant | Stax | SEO Skill | Report | Homepage Diff | Trace | Status |
| --- | --- | --- | --- | --- | --- | --- |
| `clear` | no | no | done | done | done | done |
| `skill` | no | yes | done | done | done | done |
| `st+clear` | yes | no | done | done | done | done |
| `st+skill` | yes | yes | done | done | done | done |
| Codex blind scoring | n/a | n/a | done | n/a | done | done |
| Secondary Codex blind scoring | n/a | n/a | done | n/a | operator-provided | done |
| Claude blind scoring | n/a | n/a | not usable | n/a | done | stopped after timeout |

## Scores

| Rank | Report | Revealed Variant | Score 1 | Score 2 | Mean |
| ---: | --- | --- | ---: | ---: | ---: |
| 1 | C | `st+clear` | 92 | 93 | 92.5 |
| 2 | A | `clear` | 91 | 92 | 91.5 |
| 3 | D | `st+skill` | 88 | 84 | 86 |
| 4 | B | `skill` | 84 | 83 | 83.5 |

## Interpretation

- Stax improved both comparable pairs in the two Codex scorings:
  - `clear` -> `st+clear`
  - `skill` -> `st+skill`
- The measured gain was small.
- Stax did not reduce total workflow time in this run.
- The SEO skill made the workflow more explicit, but did not improve the score by
  itself.
- The strongest shared SEO recommendation was to optimize
  `/diagnostic-automatisation-process/`.

## Workflow Cost

| Variant | Total Duration | Input Tokens | Cached Input | Output Tokens |
| --- | ---: | ---: | ---: | ---: |
| `clear` | 397 s | 1,134,434 | 965,248 | 16,508 |
| `skill` | 512 s | 1,625,959 | 1,447,040 | 22,099 |
| `st+clear` | 461 s | 1,178,009 | 1,022,592 | 19,961 |
| `st+skill` | 594 s | 2,180,313 | 1,827,200 | 25,856 |

## Stax Init Notes

Stax was initialized before any data reading in `st+clear` and `st+skill`.

The local traces record:

- `st+clear`: 5 seconds
- `st+skill`: 4 seconds
- untracked local Stax files appeared in each Stax worktree
- no Stax-created commits were observed by the orchestration
- data sent to Stax was not independently observable from local stdout
- the orchestration did not pass GA/GSC data to the Stax commands

## Not Completed

- Claude scoring did not complete. It was interrupted after 527 seconds and produced no
  usable score.
- No repeated runs were performed, so variance is unknown.
- No scorer outside Codex produced a usable ranking.
- Raw GA/GSC CSVs are not published in this artifact.

## Commands And Artifacts

Representative commands:

- `git worktree add --detach <path> <base_sha>`
- `npx -y stax-agent@latest doctor`
- `npx -y stax-agent@latest install`
- `npx -y stax-agent@latest --runtime=codex`
- `codex -a never exec --ephemeral --ignore-rules --json ...`
- `npm run check`
- `make check`

See:

- `prompts/`
- `reports/`
- `scoring/`
- `traces/`
- `diffs/`

## Public Resource State

No tunnels, DNS records, Cloudflare resources, or Tailscale resources were created for
this lab artifact.

This repository is the only public resource expected for the evidence bundle.

## Public Repo Creation Review

`review_status`: approved

`reviewer`: operator-manual-review

`review_timestamp`: 2026-05-24T09:47:00+02:00

`review_reason`: public GitHub repository creation for the article evidence bundle.

`reviewed_plan_summary`: create or update public GitHub repository
`pezzos/seo-stax-skill-lab` from the sanitized local artifact directory. Publish only
README, RESULTATS, prompts, anonymized reports, scoring files, run traces, Stax init
summaries, and diffs. Exclude raw GA/GSC CSV exports, raw Codex JSONL logs, worktrees,
credentials, node_modules, `.env`, `.wrangler`, and nested `.git` directories.

`material_findings`: Claude CLI review was blocked because the organization has
disabled Claude subscription access for Claude Code. The operator approved the reviewed
plan manually in the Codex thread with: "J'approuve".

`handling`: proceeded with public GitHub repository creation after local file inventory
and secret-pattern search pass.

## Public GitHub Repo Creation

- Repository: https://github.com/pezzos/seo-stax-skill-lab
- Visibility: public
- Created from sanitized artifact directory:
  `/Users/alexandrepezzotta/repos/PezzosLabs/seo-stax-skill-lab`
- Initial push: completed on 2026-05-24
- Post-push author correction: completed with `git commit --amend --reset-author` and
  `git push --force-with-lease`
- Secret-pattern search: no live secret hit; only a false-positive mention of the
  search itself in this file.
- Excluded materials: raw GA/GSC CSV exports, raw Codex JSONL logs, worktrees,
  credentials, `node_modules`, `.env`, `.wrangler`, and nested `.git` directories.
