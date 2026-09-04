#  Clinical Impact Prioritiser

An AI-assisted incident prioritisation system designed to help hospital IT teams identify clinically and operationally high-impact service failures among routine support requests.

The system combines rule-based logic, machine learning, operational context, safety controls, and human review pathways to prioritise hospital IT incidents into four priority levels.

> This project is a decision-support prototype and does not replace clinical, operational, or professional judgement.

---

##  Problem Statement

Hospital IT teams support critical clinical and operational systems around the clock. Urgent patient-facing system failures can sometimes be hidden among a large number of routine IT support requests.

For example, a failure involving a clinical system, emergency department service, or critical hospital workflow may require immediate escalation, while routine technical requests may require lower priority.

This project aims to help prioritise hospital IT tickets based on ticket content and operational context, allowing high-impact incidents to be identified and escalated more efficiently.

---

##  Project Objective

The objective of this project is to develop an AI-assisted system that can:

* Analyse hospital IT support tickets.
* Predict incident priority.
* Identify clinically and operationally high-impact incidents.
* Support escalation decisions.
* Provide evidence and explanations for predictions.
* Detect duplicate events.
* Handle delayed and out-of-order events.
* Provide fallback workflows when predictions are uncertain.
* Support human review for safety-critical situations.

---

##  Key Features
###  AI-Based Priority Prediction

The system uses machine learning to predict the priority level of hospital IT incidents.

Priority levels include:

| Priority | Description                                     |
| -------- | ----------------------------------------------- |
| **P1**   | Critical incident requiring immediate attention |
| **P2**   | High-impact incident requiring urgent attention |
| **P3**   | Medium-priority incident                        |
| **P4**   | Low-priority or routine request                 |

---

###  Rule-Based Baseline

A rule-based baseline prioritisation system is included to provide a comparison against the machine learning model.

This allows the project to evaluate the improvement achieved through machine learning.

---

###  High-Impact Incident Detection

The system identifies P1 and P2 incidents as high-impact incidents.

These incidents may require:

* Faster escalation.
* Operational attention.
* Human review.
* Additional safety checks.

---

###  Machine Learning Model

The project uses machine learning techniques to analyse ticket information and predict incident priority.

The trained model is stored as:

```text
models/priority_model.joblib
```

The model is used by the prediction and decision engine to generate priority recommendations.

---

###  Explanation and Evidence Layer

The system provides supporting information for predictions, helping users understand why a ticket may have been classified as a high-impact incident.

This improves transparency and supports responsible AI practices.

---

### Safety Controls

The project includes safety mechanisms such as:

* Input validation.
* Evidence checks.
* Fallback behaviour.
* Human review pathways.
* Uncertainty handling.
* Event-state protection.

The system is designed to assist decision-making rather than automate critical decisions without human oversight.

---

###  Event Processing

The project includes an event processing system that handles potential operational failure scenarios.

These include:

#### Duplicate Events

Repeated events are detected to prevent duplicate processing and ticket-state corruption.

#### Out-of-Order Events

Older events are prevented from overwriting newer ticket information.

#### Delayed Events

The system preserves the latest valid ticket state when delayed events arrive.

---

## Streamlit Application

The project includes a multi-page Streamlit application.

The application provides the following sections:

###  Operations Dashboard

Provides an overview of:

* Incident statistics.
* Priority distribution.
* High-impact incidents.
* Escalation activity.

---

###  Prioritise Ticket

Allows users to enter ticket information and receive an AI-assisted priority prediction.

The system can provide:

* Predicted priority.
* High-impact status.
* Supporting evidence.
* Safety recommendations.
* Human review guidance.

---

###  Active Incident Queue

Displays incidents that may require operational attention.

Users can view and filter high-impact incidents based on priority and operational relevance.

---

###  System Monitoring

Provides information about:

* Model performance.
* Classification accuracy.
* Processing time.
* System performance metrics.

---

### Failure and Recovery

Demonstrates how the system handles operational event-processing failures, including:

* Duplicate events.
* Delayed events.
* Out-of-order events.

---

###  Responsible AI

Provides information about:

* Safety controls.
* System limitations.
* Human oversight.
* Deployment considerations.
* Responsible AI practices.

---

#  Dataset

The project uses a synthetic hospital IT ticket dataset.

Dataset file:

```text
hospital_it_tickets.csv
```

The dataset contains:

* Ticket information.
* Ticket content.
* Affected services.
* User groups.
* Operating schedules.
* Impact scope.
* Escalation outcomes.
* Priority labels.

## Dataset Statistics

| Metric           | Value |
| ---------------- | ----: |
| Total Tickets    | 2,000 |
| Training Samples | 1,600 |
| Testing Samples  |   400 |
| Missing Values   |     0 |
| Duplicate Rows   |     0 |

### Priority Distribution

| Priority | Number of Tickets |
| -------- | ----------------: |
| P1       |               200 |
| P2       |               400 |
| P3       |               600 |
| P4       |               800 |

> The dataset used in this project is synthetic and is intended for experimentation and demonstration purposes.

---

#  System Results

The system was evaluated using a held-out synthetic test dataset.

