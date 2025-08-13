# Architecture Overview

## Flow
|Ingress|→|Active Store|→|Policy|→|Compressor|→|Archive Store(s)|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | | |↑| | | |↓|
|     |     |     |     |Retriever||←||Cues/context|



## Components
- Ingress: normalizes new memories (content + metadata)
- Active Store (fast): recent, high-M items (KV + ANN index)
- Policy Engine: computes M and decides keep/compress/drop
- Compressor: produces Level 1–3 representations
- Archive Stores: slower tiers (vector DB + symbol graph + signatures)
- Retriever: hybrid search (embedding + symbolic pattern)
- Telemetry: logs uses→reinforcement; writes to Failures/Insights

## Data model (sketch)
Memory {
  id, timestamps, source,
  rep_levels: {L0_raw?, L1_vec, L2_symbols, L3_signature},
  scores: {M, R, F, I, U, C},
  history: [{event, t, deltaS}]
}

## Tiers & latency targets
- Tier A (RAM/SSD): Active Store, ANN index (ms)
- Tier B (SSD/disk): L1 vectors, L2 symbols (10–100 ms)
- Tier C (cheap): L3 signatures (subsecond)

## Lifecycle
1) New item → compute initial M → Active Store.
2) Periodic sweep: apply decay; re-score; compress/demote/promote.
3) On query: hybrid retrieval; on use: reinforce S and F.
4) Telemetry feeds metric dashboards for tuning λ, α_use, thresholds.
