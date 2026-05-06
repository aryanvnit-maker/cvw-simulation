# CVW Simulation Study

This repository contains the simulation study reported in Section 5.3.1 of:

Shah, A. (2026). *Convergent-Validity-Weighted Integration of Multi-Instrument Personality Data*. Zenodo. https://doi.org/10.5281/zenodo.19842795

---

## What this repository contains

- **`cvw_simulation.py`** — The simulation script. Takes no arguments; running it reproduces all results reported in the paper.
- **`data/cvw_simulation_results.csv`** — The full simulation output (three conditions × two integration methods × MAE values × bootstrap confidence intervals).
- **`data/cvw_simulation_figure.png`** — The MAE comparison figure reproduced from Section 5.3.1.
- **`LICENSE`** — MIT License. The simulation code is free to use, modify, and redistribute.

---

## What the simulation does

The script tests whether the Convergent-Validity-Weighted (CVW) integration formula recovers a latent target construct with lower error than equal-weight averaging, across three levels of convergent-validity spread:

1. **Uniform validity** — all three simulated instruments correlate with the target at r = 0.70.
2. **Moderate differential validity** — instruments correlate at r = 0.75, 0.65, 0.55.
3. **High differential validity** — instruments correlate at r = 0.80, 0.60, 0.40.

For each condition, 10,000 synthetic respondents are simulated. Mean absolute error (MAE) is computed between the recovered composite score and the known latent construct score. Bootstrap 95% confidence intervals are computed from 2,000 resamples.

**Expected results** (reproduced from Section 5.3.1 of the paper):

| Condition | MAE (CVW) | MAE (Equal-weight) | CVW advantage |
|---|---|---|---|
| Uniform validity | 0.418 | 0.418 | +0.00% |
| Moderate differential | 0.455 | 0.467 | +2.59% |
| High differential | 0.467 | 0.511 | +8.63% |

---

## How to reproduce the results

### If you already have Python installed

Open a terminal in this repository and run:

```
python cvw_simulation.py
```

The script prints all results to the console and writes the CSV to `data/cvw_simulation_results.csv`. Running time is approximately 30 seconds on a standard laptop.

**Dependencies:** `numpy` and `pandas`. If either is missing, install with:

```
pip install numpy pandas
```

### If you don't have Python installed

The repository includes the full results in `data/cvw_simulation_results.csv` and the comparison figure in `data/cvw_simulation_figure.png`. You can inspect these directly without running anything. The paper's Section 5.3.1 table is a direct transcription of the CSV.

---

## Reproducibility

The script uses a fixed random seed (`SEED = 2026`) for the main simulation. Running the script on different machines or different Python versions will produce the same MAE values for each condition to within numerical precision of `numpy`'s Mersenne Twister implementation.

Bootstrap CIs may drift by tiny amounts across machines due to implementation details of bootstrap indexing; the main MAE values are deterministic under the fixed seed.

---

## Author context

This repository is released alongside a methods-paper preprint. The author (Aryan Shah) wrote the CVW architecture specification and the simulation design; the simulation code was implemented in Python from that specification. The author does not come from a software-engineering background and is shipping this repository as research material rather than as production software. The simulation code is intentionally simple and straightforward to read.

If you find issues with the code or have suggestions for improving the specification's simulation reproducibility, please open a GitHub issue on this repository.

---

## Citation

If you use or adapt this simulation, please cite:

```
Shah, A. (2026). Convergent-Validity-Weighted Integration of Multi-Instrument
Personality Data. PsyArXiv preprint. (https://zenodo.org/records/19842795)
```

---

## License

MIT License. See `LICENSE` file for full terms.