| Metric                  |                  Result |
| ----------------------- | ----------------------: |
| Baseline Accuracy       |                  59.25% |
| ML Model Accuracy       |                  99.75% |
| Improvement             | 40.50 percentage points |
| High-Impact Precision   |                    100% |
| High-Impact Recall      |                    100% |
| High-Impact F1 Score    |                    100% |
| Average Processing Time |               0.0946 ms |
| Target Processing Time  |                 1000 ms |
| Target Achieved         |                     Yes |

These results are based on the synthetic dataset used for this project and should not be interpreted as real-world clinical deployment performance.

---

#  Technologies Used

* Python
* Streamlit
* Pandas
* Scikit-learn
* Joblib
* Plotly
* Machine Learning
* Data Analysis
* Responsible AI

---

#  Project Structure

```text
Clinical-Impact-Prioritiser/
│
├── app.py
├── baseline.py
├── decision_engine.py
├── event_processor.py
├── evaluate_system.py
├── explanation.py
├── predict.py
├── safety.py
├── train_model.py
├── test_event_processor.py
│
├── hospital_it_tickets.csv
├── eda.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
├── models/
│   └── priority_model.joblib
│
└── reports/
    └── evaluation_results.csv
```

---

#  File Description

## `app.py`

The main Streamlit application.

Provides the user interface for:

* Operations dashboard.
* Ticket prioritisation.
* Active incident queue.
* System monitoring.
* Failure-state demonstrations.
* Responsible AI information.

---

## `baseline.py`

Contains the rule-based baseline prioritisation logic.

The baseline system is used to compare traditional rule-based prioritisation against the machine learning approach.

---

## `decision_engine.py`

Acts as the central decision-making component.

It combines prediction, evidence, safety checks, and prioritisation logic.

---

## `event_processor.py`

Handles ticket events and protects the system against event-processing issues such as:

* Duplicate events.
* Delayed events.
* Out-of-order events.

---

## `explanation.py`

Provides explanations and evidence related to priority predictions.

This supports transparency and responsible AI decision-making.

---

## `predict.py`

Loads the trained machine learning model and generates priority predictions for incoming tickets.

---

## `safety.py`

Contains safety controls and fallback mechanisms.

It helps ensure that uncertain predictions and potential failures can be directed toward appropriate human review.

---

## `train_model.py`

Used to train the machine learning priority prediction model.

The trained model is saved for later use by the application.

---

## `evaluate_system.py`

Evaluates the performance of the overall prioritisation system.

Evaluation results are stored in the reports directory.

---

## `test_event_processor.py`

Tests the event-processing functionality, including handling of duplicate, delayed, and out-of-order events.

---

## `hospital_it_tickets.csv`

Contains the synthetic hospital IT ticket dataset used for model training, testing, and analysis.

---

## `eda.ipynb`

Contains exploratory data analysis for understanding the dataset and priority distribution.

---

## `models/priority_model.joblib`

Contains the trained machine learning model.

---

## `reports/evaluation_results.csv`

Contains system evaluation results and performance metrics.

---

#  Installation

## 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/Clinical-Impact-Prioritiser.git
```

## 2. Navigate to the Project Directory

```bash
cd Clinical-Impact-Prioritiser
```

## 3. Create a Virtual Environment

```bash
python -m venv .venv
```

## 4. Activate the Virtual Environment

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

### Windows Command Prompt

```cmd
.venv\Scripts\activate
```

### Linux/macOS

```bash
source .venv/bin/activate
```

## 5. Install Dependencies

```bash
pip install -r requirements.txt
```

---

#  Running the Application

Start the Streamlit application using:

```bash
streamlit run app.py
```

The application will open in your web browser.

---

#  Running System Evaluation

To evaluate the prioritisation system, run:

```bash
python evaluate_system.py
```

---

#  Training the Machine Learning Model

To train or retrain the model:

```bash
python train_model.py
```

The trained model will be stored in the `models` directory.

---

#  Testing Event Processing

To test the event-processing functionality:

```bash
python test_event_processor.py
```

---

#  Responsible AI Considerations

This project is designed as an AI-assisted decision-support prototype.

It does not replace:

* Clinical judgement.
* Professional judgement.
* Operational decision-making.
* Human incident management.

The system includes several responsible AI considerations:

* Human review pathways.
* Input validation.
* Evidence-based predictions.
* Fallback behaviour.
* Uncertainty handling.
* Event-state protection.

---

#  Limitations

This project has several limitations:

* The dataset is synthetic.
* Real hospital IT environments may contain more complex incident patterns.
* Model performance may vary with real-world data.
* Predictions should not be used as the sole basis for critical decisions.
* Real deployment would require privacy, security, validation, governance, and regulatory considerations.

---

#  Future Improvements

Potential future improvements include:

* Real-time incident ingestion.
* Integration with hospital IT service-management platforms.
* Advanced NLP models.
* Transformer-based text classification.
* Explainable AI dashboards.
* Role-based access control.
* Audit logging.
* Model monitoring and drift detection.
* Real-time alerting.
* Integration with external incident-management systems.
* Bias and fairness evaluation.
* Secure production deployment.

---

#  Author

Developed as an AI-assisted Clinical Business-Impact Prioritisation project using Python, Machine Learning, Streamlit, and Responsible AI principles.

---

# Support

If you find this project useful, consider giving the repository on GitHub!
