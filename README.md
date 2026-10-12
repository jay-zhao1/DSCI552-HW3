# DSCI 552 Homework 3

Name: Yang Zhao  
USC NetID: yzhao528

## Contents and submission checklist

For GitHub submission, push the contents of this directory to the repository root. Upload the files and folders below, rather than a ZIP archive:

- `DSCI552_Homework3_Yang_Zhao.ipynb`: executed Python notebook with saved tables and plot.
- `DSCI552_Homework3_Yang_Zhao.pdf`: 17-page report, including all 42 bootstrap intervals, all ISLR 3.7.4 answers, and all 88 x 42 extracted values in the appendix.
- `README.md`, `requirements.txt`, and `.gitignore`.
- `data/AReM/`: the 88 supplied original CSVs, retained for portable execution.
- `results/`: computed feature table, split manifest, data audit, 42-row bootstrap table, feature-type evidence and correlations, and the displayed plot.

Repository visibility, repository naming, and the portal link to submit must follow the latest instructor announcement. These rules are not stated in Homework3.pdf and have not been independently confirmed. If that announcement requires a public GitHub repository and its homepage URL on Brightspace, use those settings and submit that URL. The dataset is bundled so the notebook runs without a download. Do not upload ZIP archives, virtual environments, checkpoints, temporary files, old report copies, the textbook, or the assignment PDF. This submission directory contains none of those extra files.

## Run from a clean environment

Use Python 3.11 or later. From this directory:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyterlab DSCI552_Homework3_Yang_Zhao.ipynb
```

Select the environment's Python kernel and choose **Restart Kernel and Run All Cells**. All input/output paths are relative to this directory. The notebook recreates `results/`; no internet access is needed after installing packages. A fresh kernel execution has already been completed and saved with zero execution errors.

## Methods and data integrity

- Exact split: dataset1-2 in bending1/bending2 and dataset1-3 in all other activities are test data; 69 training and 19 test instances.
- All 88 files and all 42,239 observed numeric rows are checked. No observed rows are discarded. Original CSV bytes were verified against the supplied ZIP before copying.
- `bending2/dataset4.csv`: 480 whitespace-delimited rows.
- `cycling/dataset9.csv` and `cycling/dataset14.csv`: one extra trailing comma each.
- `sitting/dataset8.csv`: 479 observed rows; timestamp 13,500 ms is absent from the supplied ZIP. No imputation; its features use all observed values.
- Seven summaries per channel, six channels: 88 x 42 numeric features. Within-recording and across-recording standard deviations use ddof=1; quantiles use linear interpolation. Raw values are used.
- Nonparametric percentile bootstrap over all 88 instance rows: 10,000 resamples, NumPy default_rng seed 552, 5th/95th percentile endpoints. Whole-row resampling preserves cross-feature dependence. These are pointwise intervals under an independent-recording approximation, conditional on the observed activity mixture.
- Feature-type judgment uses only the 69 training instances: mean, standard deviation, maximum. Evidence is descriptive activity separation and redundancy; no classification models are trained.
- Displayed numbers use four decimal places. CSVs retain full precision.

## Final verification

- [x] A new isolated virtual environment (without system site-packages) installed only requirements.txt, passed pip check, and executed all seven cells with zero errors from a clean copy of the repository root. The copy initially contained no results directory; all seven result files were regenerated.
- [x] All requested subparts: 1(a), 1(b), 1(c)(i)-(iv), and 2(a)-(d).
- [x] 88 total instances; 69 train / 19 test; exact per-activity file membership asserted.
- [x] Exactly 42 feature columns and 42 complete bootstrap intervals. All 3,696 feature values were independently recomputed directly from original ZIP bytes. All 42 standard deviations and 84 interval endpoints were independently reproduced.
- [x] Every displayed PDF feature value, bootstrap-table entry, and feature-type evidence entry matches the generated CSV at four-decimal precision. CSV results from the isolated execution match the delivered results.
- [x] All 17 PDF pages rendered and visually inspected for clipping, missing figures, and table layout.
- [x] Homework 4 Part 4 and extra-practice ISLR 3.7.3/3.7.5 are excluded.

Validation environment: Python 3.13; direct package versions are recorded in requirements.txt. This submission has been prepared locally; it has not been uploaded to a course portal.

Reasoning update: each requested question includes justification; added split-count arithmetic, feature definitions, cleaning and normalization rationale, bootstrap rationale, and expanded ISLR derivations. The revised notebook was executed again in a fresh kernel with zero errors.

## Audit decisions

- Question 1(c)(iv) explicitly says to use judgment and gives min/mean/max as one option. The justified mean/std/max choice is retained. No supplied rule mandates the example; an unseen lecture rubric or Homework 4 grading convention cannot be confirmed from this assignment.
- The PDF does not need to print the full feature dataset under the supplied assignment wording. Its existing full appendix is retained because it is complete and not a rubric or execution defect. The notebook and full-precision CSV also retain every feature.
- ISLR conclusions match the supplied exact exercise: (a) cubic training RSS lower or equal; (b) linear expected test RSS lower under a true linear mean and the usual assumptions; (c) cubic training RSS lower or equal; (d) nonlinear truth alone does not determine test RSS. Reasoning and mathematical qualifications are retained.
- The original sitting/dataset8.csv SHA-256 is a551a654418ffe478e7b16b7499ef6aa155d8411ddf5c60d8c09c0667af19a02. Byte comparison against the provided ZIP confirmed 479 numeric rows and absence of timestamp 13500 ms. No imputation was performed.
