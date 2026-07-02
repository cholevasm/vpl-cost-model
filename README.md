# VPL — A Cost Model for Satellite Constellations

A parametric **cost estimating relationship (CER)** for the development and production cost of
navigation and communication satellite constellations, for Earth and Mars orbit. Winner of the
2025 ESA/CNES Cost Engineering Challenge; presented at the **ESA/CNES Cost Engineering Conference 2026**.

M. Cholevas (TU München) · G. Vardanikas (TU Delft)

## The model

```
TOTAL(M, N) = F · g · [ DEV(M) + PFM(M) · N^LRE ]          (FY2025 EUR M)

DEV(M) = 3.29 · M^0.682          (one-time development)
PFM(M) = 0.215 · M^0.828         (first-unit production)
LRE    = 1 + ln(0.9)/ln(2) = 0.848
g      = 1 (traditional) | 0.118 (New-Space)
F      = 1 (Earth) | 1.14 (Mars)
```

`M` = platform (bus) mass in kg, `N` = number of units. Plug in `M` and `N` to get the programme cost.

## Results

- Leave-one-out cross-validation **R² = 0.92** over 27 systems (1997–2025); **0.81** on the traditional regime.
- A distinct **New-Space regime** costs **5–21× less** at equal mass and unit count.
- The development/production split is **identified from six disclosed programme budgets** (US SARs, ESA, GAO),
  bounding `DEV(1000 kg) = €365M` to ±1.3× (unit-cost data alone cannot identify it).
- On traditional systems the CER matches the **SMAD USCM8 + QuickCost** benchmark (R² = 0.86 for both);
  on New-Space systems that benchmark over-predicts unit cost by ~8×.
- Every model input is traceable to a public source (two-pass verified).

## Contents

| File | Description |
|---|---|
| `VPL_poster.pdf` | A0 conference poster |
| `VPL_report.pdf` | Full report (elsarticle), with the backtraceable dataset and provenance tables |
| `VPL_Cost_Model.ipynb` | Single-source-of-truth notebook (framework → dataset → model → results) |
| `vpl/` | Tested Python package: `dataset`, `model2` (the CER), `benchmark` (USCM8+QuickCost), `expanded` |
| `references/bibliography.bib` | All sources (BibTeX) |
| `references/provenance_final.json` | Per-attribute two-pass sourcing record |
| `figures/` | Vector figures used in the report |

## Reproduce

```bash
pip install -r requirements.txt
jupyter notebook VPL_Cost_Model.ipynb        # run top-to-bottom
# or, from the package:
python -c "from vpl import expanded, model2; f=model2.fit(expanded.rows()); print(model2.loocv(expanded.rows()))"
```

## License / citation

Please cite the conference paper. The dataset and code are provided for research and review.
