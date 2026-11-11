# Reasoning Agent --- Submission Guide

**Student:** Pawan Kumar Koli\
**Roll No.:** M24MA2007

## Files required

Place the following files in the `submission/` directory:

``` text
submission/
├── reasoning_agent.ipynb
├── report.pdf
├── submission.csv
└── README.md
```

The assignment statement names `README.txt`; if the submission portal
strictly requires that filename, save a copy of this README as
`README.txt` as well.

## Overview

The notebook implements a first-order logic reasoning agent. It parses
formulas, converts them into clauses, and attempts to determine whether
a conclusion follows from a knowledge base using resolution refutation.

## Main components

-   **Formula parsing:** supports logical symbols and operators
    including negation, conjunction, disjunction, implication,
    biconditional, exclusive-or, quantifiers, and equality syntax.
-   **Clause conversion:** transforms formulas toward clause normal form
    using negation-normal-form conversion, Skolemization, and CNF
    distribution.
-   **Unification:** matches terms and predicates while respecting
    variable substitutions and an occurs check.
-   **Resolution refutation:** adds the negation of the query to the
    premises and searches for a contradiction. A proof of contradiction
    that uses the negated goal is treated as entailment.
-   **Search controls:** resolution uses bounds on time, generated
    clauses, clause length, depth, and retained clauses.
-   **Data handling:** reads supported CSV, TSV, JSON, JSONL, or Parquet
    test files when one is found. Otherwise, the notebook attempts to
    load public datasets through Hugging Face and falls back to built-in
    demonstration examples if no data can be loaded.
-   **Output:** writes `submission.csv` with an `id` column and
    prediction columns named `flag` and `label`. Both prediction columns
    contain the same answer; the default output style is `True`/`False`.

## How to run

1.  Open `reasoning_agent.ipynb` in Jupyter or Google Colab.
2.  Install any missing dependencies used by the notebook, including
    `pandas` and, for public dataset loading, `datasets` and
    `huggingface_hub`.
3.  Put the supplied test file in a location searched by the notebook,
    or set `TEST_FILE` to its path near the top of the notebook.
4.  Run the notebook cells in order.
5.  Check the printed mode and item count to confirm that the intended
    dataset was loaded.
6.  Review the printed inference time and, when ground-truth labels are
    available, the final accuracy and confusion-matrix counts.
7.  Confirm that `submission.csv` was created and that its row count
    matches the number of test examples.

## Evaluation notes

Accuracy is printed only when every loaded row has a usable label. A
test set without labels is used for prediction and CSV generation, but
its accuracy cannot be computed by the notebook. If no test file is
found, the notebook may use public datasets or demonstration rows; do
not treat demonstration results as test-set performance.

The report should quote the actual metrics printed by the notebook for
the intended public dataset. Do not insert estimated or invented
accuracy or inference-time values.

## Important implementation limitations

-   Resolution is a bounded search procedure in this implementation.
    Failure to find a proof within the search limits is not a formal
    proof that the conclusion is not entailed.
-   The default prediction is `False` unless a proof is found (subject
    to the notebook's inconsistent-knowledge-base setting).
-   The optional English-input converters use heuristic parsing and may
    not correctly interpret every natural-language sentence.
-   Dataset availability, versions, and access permissions may affect
    which experiments run. The notebook prints load errors and
    identifies the selected data mode.

## Security note

Do not commit access tokens or passwords to a notebook. If a real
Hugging Face token has been placed directly in the notebook, revoke it
and use a private environment variable or Colab Secret instead. Remove
the token from the notebook before submission.

## Reproducibility checklist

-   [ ] `reasoning_agent.ipynb` runs from top to bottom.
-   [ ] The intended public dataset or test file is confirmed in the
    notebook output.
-   [ ] Final accuracy is recorded only when gold labels are available.
-   [ ] Total inference time and average time per item are recorded.
-   [ ] `submission.csv` contains the expected IDs and predictions.
-   [ ] The report includes the actual experiment results and reasoning
    traces.
-   [ ] No credentials or access tokens remain in the submitted files.
