# BigMart Sales Prediction App

A Streamlit app that predicts item outlet sales for BigMart-style retail data using a pre-trained scikit-learn model packaged with version metadata. The interface collects item and outlet attributes, builds a single-row pandas DataFrame, and outputs a point estimate for sales.

### Features
- Intuitive Streamlit UI with text, select, slider, and numeric inputs.
- Model artifact bundled with scikit-learn version for transparency and compatibility display
- Direct pandas DataFrame inference without manual encoding in the UI layer.

## Tech stack and requirements

- Language: Python 3.10+ recommended.
- Web UI: Streamlit (>=1.30).
- ML/Array/Data: scikit-learn (>=1.3), pandas (>=1.3), numpy (>=1.21), joblib (>=1.2).
- Optional integrations: SQLAlchemy (>=2.0) and PyMySQL (>=1.0) for future persistence/logging.
- OS: Linux, macOS, or Windows.

Dependencies file (requirements.txt) should contain:
- pandas>=1.3
- numpy>=1.21
- scikit-learn>=1.3
- joblib>=1.2
- pymysql>=1.0
- streamlit>=1.30
- sqlalchemy>=2.0

## Repository structure

- app.py or app-4.py: Streamlit application code.
- bigmart_best_model.pkl: Pickle containing (model, sklearn_version).
- - requirements.txt: Python dependencies.
  
## Model artifact contract

The app expects a pickle named bigmart_best_model.pkl in project root with:
- model: a fitted estimator exposing predict(DataFrame) and returning a numeric sales value.
- sklearn_version: a string with the scikit-learn version used during training, displayed in the UI.

Note: Ensure the prediction pipeline inside the model handles categorical encodings and any scaling/feature engineering internally, as the UI passes raw, human-readable values.

## Installation

- Create and activate a virtual environment (venv or conda).
- Install dependencies: pip install -r requirements.txt.
- Place bigmart_best_model.pkl in the repository root.

## Running locally

- Start the app: streamlit run app.py (or streamlit run app-4.py if keeping the filename).
- Open the local URL that Streamlit prints in the terminal.

## Inputs schema

The UI collects the following fields; values are passed as-is to the model via a single-row pandas DataFrame:
- Item_Identifier: string, e.g., “FDA15”.
- Item_Weight: float, non-negative.
- Item_Fat_Content: one of ["Low Fat", "Regular"].
- Item_Visibility: float in [0.0, 0.3].
- Item_Type: one of the listed retail categories (e.g., “Dairy”, “Snack Foods”).
- Item_MRP: float, non-negative.
- Outlet_Identifier: one of the listed IDs (e.g., OUT027, OUT013, …).
- Outlet_Size: one of ["Small", "Medium", "High"].[2]
- Outlet_Location_Type: one of ["Tier 1", "Tier 2", "Tier 3"]
- Outlet_Type: one of ["Supermarket Type1", "Supermarket Type2", "Supermarket Type3", "Grocery Store"].
- Outlet_Age: integer in.

## Usage

- Fill inputs and click “Predict Sales”.
- The app displays “Using scikit-learn vX.Y.Z” based on the pickled version and outputs a currency-formatted sales prediction.

## Deployment

- Streamlit Community Cloud:
  - Rename app file to app.py for auto-detection.
  - Push repo with requirements.txt and bigmart_best_model.pkl.
  - Optionally pin Python version via a runtime.txt if needed.
- Docker (optional):
  - Use a Python base image, copy app, requirements, and pickle, then run streamlit run app.py.

## Configuration

- No environment variables are required by default.
- For DB logging extensions, configure SQLAlchemy URL via env vars and install drivers (PyMySQL).

## Testing

- Smoke test: launch app and predict with defaults; ensure no errors
- Determinism test: repeat same input; predictions should match.
- Boundary test: test min/max ranges for numeric fields (e.g., visibility 0.0 and 0.3)

## Troubleshooting

- FileNotFoundError: Ensure bigmart_best_model.pkl is in project root.
- Version issues: If pickle fails due to version mismatch, retrain or re-serialize with runtime scikit-learn, or ensure compatible ABI. The app displays expected version for visibility.
- Feature handling: If categorical mapping errors occur, ensure the model’s preprocessing pipeline supports the provided categories.

### About Author
Pulin Shah — Lead IT Support Coordinator | IT Service Delivery | n8n Automations |ML|DL|Data Science|Prompt Enigneering|RAG|Gen-AI|EDA

IT service delivery leader with 20+ years across incident, change, and problem management, PSA/RMM operations (ConnectWise), and endpoint security. Designs and operates Service Desk workflows with SLA rigor, and builds support automations using n8n, LLMs, and vector search for policy-aligned responses.

Leads Service Desk operations: ticket triage, scheduling, vendor coordination, SLA governance, and reporting.

Builds LLM-powered assistants on Telegram with strict topic guardrails and end-of-conversation flows.

Implements RAG pipelines: Google Drive ingestion, OpenAI embeddings (512-dim), Pinecone indexing, and chunking strategies for retrieval quality.

Experienced with ESET/SentinelOne endpoints, Microsoft stack, AWS (Solutions Architect), and ITIL-based practices for change/incident/request management.

Links

GitHub: https://github.com/Pulin2411

LinkedIn: linkedin.com/in/pulin-shah-741212b

Email: pulin2411@gmail.com


