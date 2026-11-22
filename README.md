# How Autonomous Are AI Coding Agents?

An analysis of **33,596 pull requests** written by AI coding agents (the AIDev "Agentic Pull Requests" dataset) to measure how often agents finish the job on their own, what kind of work they handle, and how human involvement relates to whether a PR gets accepted.

## Key findings

- **Most agent PRs still involve a human.** Only **9.5%** (3,205) were fully automated. **10.6%** (3,574) had humans review or comment only, and **79.8%** (26,817) included at least one human-authored code commit.
- **Fully automated PRs are small and fix-heavy.** Their median PR changes 64 lines across 2 files, and 35% are new features and 33% are bug fixes. PRs with human commits skew toward features (46%) and tests (8%, versus 3% when fully automated).
- **Human involvement tracks acceptance.** Among closed PRs, **29.6%** of fully automated PRs were merged, versus **57.5%** with human review only and **84.2%** with human commits. Median time to close was 1.4 hours, 9.7 hours and under 3 minutes respectively.

## How involvement is measured

Each PR gets one level, built by joining five tables (PRs, reviews, comments, commits, timeline) with pandas:

| Level | Meaning |
|-------|---------|
| 0 | Fully automated: no human review, comment or commit |
| 1 | Human review or comments only |
| 2 | At least one human-authored code commit |

Bots are identified from review and comment authors flagged as `Bot`. Administrative timeline events (merge, close, label, assign and similar) are excluded, so a PR written entirely by an agent but merged by a human still counts as automated.

## Data

| File | Contents |
|------|----------|
| `data/pr_with_human_interaction_levels.csv` | One row per PR: `pr_id` and involvement `level` |
| `data/pr_rq2.csv` | One row per PR: `level`, `task_type` (feat, fix, docs, test, refactor, chore, ...), `n_commits`, `n_files`, `lines_added`, `lines_deleted`, `lines_changed` |
| `data/pr_rq3.csv` | One row per level: PR count, acceptance rate, and median / 25th / 75th percentile turnaround hours |

The raw AIDev tables (`pull_request`, `pr_reviews`, `pr_comments`, `pr_commits`, `pr_timeline`) are not included. Download them from the AIDev dataset and place them in `data/dataset/`.

## Repository structure

```
data/       derived CSVs (raw AIDev tables are not tracked)
scripts/    RQ1.ipynb (involvement levels), RQ2.ipynb (work type and size), RQ3.ipynb (acceptance and turnaround)
reports/    written project reports
```

## Reproduce

1. Install `pandas`, `numpy`, `pyarrow` and `matplotlib`.
2. Download the AIDev tables and update the file paths at the top of each notebook.
3. Run `scripts/RQ1.ipynb`, then `RQ2.ipynb`, then `RQ3.ipynb`.
