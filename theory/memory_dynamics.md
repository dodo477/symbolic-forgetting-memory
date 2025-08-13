# Memory Dynamics

## State variables
- S(t): memory strength in [0, 1]
- f: usage frequency (short rolling window)
- r: recency (time since last use)
- I: semantic importance (model-estimated)
- U: utility (task success contribution)
- C: storage cost (size/latency penalty)

## Update rule (continuous decay + discrete reinforcement)
Decay:      S(t+Δ) = S(t) * exp(-λΔ)
Reinforce:  on use at time t*: S ← clamp(S + α_use * g(context), 0, 1)

Where g(context) can include:
- match confidence / cue similarity
- task reward or success signal
- novelty bonus (penalized if redundant)

## Composite scoring (for policy decisions)
Score M = w_r*R + w_f*F + w_i*I + w_u*U - w_c*C
- R := exp(-β * r)       # recent memories score higher
- F := normalized freq
- I, U come from model heuristics or labels
- C reflects bytes and retrieval latency

## Policy thresholds (mutually exclusive bands)
- τ_active: keep in fast store if M ≥ τ_active
- τ_archive: compress+archive if τ_archive ≤ M < τ_active
- τ_drop: drop if M < τ_drop (or convert to ultra‑coarse sketch)

Typically: τ_active > τ_archive > τ_drop

## Compression schedule
- Level 0: full object (raw text+metadata)
- Level 1: dense vector + salient spans
- Level 2: symbolic sketch (triples, tags, key claims)
- Level 3: cue-only signature (hash + topic + anchors)

Promote/demote level based on M and storage pressure.

## Retrieval trigger
Return candidates if cosine_sim(cue, vec) ≥ θ_vec OR
symbolic_match(sketch, cue_graph) ≥ θ_sym.
On retrieval, apply small reinforcement (contextual).

