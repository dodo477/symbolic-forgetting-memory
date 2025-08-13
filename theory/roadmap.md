# Roadmap 

## Sprint 1: Minimal Dynamics
- Implement M scoring (R, F, I, U, C) + decay/reinforce
- In-memory Active Store with ANN (faiss/pynndescent or placeholder)
- CLI demo: ingest → query → see state change

## Sprint 2: Compression Levels
- L1 vectorization + salient span extraction
- L2 symbolic sketcher (triples/tags from salient spans)
- Policy thresholds + periodic sweep

## Sprint 3: Hybrid Retrieval
- Vector + symbolic retrieval; simple rank fusion
- Retrieval-triggered reinforcement; novelty penalty

## Sprint 4: Metrics & Tuning
- Track hit-rate, latency, storage footprint, promotion/demotion churn
- Grid search λ, α_use, {τ_active, τ_archive, τ_drop}, θ_vec/θ_sym
