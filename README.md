# Conditional quantile correction for workflow completion quotations

Research materials accompanying manuscript **2024659**, revised for the **Practitioner's Corner** of *Applied Stochastic Models in Business and Industry*.

**Review version: [pc-v1.0.0](https://github.com/liziqi2064/workflow-quantile-correction/releases/tag/pc-v1.0.0).** The release assets contain code, prepared real-data matrices, saved predictions, comparison settings, the latest supplementary information and the historical implementation archive. No GitHub account is needed to download them. This is an author-prepared revision, not an accepted or peer-reviewed publication.

Authors: Ziqi Li, Mengyang Wang, Tianqi Zhou, **Jiarui Wang**. Jiarui Wang is fourth in the revised author list. Journal processing of the requested author-list change is separate from this public research deposit.

## Start here

1. Open the [fixed review release](https://github.com/liziqi2064/workflow-quantile-correction/releases/tag/pc-v1.0.0).
2. Download **pc_reproduction_v1.0.0.zip** and **SHA256SUMS.txt**. Extract the ZIP.
3. In its `pc_reproduction` folder, install the pinned requirements and run:

```sh
python -m pip install -r requirements.txt
python run_checks.py
python run_checks.py --broader
```

Alternatively, the self-contained exploratory calibration needs only Python's standard library:

```sh
python round37_coverage_calibration/reproduce.py
```

Read [REPRODUCING.md](REPRODUCING.md) for inputs, expected values, result-to-file mapping, optional training and side effects. **The GitHub-generated “Source code” ZIP is only this landing page and navigation files; download the named research assets for the actual data and programs.**

## Release modules

| Asset | Contents | Use |
|---|---|---|
| `pc_reproduction_v1.0.0.zip` | Current correction code, prepared matrices, saved models, forecasts, frozen settings, DMQ source, diagnostic and calibration code | Recompute current results; optional saved-model checks and correction training |
| `historical_research_v1.0.0.zip` | Upstream scientific implementation, source manifests, derived task records, earlier experiments and technical appendices | Inspect historical method construction and comparisons; not a tested one-command raw-data retrain |
| `online_supporting_information.pdf` | Current 16-page supplement, S1–S7, Tables S1–S10, Figure S1 and its references | Read detailed methods, comparisons, exclusions and interpretation |
| `supporting_sources_v1.0.0.zip` | Editable supplement sources and figure | Inspect or compile the supplement |
| `SHA256SUMS.txt` | Exact hashes and byte sizes of the research assets | Verify download integrity |

The clean 12-page main manuscript, marked manuscript, response, cover letter, author details and unsigned author-change forms are supplied separately for the journal submission. Private editorial correspondence and personal review notes are excluded from the public research deposit.

## Main results and their scope

The selected conditional correction reduces mean four-quantile pinball loss by **6.28% and 6.00%** in two Alibaba evaluation windows (1,492 and 1,439 completed workflows). Individual scores improve for **75.87% and 65.46%** of jobs. A score is an asymmetric forecast penalty in time units, not a job failure or a measured financial loss. All comparators, unfavorable individual outcomes and historical alternatives remain in the data.

At nominal 90%, full-window conditional coverage is **87.60% and 91.10%**. In the first window, the subgroup with no completed task improves from **79.27% to 81.18%**. The exploratory later-subset calibration is a separate analysis: it does not replace those original figures, guarantee 90% future coverage, or meet both the coverage and loss criterion against the uncalibrated base in both windows.

Each workflow receives one quotation 15 seconds after its first task starts. Evaluation is retrospective and restricted to eligible completed jobs. The study supports the stated workflow implementation and adoption comparisons; it does not establish a universally superior dynamic-forecasting method, realized operating savings, or an all-arrivals service guarantee.

## Data sources and rights

Sources: [Alibaba Cluster Trace Program](https://github.com/alibaba/clusterdata), [Workflow Trace Archive](https://wta.atlarge-research.com/), and the BWA/Wien2k Zenodo records cited in [DATA_SOURCES.md](DATA_SOURCES.md). Raw Alibaba archives and large upstream model caches are not mirrored. See [LICENSES.md](LICENSES.md) for source terms and the retained GPL-3 DMQ attribution. Public access does not imply a blanket unrestricted license for third-party data.

The supplied checks distinguish frozen-prediction arithmetic, deterministic replay, model inference, correction training and upstream reconstruction. Fresh public-download verification is recorded in the release description and the local submission audit. No model fitting or new-data experiment is implied by a successful integrity check.
