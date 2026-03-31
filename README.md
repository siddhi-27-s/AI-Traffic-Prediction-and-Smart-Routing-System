
# Hybrid Intelligent Traffic Management System

A hybrid intelligent system that couples **Statistical Machine Learning** (Random Forest) with **Symbolic Reasoning** (Prolog) to forecast urban congestion and determine safe routing paths.

##  Project Overview
This project combines Machine Learning and Logic Programming to predict traffic conditions and suggest optimal routes across a small road network of 5 junctions (A–E).
A Random Forest classifier is trained on a synthetic dataset of 300 samples, learning to classify traffic as High, Medium, or Low based on the hour of day and vehicle count. It achieves ~97% accuracy.
The predicted traffic level is then passed to a Prolog knowledge base, which applies rule-based logic to recommend the best route — avoiding congested edges (A↔B, B↔C) during peak hours and falling back to mid-junction routing when needed.
The system runs in two modes — a batch mode that tests 4 preset scenarios (morning rush, midday, night, evening rush), and an interactive mode where the user inputs their own junction, hour, and vehicle count to get a real-time prediction and route suggestion.
Tech used: Python, scikit-learn, pandas, SWI-Prolog, PySwip.
### Key Features
* **Dual-Engine Architecture:** Uses ML for noisy sensor data and Prolog for human-readable safety rules.
* **Synthetic Data Generation:** Recreates 24-hour traffic cycles (Peak, Midday, Overnight) using NumPy.
* **No External Dependencies:** Operates independently of commercial traffic databases.
* **High Accuracy:** The Random Forest component achieves **>97% accuracy** on traffic level classification.

---

##  System Architecture

The project is structured into three distinct layers:

1.  **Data Layer:** Synthetic CSV generation (`traffic.csv`) using a fixed random seed for reproducibility.
2.  **Intelligence Layer:** * **ML Predictor:** Scikit-learn Random Forest Classifier.
    * **Logic Engine:** SWI-Prolog via PySwip for knowledge base (KB) reasoning.
3.  **Interface Layer:** CLI for batch processing and interactive user queries.

### The Road Network
The system manages five junctions (**a, b, c, d, e**) with bidirectional edges.
* **Congested Edges:** `a↔b` and `b↔c` are pre-marked as congested in the KB.
* **Routing Logic:** The system filters routes through a `safe/2` predicate to ensure drivers avoid high-risk or congested zones.

---

##  Getting Started

### Prerequisites
* **Python 3.x**
* **SWI-Prolog** (Must be installed and added to your system PATH)
* **Required Libraries:**
    ```bash
    pip install numpy pandas scikit-learn pyswip matplotlib
    ```

### Running the System
1.  **Generate & Train:** Run the system to create the `traffic.csv` and train the `model.pkl`.
2.  **Interactive Mode:**
    * Input a **Start Junction**, **End Junction**, **Hour**, and **Vehicle Count**.
    * The system will output a traffic prediction (with confidence bars) and a Prolog-derived route.

---

##  Dataset Design & ML Performance

The model classifies traffic into three tiers based on time and vehicle density:

| Traffic Level | Time Windows | Vehicle Range |
| :--- | :--- | :--- |
| **High** | 08:00–10:59 / 17:00–19:59 | 350–599 |
| **Medium** | 11:00–16:59 | 150–349 |
| **Low** | 00:00–07:59 / 20:00–23:59 | 10–149 |

### Classification Results
| Metric | High | Medium | Low | Weighted Avg |
| :--- | :--- | :--- | :--- | :--- |
| **Precision** | 1.00 | 0.96 | 1.00 | **0.99** |
| **Recall** | 1.00 | 1.00 | 0.93 | **0.98** |
| **F1-Score** | 1.00 | 0.98 | 0.96 | **0.98** |

---<img width="920" height="822" alt="vehicle-count" src="https://github.com/user-attachments/assets/deec77f3-1d32-4d73-ad7d-130c44a47748" />
<img width="921" height="817" alt="traffic-level-counts" src="https://github.com/user-attachments/assets/61488ddf-cd14-483d-9466-e3ebcd56f6d9" />


##  Prolog Routing Logic

The logic engine uses a `suggest/5` predicate to determine paths based on the following priority:

| Priority | Condition | Strategy | Advisory Note |
| :--- | :--- | :--- | :--- |
| 1 | High Traffic | Use safe/uncongested roads | Use alternate — high traffic |
| 2 | Medium Traffic | Direct route | Direct route
 OK |
| 3 | Low Traffic | Direct route | Clear — take direct route |
| 4 | Fallback | Any traffic | Route via mid-junction |

---

##  Limitations & Future Extensions
* **Current State:** Uses synthetic data and manual KB updates.
* **Scalability:** For city-scale deployment, A* or Dijkstra’s algorithm would replace the current routing logic.
* **Planned Upgrades:** * Integration of real-world datasets (PeMS/SCATS).
    * Dynamic Prolog fact assertion (`assert/retract`) for real-time sensor updates.
    * Development of a REST API using FastAPI.

---

## 📄 Conclusion
This prototype demonstrates that **Neuro-Symbolic AI** (learned patterns + structured reasoning) provides a more robust and explainable solution for urban mobility than either method used in isolation.
