# LexiFlow — Smart Reading & Writing Assistant

A project-level implementation of the assignment **Building a Smart Reading & Writing Assistant (NLP Pipeline)**. The application uses a React/Vite premium frontend and a FastAPI Python backend. It exposes all five syllabus stages as visible, testable UI views.

## Architecture
- `frontend/` — React + Vite UI
- `backend.py` — FastAPI API server
- `pipeline.py` — stage 1 → 4 orchestration
- `stage1_spell/` — from-scratch Levenshtein + context-aware spell checking
- `stage2_syntax/` — spaCy POS/dependencies + hand-written CKY/CFG parser
- `stage3_semantics/` — NER, semantic frames, Lesk-style WordNet WSD
- `stage4_discourse/` — heuristic coreference, discourse connectives, pragmatic inference
- `data/test_samples.txt` — 10 messy test samples

## Run locally
### Backend
```bash
pip install -r requirements.txt
uvicorn backend:app --reload --port 8000
```
The spaCy model is installed by the requirements URL.

### Frontend
```bash
cd frontend
npm install
npm run dev
```
Open the Vite URL shown in the terminal. The frontend expects the API at `http://localhost:8000` by default. For deployment, set `VITE_API_URL` to the deployed backend URL.

## Assignment mapping
1. Spell checking: Levenshtein distance is implemented from scratch; explicit typo corrections and context evidence are displayed.
2. Syntactic processing: spaCy POS/dependencies plus a hand-written compact CKY parser.
3. Semantic analysis: NER, semantic role frames and Lesk-style WSD for bank/bat/light.
4. Discourse/pragmatics: nearest-antecedent coreference, connective relation labels and indirect-request inference.
5. Full pipeline: `process(raw_text)` returns corrected text, syntax, semantic frames, discourse relations and summary data.
