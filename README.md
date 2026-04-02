# LLM Evaluation Pipeline for E-commerce Product Descriptions

This project implements an end-to-end evaluation pipeline for LLM-generated product descriptions, including rubric design, baseline generation, manual evaluation, iterative improvement, and automated judging using an LLM.

---

## Business Use Case

The dataset contains e-commerce products with structured information:

- Product name
- Structured attributes
- Material
- Warranty

The goal is to generate a **persuasive 50–90 word product description** that is accurate, grounded, and aligned with a sales tone.

---

## Project Goals

- Define a consistent evaluation framework for LLM outputs
- Compare **human evaluation** vs **LLM-as-a-judge**
- Identify strengths and weaknesses of automated evaluation
- Improve generation quality through iteration

---

## Evaluation Criteria

Each generated description is evaluated using the following criteria:

- **Fluency** — natural, easy-to-read writing  
- **Grammar** — correct spelling and punctuation  
- **Tone** — friendly, credible sales voice  
- **Length** — 50–90 words  
- **Grounding** — no hallucinations or unsupported claims  
- **Latency** — response time  
- **Cost** — inference cost  

Each criterion is rated as:

- `good`
- `ok`
- `bad`

The final score is computed using:

- A cumulative pass threshold  
- A strict **grounding-based rejection rule**

---

## Project Structure

    llm-evaluation-pipeline/
    ├── data/
    │   └── products.csv
    ├── notebooks/
    │   ├── 01_task1_rubric.ipynb
    │   ├── 02_task2_generation.ipynb
    │   ├── 03_task3_human_eval.ipynb
    │   ├── 04_task4_improvement.ipynb
    │   ├── 05_task5_judge.ipynb
    │   └── 06_task6_analysis.ipynb
    ├── outputs/
    │   ├── assignment_01.xlsx
    │   ├── assignment_01_sample.xlsx
    │   ├── assignment_01_with_judge.xlsx
    │   └── assignment_01_single_criterion_judge.xlsx
    ├── requirements.txt
    └── README.md

---

## Tasks Overview

### Task 1 — Rubric Design

- Defined explicit criteria for `good / ok / bad`
- Established pass/fail rules
- Added grounding as a strict rejection condition

### Task 2 — Baseline Generation

- Generated descriptions using an LLM
- Collected:
  - generated text
  - latency
  - token usage
- Saved results to:
  - `outputs/assignment_01.xlsx`

### Task 3 — Manual Evaluation

- Evaluated a subset of products manually
- Added:
  - criterion ratings
  - cost calculation
  - final score
- Saved results to:
  - `outputs/assignment_01_sample.xlsx`

### Task 4 — Improvement Cycle

- Tested improvements such as:
  - prompt engineering
  - temperature tuning
  - model changes
- Compared quality, latency, and cost across experiments

### Task 5 — Judge Model

- Built an automated evaluator using an LLM
- Implemented:
  - a dedicated judge prompt
  - structured JSON output
  - a Pydantic schema
- Returned:
  - explanation
  - verdict
  for each criterion

### Task 6 — Judge Analysis

- Ran the judge on the dataset
- Performed:
  - sanity check
  - full run
  - agreement comparison with human evaluation
  - criterion-by-criterion judging
  - final analysis of trade-offs

---

## Main Findings

### Objective criteria are easier for LLM judges

Strong agreement on:
- Fluency
- Grammar

### Tone is harder

Lower agreement due to subjectivity in marketing language.

### Grounding is the hardest and most critical

Largest disagreement between human and judge model.  
LLM judge tends to be more lenient in borderline cases.

### Bigger models are not always better

Higher cost and latency did not significantly improve quality over smaller models with better prompting.

---

## Production Recommendation

Use a hybrid approach:

- LLM-as-a-judge for scale
- Rule-based validation for grounding
- Human sampling for quality control

---

## Setup

### Create virtual environment

    python3 -m venv .venv
    source .venv/bin/activate

### Install dependencies

    pip install -r requirements.txt

### Environment variables

Create `.env` file:

    NEBIUS_API_KEY=your_api_key_here

---

## Running the Project

Run notebooks in order:

1. 01_task1_rubric.ipynb  
2. 02_task2_generation.ipynb  
3. 03_task3_human_eval.ipynb  
4. 04_task4_improvement.ipynb  
5. 05_task5_judge.ipynb  
6. 06_task6_analysis.ipynb  

---

## Notes

- `.env` is excluded from version control  
- `.venv` is excluded from version control  
- `outputs/` is included because it is part of the assignment deliverables  

---

## Author

Moshe Oz