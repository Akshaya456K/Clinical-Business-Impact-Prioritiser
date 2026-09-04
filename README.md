The Clinical Business-Impact Prioritiser is an AI-powered system to help hospital IT teams quickly identify and prioritise urgent, patient-facing incidents among routine IT service requests. It analyses ticket data (text, service affected, user group, schedule, impact) to predict priority levels (P1–P4). The approach combines a simple rule-based baseline with a machine learning model, along with explanation/evidence for each high-priority decision. Safety checks and a human-in-the-loop fallback ensure reliable outcomes.

##System Architecture & Components
The system is organized into modular components:

EDA Notebook (eda.ipynb): Exploratory Data Analysis and data validation on the synthetic hospital tickets dataset (2,000 entries, fields like Ticket ID, content, affected service, user group, schedule, escalation, etc.).
Rule-Based Baseline (baseline.py): Computes a simple risk score using predefined rules (service, user, schedule) to assign a priority.
ML Model Training (train_model.py): Trains a classifier using text and structured features. Produces a trained model in the models/ folder.
Prediction (predict.py): Loads the trained model to predict priorities for new tickets.
Safety Logic (safety.py) & Decision Engine (decision_engine.py): Validates inputs, checks for low-confidence predictions, and routes uncertain cases for human review.
Event Handling (event_processor.py, event_test_processor.py): Processes ticket updates and tests for duplicate, delayed, or out-of-order events to maintain correct state.
Explanation Layer (explanation.py): Generates supporting evidence and recommended actions for high-priority predictions.
Evaluation (evaluate_system.py): Compares baseline vs ML performance and computes final metrics.
Streamlit App (app.py): Integrates all modules into a web interface: ticket entry, dashboard, explanations, and monitoring.

##Dataset
A synthetic dataset of 2,000 hospital IT tickets was used for development. Key fields include:

Ticket Content: Description of the issue.
Affected Service: e.g. “Lab System”, “Radiology”, etc.
User Group: e.g. “Doctor”, “Nurse”, “Admin”.
Operating Schedule: On-hours or off-hours.
Escalation Outcome: e.g. “Not Escalated”, “Escalated”, “Emergency”.
Priority (P1–P4): Manually assigned. P1/P2 are considered high-impact.
##Core Results
Metric	Value
Baseline Accuracy	59.25%
ML Model Accuracy	99.75%
Improvement (points)	40.50
High-Impact Precision	100%
High-Impact Recall	100%
High-Impact F1 Score	100%
Avg. Processing Time	0.0946 ms

The ML model greatly outperformed the rule-based baseline, especially in identifying P1/P2 tickets (100% precision/recall on the test set). The average processing time (~0.095 ms per ticket) meets the sub-1000 ms goal.

##Setup & Usage
Clone the repo and install dependencies:
bash
Copy
git clone <repo-url>
cd Clinical-Business-Impact-Prioritiser
pip install -r requirements.txt
Run the Streamlit app:
bash
Copy
python -m streamlit run app.py
This launches the web interface (usually at http://localhost:8501).
Train or evaluate models (optional):
To retrain or test the ML model on the dataset:
bash
Copy
python train_model.py
To compare baseline and ML performance:
bash
Copy
python evaluate_system.py
Official docs: Streamlit installation and pip usage provide guidance.

##Repository Structure
ruby
Copy
Clinical-Business-Impact-Prioritiser/
│
├── models/                  # Trained ML models
├── reports/                 # Evaluation outputs
│
├── hospital_it_tickets.xlsx # Synthetic dataset (CSV)
├── eda.ipynb                # Data exploration and validation
├── baseline.py              # Rule-based prioritiser
├── train_model.py           # ML model training
├── predict.py               # Predict new ticket priorities
├── safety.py                # Input checks and fallback logic
├── decision_engine.py       # Decision integration logic
├── event_processor.py       # Handle ticket events/updates
├── event_test_processor.py  # Tests for duplicate/delayed events
├── explanation.py           # Generate evidence/explanations
├── evaluate_system.py       # Final system evaluation
├── app.py                   # Streamlit application
│
├── requirements.txt         # Python dependencies
└── README.md                # Project overview (this file)


