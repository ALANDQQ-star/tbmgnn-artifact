# TBMGNN Artifact

This repository hosts the ACSAC artifact package for:

**TBMGNN: Transferable Bot Detection Method Based on Multi-View Graph Neural Networks**

Current release: **v1.1-artifact**
<https://github.com/ALANDQQ-star/tbmgnn-artifact/releases/tag/v1.1-artifact>

## What changed in v1.1

* **Tolerance-aware claim checks.** The claim checkers no longer require
  bit-exact floating-point equality. JSON structure, strings, booleans, nulls,
  and integer counters are compared exactly; floating-point fields are accepted
  within `atol=1e-9` and `rtol=1e-6` by default, and every verdict reports how
  many floating-point values needed the tolerance and the maximum deviation.
  `--strict` restores the old bit-exact behaviour. This fixes the spurious
  `fusion.json: DIFF` (13 values, max deviation ~5e-13) reported in review.
* **Fresh retraining works.** The missing `import copy` that raised
  `NameError: name 'copy' is not defined` is fixed, together with the next
  missing imports (`time`, `gc`, `json`, ...) that would have failed later in
  the same workflow. Retraining can now write to a separate model directory
  (`--model-dir`, `TBMGNN_MODEL_DIR`) so the released weights stay untouched,
  and the evaluation can actually consume the retrained bundles. A fast smoke
  test (`optional/retrain/smoke.sh`, minutes) and a retraining report
  (`src/retrainreport.py`) were added.
* **Install hardening.** `install.sh` pins torch 2.8.0 and the tested
  dependency set, installs the PyG sampling backend required by
  `NeighborLoader` (`pyg-lib`, with `torch-sparse` as fallback), and verifies
  it. v1.0 could install a newer torch build for which no PyG wheel exists.
* `run_all.sh` runs the five checked claims and prints a PASS/FAIL summary;
  `selftest.sh` runs the unit tests of the comparison policy.

See `REVIEW_RESPONSE.md` and `docs/PERMANENT_ARCHIVE.md` inside the package.

## Download

The full artifact is distributed through the release assets as split archive
parts. Download all files named:

```text
tbmgnn_artifact.tar.gz.part-*
tbmgnn_artifact.tar.gz.sha256
```

Reassemble and verify on Linux or WSL:

```sh
cat tbmgnn_artifact.tar.gz.part-* > tbmgnn_artifact.tar.gz
sha256sum -c tbmgnn_artifact.tar.gz.sha256
tar -xzf tbmgnn_artifact.tar.gz
cd artifacts
chmod +x install.sh py.sh run_all.sh selftest.sh claims/*.sh claims/*/run.sh optional/*/run.sh
./install.sh
./run_all.sh
```

The checked artifact evaluation runs on Ubuntu 22.04 or 24.04, including WSL2,
with Python 3, `python3-venv`, `pip`, and 16 GB RAM recommended (8-12 GB works
for the checked claims). See `README.txt` in the package for the individual
claims, the comparison policy, and the optional retraining workflows.

## Permanent archive

* Software Heritage save request for this repository:
  <https://archive.softwareheritage.org/api/1/origin/save/2585637/>
* Zenodo DOI deposit is prepared in the package (`.zenodo.json`,
  `docs/PERMANENT_ARCHIVE.md`) and will be linked here once published.

## Earlier release

`v1.0-artifact` (superseded) had exact floating-point comparisons and a broken
fresh-retraining path; both are fixed in v1.1. Keep using v1.1 for evaluation.
