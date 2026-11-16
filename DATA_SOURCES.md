# Data origin and interpretation

## Alibaba Cluster Trace 2018

Official source: https://github.com/alibaba/clusterdata/tree/master/cluster-trace-v2018

The original batch-task archive is at https://aliopentrace.oss-cn-beijing.aliyuncs.com/v2018Traces/batch_task.tar.gz . The source project recorded 130,310,549 bytes and SHA256 `7c4b32361bd1ec2083647a8f52a6854a03bc125ca5c202652316c499fbf978c6`. The raw archive and partial instance downloads are not redistributed here.

The publisher’s README permits research/study use. Consult its current terms before reuse: https://github.com/alibaba/clusterdata . This package does not represent the Alibaba data as CC0 or grant a new blanket data license. The retained derived records and predictions support research reproduction, with the original source attribution intact.

Historical source manifests are in `archive/data/manifest.json` and source-specific audit records. The remaining-time target includes waiting and execution, uses one landmark at origin + 15 seconds, and is measured in seconds. The main release includes only retrospectively eligible completed workflows; it is not a complete production arrival log.

## Workflow Trace Archive / new-ASKALON

BWA: https://doi.org/10.5281/zenodo.3254520

Wien2k: https://doi.org/10.5281/zenodo.3254478

The retained official record metadata identify CC0 for these records. Copies of the metadata and the full 67-source file manifest are in `archive/revisions/external_v5/`. Check the specific source record when reusing a trace. The phase-to-parent reconstruction uses WTA’s published conversion logic; task events are engine timing records and do not identify CPU service starts.

## Root CSV fields

`job`: released workflow identifier; `job_id`: numeric source identifier where available; `origin`: first recorded task start; `issue`: origin + 15; `end`: issue + remaining; `remaining`: observed remaining completion time; `window`: evaluation start hour (144 or 168); `block`: six-hour origin block; `method`: comparator name; `tau`: quantile level; `prediction`: quoted remaining duration. All time values except `window` and the block index use seconds. Initialization files carry base forecasts `p0`–`p3` at levels 0.5, 0.8, 0.9 and 0.95.

`replay_metrics.csv` reports `mean_loss`, percent relative `gain_vs_base`, descriptive interval endpoints `ci_lo`/`ci_hi`, and coverage fractions. These intervals hold realized adaptive predictions fixed, use only four temporal blocks per window and do not include model-fitting or selection uncertainty.

The research archive contains original, unchanged result records with their historical method names. Some historical metadata contain local relative paths or prior execution information; those are provenance records rather than requirements of the root reproduction command. No private editor correspondence is included.
