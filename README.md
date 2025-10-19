# Insider Threat Detection Dashboard

An interactive Power BI dashboard for detecting insider threats by analyzing user behavior logs with a Python-based statistical risk-scoring engine. This project demonstrates an end-to-end analytical workflow, from raw data processing and statistical modeling to creating an interactive, decision-support tool.

---

## Final Dashboard


<img width="1416" height="763" alt="image" src="https://github.com/user-attachments/assets/d64b93a8-4ab7-4eee-bacd-6b2e8028aade" />

*A high-level overview of the Security Operations Center (SOC) dashboard, highlighting the top 10 riskiest users and their corresponding behavioral profiles.*

---

## Key Features

*   **Scalable Risk-Scoring Engine:** A Python script that processes data for 1,000 users, calculating a composite risk score based on multiple behavioral factors (file activity, after-hours work, weekend activity).
*   **Interactive SOC Dashboard:** The Power BI interface allows an analyst to select any high-risk user and instantly see their detailed behavioral data, including logon patterns, USB connection timelines, and most-used PCs.
*   **Statistical Anomaly Detection:** Utilizes Z-scores to mathematically identify and rank users, moving beyond simple volume metrics to find true behavioral outliers.
*   **Drill-Through Capability:** Analysts can right-click any user to pivot to a detailed, granular log view, showing every single logon and USB event for that individual.
*   **Narrative-Driven Investigation:** The analysis successfully identifies a "decoy" anomaly (an automated script) and pivots to uncover the true human threat, demonstrating a realistic investigative process.

---

## The Analytical Workflow

This project followed a structured, multi-stage analytical process:

### 1. Data Processing and Cleaning
The raw CERT Insider Threat Dataset (over 5GB) was processed using Python with the Pandas library. Key datasets for logon, file, and device activity were loaded, cleaned, and prepared for analysis.

### 2. Exploratory Data Analysis (EDA)
A corporate-wide baseline for "normal" behavior was established by visualizing logon activity. The resulting heatmap clearly identified the standard 7 AM - 6 PM workday and minimal weekend activity, defining what constitutes an "anomaly".

<img width="944" height="708" alt="image" src="https://github.com/user-attachments/assets/6d845273-b540-4fac-bcb7-52588226e733" />

*Heatmap showing normal logon patterns for the entire organization.*

### 3. Risk-Scoring Engine
A composite risk score was engineered for all 1,000 users. The score is a weighted sum of normalized values (Z-scores) for three key risk indicators:
*   Total volume of file copies.
*   Total number of after-hours logons.
*   Total number of weekend logons.

This system produced a ranked list of the most suspicious users.

<img width="964" height="475" alt="image" src="https://github.com/user-attachments/assets/027eb203-dc5b-49ee-bcdb-273d6fba7ca1" />

*The final ranked list of suspects, with AJF0370 identified as the highest risk.*

### 4. Interactive Dashboarding in Power BI
The risk scores and raw log data were loaded into Power BI. A relational data model (star schema) was built to connect the tables, and a dynamic, multi-visual dashboard was created to allow for interactive investigation.

<img width="1304" height="427" alt="image" src="https://github.com/user-attachments/assets/56e3f8ee-0707-4ac9-8bdd-1a843df63608" />

*The star schema data model connecting the risk scores to the logon and device event logs.*

### 5. Findings and Conclusion
The dashboard revealed a compelling story.
*   The user with the highest file volume (`HSB0196`) exhibited machine-like logon patterns, indicating it was a non-threatening automated process.
*   The user with the highest risk score (`AJF0370`) showed a clear human pattern of working late at night and on weekends, correlating directly with their high volume of file and USB activity. This user was identified as the primary insider threat.

<img width="1436" height="643" alt="image" src="https://github.com/user-attachments/assets/3a9d5460-51c6-4ade-bfef-fe1b82cc1717" />

*The filtered dashboard view for the top suspect, AJF0370, showing their highly anomalous logon and USB connection patterns.*

---

## Technical Stack

*   **Data Analysis & Modeling:** Python, Pandas, Jupyter Notebook
*   **Data Visualization & Dashboarding:** Microsoft Power BI
*   **Data Cleaning & ETL:** Power Query (within Power BI)
*   **Formulas & Measures:** DAX (within Power BI)

---

## How to Reproduce

1.  **Prerequisites:**
    *   Python 3.x
    *   Microsoft Power BI Desktop
2.  **Clone the repository:**
    ```bash
    git clone https://github.com/sohankanna/Insider-Threat-Detection-Dashboard.git
    ```
3.  **Data Source:**
    *   Download the CERT Insider Threat Dataset (r4.2) from an official source (e.g., Kaggle or Carnegie Mellon).
    *   **This dataset is not included in the repository due to its large size.**
    *   Place all the `.csv` files inside a folder named `data/` in the project's root directory.
4.  **Python Environment:**
    *   Create and activate a virtual environment:
      ```bash
      python -m venv venv
      source venv/bin/activate  # On Windows: .\venv\Scripts\Activate.ps1
      ```
    *   Install the required libraries:
      ```bash
      pip install pandas jupyter notebook seaborn
      ```
5.  **Execution:**
    *   Run the `insider_threat_analysis.ipynb` Jupyter Notebook. This will perform the analysis and generate the necessary files in the `processed_data/` folder.
    *   Open the `Insider_Threat_Dashboard.pbix` file in Power BI Desktop.
    *   Click "Refresh" to ensure it connects to the data files you have generated.
