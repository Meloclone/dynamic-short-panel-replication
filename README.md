# Replication materials for dynamic short panels

This repository contains the code, data, configuration files, and generated
outputs for the manuscript **“Separating State Dependence from Serial
Correlation in Dynamic Short Panels.”** It is an anonymous repository version
prepared for peer review.

The complete submission-ready archive is available as
`JBES_code_and_data_2026-08-21.zip` in the repository root.

## Contents

- `simulation/`: Monte Carlo designs, configuration files, replication-level
  results, grouped summaries, and plotting code.
- `empirical/`: Spanish and United Kingdom manufacturing-panel analyses,
  numerical audits, bootstrap diagnostics, source data, and reported outputs.
- `output/figures/`: vector figures and PNG previews used to check the
  manuscript graphics.
- `plot_style.py` and `plot_journal_previews.py`: shared plotting style and the
  descriptive-data figure script.
- `requirements.txt`: Python environment requirements.

## Data provenance

The empirical source files are the `Snmesp` and `EmplUK` datasets distributed
with the CRAN `plm` package. CSV conversions are included for transparent
inspection, and the original R data files are retained for exact reproduction.
No confidential or individually identifiable data are used.

## Environment

The reported results were produced with Python 3.11. From the repository root:

```text
python -m venv .venv
python -m pip install -r requirements.txt
```

## Main reproduction commands

```text
python simulation/monte_carlo.py --config simulation/config_main.json --out simulation/remote_main --workers 1
python simulation/plot_results.py
python empirical/empluk_analysis.py --out empirical/results.csv
python empirical/spanish_analysis.py --out empirical/spanish_results.csv
python empirical/spanish_time_dummies.py --out empirical/spanish_time_dummies.json
python empirical/key_audit.py --out empirical/audit_results.csv
python empirical/estimation_audit.py
python empirical/bootstrap.py --data empirical/data/Snmesp.csv --dataset spanish --B 999 --workers 1 --out empirical/bootstrap/spanish_bootstrap.csv
python empirical/plot_empirical.py
python plot_journal_previews.py
```

The `simulation/RESULTS.md` and `empirical/RESULTS.md` files identify the
headline results reported in the manuscript. The bootstrap is a stability
diagnostic; formal label inference uses the asymptotic minimum-distance
statistics described in the manuscript.

## Reproducibility note

The repository is organized so that the supplied source data, scripts,
configuration files, and reported intermediate results can be inspected
without access to the authors’ local working directory.

## License

The scripts are released under the MIT License. The included empirical data
remain subject to the terms of the original CRAN `plm` data distribution.
