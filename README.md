# Real-Time Attack Detection and Analysis Using a Low-Interaction Honeynet

1) Problem Overview  

Binary or multi-class classification of cyberattacks captured from a low-interaction honeynet in real time.  
The system detects and classifies malicious activity such as brute-force attacks, port scanning, and suspicious behavior with low latency to enable early warning on a host system.

---

2) Goals & Success Criteria  

Primary  
- Accuracy ≥ 90%  
- F1-score (attack classes) ≥ 0.88  
- Inference latency < 1s per log event (p95)  

Secondary  
- False Positive Rate (normal → attack) ≤ 2%  
- Stable performance during continuous 1-hour lab sessions  

---

3) Data Summary  

Sources  
- Real-time logs from low-interaction SSH honeypots  
- Locally generated attack traffic during controlled lab sessions  

Format  
- JSON or CSV  

Latest dataset version  
- See DATASET_CARD.md  

Bias & Privacy  
- Data collected only from honeynet systems  
- No real user data or PII  
- Traffic is simulated or unsolicited, minimizing privacy risk  

---

4) Features (current plan)  

Network-level  
- Source IP address  
- Destination port  
- Protocol  
- Connection rate per time window  

Authentication  
- Username attempt count  
- Password attempt count  
- Login success or failure ratio  

Behavioral  
- Command sequence length  
- Command frequency  
- Attempts per minute  

---

5) Modeling  

Baselines  
- Logistic Regression  
- Decision Tree  

Advanced  
- Random Forest  
- Isolation Forest for anomaly detection  

Explainability  
- Feature importance based on tree models  
- Key indicators include login rate, port count, command frequency  

Model releases tracked in MODEL_CARD.md  

---

6) Evaluation  

Offline  
- Accuracy  
- Precision  
- Recall  
- F1-score (macro and per attack class)  

Online (lab validation)  
- Detection rate during live attacks  
- Alert delay  
- False positive count per session  

Results and experiment lineage stored in EVAL_LOG.md  

---

7) Versioning & Refinement Workflow (Main)  

Git is used for version control of code, data summaries, and experiments.

DATASET_CARD.md  
- Dataset schema  
- Size and class distribution  
- Collection method and date  
- Known biases or limitations  

MODEL_CARD.md  
- Model version  
- Training dataset reference  
- Feature set  
- Metrics and latency  

EVAL_LOG.md  
- Experiment runs  
- Configurations and random seeds  
- Confusion matrices  

CHANGELOG.md  
- Human-readable summary of changes  

FEEDBACK_LOG.md  
- Instructor or stakeholder feedback  
- Action items and resolution status  

Update cadence  

Weekly  
- Minor fixes and feature adjustments  
- EVAL_LOG updates  

Bi-weekly  
- Dataset refresh from new honeynet logs  
- MODEL_CARD update if retrained  

Monthly  
- Review detection quality and false positives  
- Update CHANGELOG and FEEDBACK_LOG  

Refinement triggers  

- F1-score < 0.88 for attack classes  
- Sudden increase in false positives  
- Inference latency > 1s  
- Feedback from lab evaluations  

How to add an update  

- Create a branch: docs/update-YYYY-MM-DD-short-title  
- Update relevant documentation files  
- Open a pull request with before/after metrics  
- Merge and update CHANGELOG.md  

---

8) Reproducibility  

- Fixed random seed: 42  
- Configuration files stored in configs/  
- Each experiment records:
  - Dataset version  
  - Feature list  
  - Model parameters  
  - Commit hash  
  - Execution environment  

---

9) Ethics & Risk  

- Honeynet is fully isolated and controlled  
- No outbound traffic or attack propagation  
- Minimize false positives to avoid misleading alerts  
- Used strictly for educational and research purposes  

---

10) Architecture & Workflow  

High-level flow  
- Honeypot generates logs  
- Feature extraction in real time  
- ML model performs classification  
- Alerts or labels sent to monitoring dashboard  

Detailed workflow diagrams are available in docs/workflow.md  
