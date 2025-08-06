# ⚙️ Source Code — Symbolic Forgetting Memory

This folder contains the **core implementation** of the symbolic forgetting system.

Everything here should be modular and eventually production-quality.

### Planned Modules:
- `memory.py`: MemoryItem class, strength logic, decay loop
- `compression.py`: Symbolic and vector compression routines
- `retrieval.py`: Ping-based pattern matching + FAISS/semantic recall
- `storage.py` *(optional)*: Archiving system and segmentation logic

### Principles:
- Separation of concerns: memory logic ≠ retrieval logic ≠ compression logic
- Designed to allow switching compression methods later
- Favor readability and experimentation

> When this system stabilizes, this folder becomes the deployable engine.
