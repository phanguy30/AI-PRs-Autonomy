# Agentic Pull Requests: Automation and Human Interaction 

This repository contains our course project for the AIDev / Agentic Pull Requests
dataset. The overall goal is to understand **when AI coding agents can handle pull
requests (PRs) fully automatically** and **when human participation is still needed**.

In the full project we plan to answer three research questions (RQs):

- **RQ1 – Automation extent:**  
  To what extent are PRs fully automated (all commits by bots and no human review)
  versus requiring human participation?

- **RQ2 – Work type and complexity (this milestone):**  
  What types of work and what levels of PR size/complexity correspond to fully
  automated PRs compared to those that involve humans?

- **RQ3 – Bot-level differences (future work):**  
  Which bots generate PRs that require the most human feedback or corrections?

This repository mainly supports **RQ2** for the current milestone report.

---

## Repository structure

The main folders and files are:

```text
.
├── data/                 # Input data (AIDev subset or preprocessed CSVs)
│   ├── README.md         # Brief note on where the data come from / how to obtain
│   └── ...
├── scripts/              # Reproducible analysis code
│   ├── 01_rq1.ipynb   
│   ├── 02_rq2.ipynb      # aggregate work types and size metrics
│   └── 03_rq3.ipynb           
├── figs/                 # Output figures used in the report
│   ├── rq2_task_type_hbar.png
│   ├── rq2_lines_changed_box.png
│   ├── rq2_n_files_box.png
│   └── rq2_n_commits_box.png
├── report/               # LaTeX source and compiled PDF for the milestone report
│   ├── main.tex
│   └── milestone2.pdf
├── env/                  # (optional) environment files
│   └── environment.yml   # or requirements.txt
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
