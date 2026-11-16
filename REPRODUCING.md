# Reproducing the PC revision

Release: **pc-v1.0.0**, 16 November 2026. This guide supersedes local round-by-round packaging notes. All experiments use previously examined records. Running these checks reproduces recorded calculations, not independent external validation.

## 1. Start with the numeric checks

Download `pc_reproduction_v1.0.0.zip` from the [versioned release](https://github.com/liziqi2064/workflow-quantile-correction/releases/tag/pc-v1.0.0) and extract it. From the `pc_reproduction` directory:

```sh
python -m pip install -r requirements.txt
python run_checks.py
python run_checks.py --broader
```

Tested environment: Python 3.12; package versions are pinned in requirements.txt. The first command suite checks frozen predictions, job-level score distributions, exploratory q90 recalibration and current table rendering. It needs no saved model deserialization, R, GPU or network. `--broader` also independently replays scalar policies and checks historical alternatives, objective scaling and refit cutoffs. Outputs go to each check's documented output subdirectory and `verification/`; rerunning replaces those reports. Source inputs are not overwritten. CPU only; allow a few minutes and ordinary desktop memory for these checks. Exact elapsed times from the release check are in verification records, not a forecasting benchmark.

The standard-library-only route is `python round37_coverage_calibration/reproduce.py`. Other quick checks need NumPy; broader replay needs pandas. The full pinned environment is recommended.

Expected main values (four-level mean pinball loss in seconds):

| Window start (h) | Jobs | Base loss | Conditional loss | Relative reduction | Conditional q90 coverage |
|---|---:|---:|---:|---:|---:|
| 144 | 1492 | 103.304860 | 96.815682 | 6.28% | 87.6005% |
| 168 | 1439 | 104.665767 | 98.389854 | 6.00% | 91.1049% |

Frozen metrics: 14 policies per window, 164,136 quantile forecast values and 134 predeclared comparisons. Recalibration: 77,340 fields compared with stored outputs. Integer counts are exact; full-precision comparisons use 1e-9 absolute tolerance. `status=passed` verifies the named calculations; it does not mean every method improves every criterion.

## 2. Map paper results to files

| Paper item | Inputs / implementation | Verification or generation |
|---|---|---|
| Main Table 3 common comparison; Table S7 cohort counts | `materials/analysis/prepared`, `materials/analysis/results`, `materials/evidence/common_predictions.csv.gz` | `checks/verify_recorded.py`; `round30_table_render/check_tables.py` |
| Mean loss, coverage, individual improvements and subgroup 81.18% | `round34_frozen_metrics/inputs` | `round34_frozen_metrics/check.py`; `round35_loss_distribution/check.py` |
| S6 decision diagnostics, Tables S8–S9 | `round28_decision_diagnostics`, `round28_feature_dictionary` | included diagnostic entries and dictionary |
| S7 exploratory 90% calibration, Table S10 | `round37_coverage_calibration/inputs`, fixed `analysis_plan.md` and all `outputs` | `round37_coverage_calibration/reproduce.py` |
| Earlier component and external comparisons, Figure S1 | `materials/historical`, `evidence/earlier_external`, optional historical archive | `materials/historical/verify_results.py`; `checks/verify_historical_alternatives.py` |
| DMQ transition identity | `materials/analysis/results/dmq_fixture.json` | `python materials/analysis/check_dmq_fixture.py` |

`roundXX` directory names identify frozen scientific packets, not alternative manuscript versions. Historical source hashes remain for provenance. Author-machine paths in old provenance records and preparation scripts are not required by the entry points above. The latest self-contained inputs and current release manifest determine the public package identity.

## 3. Optional inference, correction training and DMQ

Use a working copy for any command that replaces model or forecast outputs. From `pc_reproduction`:

```sh
python checks/verify_saved.py --materials materials --output model_check
python materials/analysis/run_common.py
```

The first loads the project's supplied scikit-learn model objects (created with 1.9.1); only use it for this trusted release. It checks inference and scalar replay, not training. The second refits the original correction candidates and selected models from prepared real matrices, with the recorded seed 20260920 and one numerical thread. It does not retrain upstream experts and overwrites the working copy's analysis results. Detailed roles, candidate settings, frozen base construction and objective differences are in `materials/analysis/protocol.md`, `dmq_settings.md` and the supplement. Training runtime varies and is separate from the quick checks.

DMQ uses the unmodified GPL-3 source archive `materials/third_party/DMQ_0.1.2.tar.gz`. R and its C++ compiler/dependencies are required; the package DESCRIPTION lists them. After installing that package, use:

```sh
Rscript materials/analysis/verify_dmq_saved.R materials/analysis
Rscript materials/analysis/run_dmq.R materials/analysis
Rscript materials/analysis/refine_dmq_optimization.R materials/analysis
```

The first checks saved filters. The last two estimate/refine DMQ on a working copy. They are not part of `run_checks.py`, and fresh execution of these routes is not claimed for this packaging release. The original rolling-initialization and DMQ state-index repairs are already present. Pre-repair arrays are explicitly historical and must not replace current arrays.

## 4. Historical upstream implementation and data access

The optional `historical_research_v1.0.0.zip` contains original scientific code, derived task/workflow records, models' source definitions, protocols, output tables, source manifests and historical experiments. It excludes old manuscript drafts and internal editorial notes. See its README and current SHA256 manifest. Some upstream scripts retain local path assumptions. Raw Alibaba archives and large original model caches are not redistributed. Obtain raw traces through the official sources in DATA_SOURCES.md. This release does **not** establish a tested one-command raw-trace-to-upstream-model retrain.

## 5. Interpretation

The evaluation concerns one quotation 15 seconds after first task start, on retrospectively eligible completed jobs. Loss is an asymmetric prediction score, not job failure or realized money lost. Both original windows show lower average score, while 24.13% and 34.54% of jobs have higher scores. No future or subgroup coverage guarantee follows.

The exploratory calibration uses earlier completed jobs at fixed midpoints and evaluates later-issued jobs. Both later subsets already exceed 90% coverage before adjustment. First-window padding fails the joint coverage/loss criterion against the uncalibrated base; second-window padding is zero. It does not repair the original full-window 81.18% subgroup result. All six specified policies and unfavorable controls remain available.

Third-party source terms and authorship are preserved. See LICENSES.md. Editorial correspondence, personal work logs and signed author forms are not public research inputs.
