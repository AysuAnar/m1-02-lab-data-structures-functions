![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Data Structures and Function Design for Analytics

## Overview

In this lab you will build a small analytics pipeline using core Python data structures and functions. The goal is to practice selecting the right structure for each task, writing reusable functions, and validating results as you go. The scenario is a simplified customer support log where each entry includes a customer ID, issue category, resolution time, and whether the issue was escalated. You will use lists, dictionaries, sets, and tuples to model the data, then write functions that transform the data into clean, analysis-ready summaries.

## Learning Goals

By the end of the lab, you should be able to model tabular data with core Python structures, write clear functions that operate on those structures, and produce validated summary outputs. You should also be able to reason about data types, handle missing values, and design function interfaces that are easy to reuse.

## Setup and Context

You will generate a synthetic dataset directly in code so you can control the structure and intentionally introduce imperfections. Each log entry will be a dictionary with keys like `ticket_id`, `customer_id`, `category`, `resolution_minutes`, and `escalated`. You will collect entries in a list, which will serve as your raw dataset. This resembles the kind of semi-structured data you might receive from a basic system export or API.

Work in a notebook named `m1-02-data-structures-functions-lab.ipynb`. Use a fixed random seed so the data is reproducible. You can use the `random` module for category selection and resolution times, or NumPy if you prefer. The important part is that you can regenerate the same dataset consistently.

## Requirements

- Fork this repository to your own GitHub account.
- Clone your fork to your machine.
- Make sure you can open and run Jupyter notebooks (for example via Jupyter Lab or VS Code).

## Getting Started

- Create a new notebook and name it  `m1-02-data-structures-functions-lab.ipynb`.
- Use a fixed random seed so your dataset can be regenerated consistently.
- As you work, add short markdown notes where the lab asks you to explain or justify decisions.
- Before you submit, restart your kernel and run the notebook **top to bottom**.

## Tasks

### Task 1: Build a raw log dataset

Write code that generates a list of dictionaries representing support tickets. Each dictionary should include the fields described in the setup. Include at least 200 entries so that summaries are meaningful. Introduce realistic variation, such as a few categories that appear more frequently and occasional missing or malformed `resolution_minutes` values to simulate dirty data.

You are expected to write the generator logic yourself. Keep it readable and explain the logic in short markdown notes where necessary. After generating the list, print the first five entries and the total count to validate the structure.

### Task 2: Design validation helpers

Create small functions that validate the dataset. For example, write one function that checks whether all required keys are present in each record, and another function that identifies records with missing or invalid `resolution_minutes`. These functions should return clear results such as a list of bad records or counts of issues.

Keep function signatures simple and explicit. For instance, a validation function should take the list of records as input and return a list of indices or a filtered list. Avoid printing inside these functions; return values instead so you can reuse them in other contexts.

### Task 3: Clean and normalize records

Write a function that takes the raw records and returns a cleaned version. At minimum, it should handle missing `resolution_minutes` values in a defined way and normalize `category` strings (such as trimming whitespace and standardizing case). If you introduced malformed values, decide whether to drop those records or repair them, and document the decision in a short markdown cell.

Use list comprehensions or loops to build the cleaned list. Avoid mutating the original list in place. At the end, show the number of records before and after cleaning, and display a few cleaned records.

### Task 4: Build summary functions

Create functions that compute useful summaries from the cleaned data. At a minimum, include:

1. Average resolution time per category
2. Count of tickets per customer
3. Escalation rate overall and by category

Use dictionaries to store summary results, with clear keys and values. For example, the average resolution time per category should be a dictionary mapping category name to average minutes. Your functions should return these dictionaries rather than printing them directly.

After computing each summary, write a small validation check. For example, confirm that the sum of category counts matches the total number of cleaned records. These checks are essential for catching logic errors early.

### Task 5: Package a final report

Write a function that combines the outputs of your summaries into a single report structure. This might be a dictionary that contains other dictionaries. The goal is to provide a single object that could be serialized or used by another part of a pipeline.

In a final notebook cell, print a compact report and add a short text explanation of one insight you observed. Keep the report readable and avoid overly verbose output.

## Common Pitfalls and Debugging Notes

A common mistake is mixing types in the `resolution_minutes` field and forgetting to convert them before aggregation. If you see a `TypeError` during summation or averaging, inspect the types of values in that field and enforce numeric conversion during cleaning.

Another pitfall is mutating the original dataset during cleaning. If you later need to compare raw and cleaned data, mutation makes this difficult. Use new lists and new dictionaries for cleaned records to keep your workflow transparent.

It is also easy to lose track of missing values when you compute averages. If you drop records, make sure your counts and denominators match the cleaned dataset rather than the raw dataset. A simple count check after each step will prevent this class of error.

## Submission

### What to submit

Submit the following files:
- The notebook file `m1-02-data-structures-functions-lab.ipynb`
- A Python file `m1-02-summary-functions.py` containing your validation and summary functions
- A short text output cell at the end of the notebook showing your final report

### Definition of done (checklist)

Before you submit, make sure:

- [ ] The notebook runs **top to bottom** without errors after a kernel restart.
- [ ] Your dataset generator is reproducible (fixed seed) and produces at least 200 records.
- [ ] Your validation/cleaning steps are explicit, and you included the requested sanity checks (counts match, denominators match cleaned data).
- [ ] `m1-02-summary-functions.py` contains your validation and summary functions, and they return values (they don’t rely on `print()`).
- [ ] Your final report is shown in the last notebook cell with one short insight.
- [ ] All required files are saved and included in your git commit.

### How to submit (Git workflow)

- When you’re done, make sure all changes are saved, then run:

```bash
git add .
git commit -m "Solved m1-02 lab"
git push -u origin HEAD
```

- Make a pull request.
- Paste the link to your pull request in the Student Portal.

## Evaluation Criteria

Your work will be evaluated for correctness, clarity, and structure. Correctness means your summaries and validation checks are logically consistent and based on cleaned data. Clarity means your functions are well named, your data structures are chosen appropriately, and your code is readable without excessive comments. Structure means the notebook runs top to bottom, each task is completed in order, and your final report is clearly presented. The expectation is a professional workflow that could be reused by another analyst.