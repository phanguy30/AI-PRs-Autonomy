# Agentic Pull Requests: Automation and Human Interaction 

This repository contains our analysis on the AIDev / Agentic Pull Requests
dataset. The overall goal is to understand **when AI coding agents can handle pull
requests (PRs) fully automatically** and **when human participation is still needed**.

In the full project we plan to answer three research questions (RQs):

- **RQ1 – Automation extent:**  
  To what extent are PRs fully automated (all commits by bots and no human review)
  versus requiring human participation?

- **RQ2 – Work type and complexity:**  
  What types of work and what levels of PR size/complexity correspond to fully
  automated PRs compared to those that involve humans?

- **RQ3 – Bot-level differences:**  
  Which bots generate PRs that require the most human feedback or corrections?

---

## Repository structure

The main folders and files are:

```text
.
├── data/                 # Input data (AIDev subset or preprocessed CSVs)
│   ├── pr_rq1.csv
│   ├── pr_rq2.csv        
│   └── pr_rq3.csv
├── scripts/              # Reproducible analysis code
│   ├── RQ1.ipynb   
│   ├── RQ2.ipynb      # aggregate work types and size metrics
│   └── RQ3.ipynb           
├── plots/                 # Output figures used in the report
│   
├── report/               # LaTeX source and compiled PDF for the report
│   ├──Milestone 1_group22.pdf
├── ├──Milestone 2_group22.pdf
│   └──Milestone 3_group22.pdf
├── .gitignore
└── README.md             # This file
```

## Environment setup

We run our analysis in Python 3, JupyterLab, and the main packages we use
(pandas, numpy, matplotlib, ...).

If you want to run the notebooks locally, you can create a simple environment
with pip:
```bash
pip install pandas numpy matplotlib seaborn
```
Then start JupyterLab:
```bash
jupyter lab
```
Open the notebooks in the scripts/ folder and run the cells in order.


## How to run the analysis

We provide two ways to run the project: a lightweight mode that only uses the
aggregated CSV files in this repository, and a full mode that rebuilds these
aggregates from the original AIDev tables.

### Option 1 – Reproduce our results using the aggregated CSVs (recommended)

This option does **not** require downloading the full AIDev dataset. You only
need the two pre-computed CSV files already stored in `data/`:

- `data/[pr_rq1].csv`  
  PR-level interaction labels (RQ1). One row per PR, including:
  - `pr_id`
  - the human–interaction level (e.g., 0 = fully automated, 1 = human review only, 2 = human commits)
  - basic PR metadata used in our RQ1 summaries

- `data/[pr_rq2].csv`  
  PR-level summary for RQ2. One row per PR, including:
  - `pr_id`
  - `level` (same interaction levels as RQ1)
  - `task_type` (feat/fix/docs/refactor/test/other)
  - `n_commits`
  - `n_files`
  - `lines_changed`

- `data/[pr_rq3].csv`  
  RQ3 summary by interaction level. One row per interaction level (0, 1, 2), including:
  - `level`
  - `n_pr`
  - `accept_rate`
  - `median_turnaround_hours`
  - `p25_turnaround_hours`
  - `p75_turnaround_hours`


Steps:

1. **Clone this repository**

    git clone https://github.com/phanguy30/AI-PRs-Autonomy.git
    cd AI-PRs-Autonomy

2. **Data used in this project**

   The raw AIDev tables are too large to include in this repo. For our analyses
   we use two aggregated PR-level CSV files stored in `data/`:

   - `data/pr_rq1.csv` – PR-level interaction labels for **RQ1**  
     (one row per PR, including `pr_id` and the interaction level:
     0 = fully automated, 1 = human review only, 2 = human commits).

   - `data/pr_rq2.csv` – PR-level summary for **RQ2**  
     (one row per PR, including `pr_id`, `level`, `task_type`,
     `n_commits`, `n_files`, and `lines_changed`).

   - `data/pr_rq3.csv` – RQ3 summary by interaction level  
     (one row per interaction level, including `level`, `n_pr`, `accept_rate`,
     `median_turnaround_hours`, `p25_turnaround_hours`, and `p75_turnaround_hours`).

### Option 2 – Rebuild all aggregates from the raw AIDev dataset

Use this mode if you want to inspect or regenerate every intermediate table used
in our analysis.

#### 1. Download the raw AIDev tables

Download the dataset from Hugging Face:

https://huggingface.co/datasets/hao-li/AIDev

Required files:

- `pull_request.parquet`
- `pr_comments.parquet`
- `pr_reviews.parquet`
- `pr_commits.parquet`
- `pr_commit_details.parquet`
- `pr_task_type.parquet`

Place all these files into the `data/` directory.

#### 2. Run the preparation notebooks

Execute the notebooks in `notebooks/preparation/` (or the equivalent Python scripts):

- `01_build_pr_level_table.ipynb`  
  Constructs the PR-level interaction table used in **RQ1**.

- `02_build_rq2_features.ipynb`  
  Computes task type, commit stats, file counts, and line-change metrics for **RQ2**.

- `03_build_rq3_metrics.ipynb`  
  Aggregates acceptance rate and turnaround statistics for **RQ3**.

These notebooks will output:

- `data/pr_rq1.csv`
- `data/pr_rq2.csv`
- `data/pr_rq3.csv`

#### 3. Proceed with the analysis notebooks

Once the aggregates are rebuilt, follow the same steps as in **Option 1** to run:
- `scripts/RQ1.ipynb`
- `scripts/RQ2.ipynb`
- `scripts/RQ3.ipynb`







