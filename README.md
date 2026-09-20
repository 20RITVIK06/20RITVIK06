#!/usr/bin/env bash
# Applies metadata changes to your GitHub repos using the GitHub CLI.
# Prerequisites: install gh (https://cli.github.com), then run: gh auth login
# Review each line. Destructive commands are commented out on purpose.
# Do step 0 (rotate leaked keys) BEFORE anything else. See 00_AUDIT_AND_SUMMARY.md.
set -euo pipefail
OWNER=20RITVIK06

# ---- Descriptions and topics (safe, reversible) -----------------------------
gh repo edit $OWNER/production_incident_response_system \
  --description "OpenEnv-compatible RL environment simulating production incident response: partial observability, 3 difficulty tiers, deterministic graders." \
  --add-topic reinforcement-learning,openenv,incident-response,devops,simulation,pydantic,flask,python

gh repo edit $OWNER/loan_approval_system \
  --description "Explainable loan approval ML pipeline: SHAP explanations, fairness metrics, FastAPI backend, Streamlit dashboard (synthetic data)." \
  --add-topic machine-learning,explainable-ai,shap,fairness,xgboost,scikit-learn,fastapi,streamlit,python

gh repo edit $OWNER/sign-lang-translator \
  --description "Real-time sign recognition prototype: MediaPipe landmarks, PyTorch Transformer encoder, FastAPI WebSocket, React client (5 signs)." \
  --add-topic computer-vision,mediapipe,pytorch,transformer,fastapi,websocket,react,sign-language,python

gh repo edit $OWNER/engineering-assistant-RAG \
  --description "Document Q&A with retrieval-augmented generation: PDF/DOCX/TXT ingestion, embedding search, cited answers, low-confidence refusal. TypeScript, Express." \
  --add-topic rag,llm,embeddings,semantic-search,typescript,express,nodejs

gh repo edit $OWNER/LLM_api \
  --description "FastAPI service for question answering over PDFs using Pinecone retrieval, Gemini, and Redis caching." \
  --add-topic rag,fastapi,pinecone,gemini,redis,llm,python

gh repo edit $OWNER/music_generator \
  --description "PyTorch LSTM symbolic music generation from classical MIDI, with Streamlit UI." \
  --add-topic pytorch,lstm,music-generation,streamlit,python

gh repo edit $OWNER/translate_studio \
  --description "Small Node/Express translation app that keeps API keys server-side." \
  --add-topic nodejs,express,translation

gh repo edit $OWNER/stock_analyzer --description "DAA mini project: stock buy/sell analysis with brute-force and greedy algorithms."

# ---- Profile README ----------------------------------------------------------
# Copy profile/README.md over the README.md in your local clone of $OWNER/$OWNER, then:
#   git add README.md && git commit -m "Rewrite profile README" && git push

# ---- Renames (GitHub redirects old URLs; update links in your resume/READMEs) ---
# gh repo rename document-rag-chat  --repo $OWNER/engineering-assistant-RAG --yes
# gh repo rename document-query-api --repo $OWNER/LLM_api --yes
# Do NOT rename production_incident_response_system: openenv.yaml and any hackathon
# submission link to that URL.

# ---- Visibility / archive (reversible) ---------------------------------------
# gh repo edit $OWNER/operating-systems --visibility private --accept-visibility-change-consequences
# gh repo edit $OWNER/stock_analyzer    --visibility private --accept-visibility-change-consequences
# gh repo archive $OWNER/stock_analyzer --yes

# ---- Deletions (IRREVERSIBLE; needs: gh auth refresh -s delete_repo) ---------
# Only after rotating keys and confirming LLM_api has everything you need:
# gh repo delete $OWNER/weather-api    --yes   # committed venv/ (14k files)
# gh repo delete $OWNER/API            --yes   # duplicate of LLM_api
# gh repo delete $OWNER/Query_System   --yes   # earlier iteration of LLM_api
# gh repo delete $OWNER/Retrieval_api  --yes   # fork of your own repo

# ---- Pinned repositories: manual only (no API) -------------------------------
# github.com/20RITVIK06 > "Customize your pins". Recommended:
#   production_incident_response_system, loan_approval_system, sign-lang-translator,
#   engineering-assistant-RAG (or document-rag-chat), LLM_api (or document-query-api)
echo "Done. Now pin repositories in the GitHub UI."
