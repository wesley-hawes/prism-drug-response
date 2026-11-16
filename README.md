# PRISM Drug Response

Exploring why cancer cell lines respond differently to the same compound.

**Status:** data understanding and quality audit. Predictive modeling has not started; no model performance or biological discoveries are claimed.

## Research questions

1. How much do responses vary across cell lines and cancer types?
2. Which compounds show broad versus selective effects in this screen?
3. In a later phase, can baseline molecular features improve prediction for unseen cell lines beyond cancer-type baselines?

## Start here

Open [notebooks/EDA1.ipynb](notebooks/EDA1.ipynb) for the response-matrix audit, metadata joins, missingness and cell-identity checks, and comparisons of response distributions across treatments and cell lines.

The initial files contain 578 response rows and 4,686 treatment columns. Ten response rows lack a confirmed cell identity and fail STR profiling. All 568 remaining cell identities match the supplied DepMap sample metadata. There are 2,632,171 observed responses; these are repeated measurements across cell lines and treatments, not independent patients.

## Run locally

Use Python 3.11 or newer. From this repository's root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Download the inputs listed in [data/raw/README.md](data/raw/README.md), place them in `data/raw/`, and open the notebook in VS Code with the Python and Jupyter extensions. Select `.venv/bin/python` as the notebook kernel, then Run All.

The initial local setup uses an environment that inherits the existing Anaconda packages to avoid changing the global installation. `requirements.txt` records the package versions used for this first walkthrough; the fresh-install workflow above has not been tested on other platforms.

## Validation

All EDA code cells passed sequential execution in Python, including identifier uniqueness and the 568 × 4,686 verified response matrix. The notebook retains outputs saved in VS Code. A separate Jupyter-kernel rerun was blocked by local socket restrictions; re-run the notebook in VS Code with the inputs in `data/raw/`.

## Data relationships

```text
response row -> screen_cells.row_name -> screen_cells.depmap_id -> samples.DepMap_ID
response column -> treatments.column_name
```

A future SQL response table will use one row per cell-treatment pair, joined to cell and treatment dimension tables. Original files remain unchanged; derived datasets belong in `data/processed/`.

## Project layout

- `notebooks/`: explained analyses and visualizations
- `src/`: reusable Python functions as the project develops
- `docs/`: data dictionary, source notes, and input checksums
- `reports/figures/`: generated figures
- `data/`: local inputs and derived data, excluded from Git

## Analysis standards

- Exclude failed cell identities from analyses requiring confirmed biological annotations.
- Preserve missing responses; do not replace them with zero.
- Split by cell line when evaluating generalization to unseen cells.
- Fit preprocessing and feature selection on training data only.
- Compare against simple baselines before increasing model complexity.
- Distinguish predictive associations from causal mechanisms and laboratory responses from clinical efficacy.

## Roadmap

- [x] Document input files and verify table relationships
- [x] Audit missing responses and cell identity
- [x] Inspect one treatment's response distribution
- [ ] Explore coverage, response variation, and cancer-type patterns
- [ ] Choose a modeling question and freeze an evaluation design
- [ ] Add baseline expression data if justified by that question
- [ ] Compare baseline and regularized models with uncertainty estimates
- [ ] Publish a concise findings report and polished figures

## Sources

The PRISM inputs originate from the Broad Institute's [PRISM Repurposing dataset](https://depmap.org/repurposing/), described in [Corsello et al., Nature Cancer (2020)](https://pmc.ncbi.nlm.nih.gov/articles/PMC7328899/). `sample_info.csv` is DepMap cell-line metadata; its exact release has not yet been verified. The [dockerized_mts repository](https://github.com/cmap/dockerized_mts/blob/master/biomarker_files/README.md) supplied the original discovery route.

Upstream data retain their respective terms. Datasets are not redistributed in this repository. Gene-expression data are not included in the current inputs.
