# Track A: Data Analyst Assignment Explanation

 1. Project Architecture & Decisions
* **Data Ingestion Pipeline:** The data is loaded dynamically using a semicolon delimiter (`sep=';'`). 
* **Interactive Tooling:** Streamlit was chosen for the interactive front-end as it allows Relationship Managers to isolate variables on the fly without writing SQL or modifying python scripts.
* **Missing Value Handling Strategy:** Instead of removing or arbitrarily modifying rows with `"unknown"` tokens, we retained them explicitly within the structural category breakdowns. This tracks downstream system gaps without introducing bias into demographic calculations.

 2. Core Business Insights & Answers

 Q1: Which job types have the highest subscription rate?
* **Findings:** **Students** (~28.68%) and **Retired** individuals (~22.79%) possess the highest conversion probabilities.
* **RM Action Strategy:** RMs should pitch structural cash accumulation packages to younger students looking for low-risk alternatives, and stable asset preservation models to retirees.

 Q2: Account Balance Pattern vs Likelihood to Subscribe
* **Findings:** Subscribers have a significantly higher median capital reserve (~$733) compared to non-subscribers (~$417). 
* **RM Action Strategy:** Implement a filter threshold focusing outreach efforts on clients holding over $700 in available balances to avoid inefficient cold-calling.

Q3: Subscription Rate across Age Groups
* **Findings:** Outbound campaigns show a distinct U-shaped curve. Seniors (**60+**) convert at an exceptional **42.26%**, and younger groups (**18-30**) follow at **16.22%**. Mid-career segments remain low.
* **RM Action Strategy:** Pivot campaign intensity away from target demographics aged 31–60 towards older wealth management groups.

 Q4: Does having an existing housing loan make someone less likely to take a new product?
* **Findings:** Yes. Unencumbered individuals subscribe at a rate of **16.70%**, while clients carrying existing housing loans fall sharply to **7.70%**.
* **RM Action Strategy:** Filter out clients with active housing liens to protect margin and efficiency.


Section 1: Core Technical & Analytical Questions (Everyone)

 1. What percentage of customers in your dataset have y = yes? What does this imbalance mean for how you'd evaluate a model?
Approximately **11.70%** of the customers in the dataset have `y = yes` (5,289 out of 45,211 rows). Because the dataset is highly imbalanced, using standard **Accuracy** as an evaluation metric would be highly misleading, as a naive model could simply predict "no" for every client and still achieve ~88% accuracy. Instead, a classification model should be evaluated using metrics like **Precision, Recall, F1-Score, or the Area Under the Precision-Recall Curve (AUPRC)** to ensure it effectively captures actual subscribers without destroying operational efficiency.

 2. Which job category had the highest subscription rate? Does this make sense to you intuitively?
The **Student** category had the highest absolute subscription rate at **28.68%**, followed closely by **Retired** individuals at **22.79%**. This makes perfect intuitive sense because both groups are in distinct lifecycle transitions where low-risk, guaranteed financial vehicles are highly attractive. Students are often looking for safe, predictable structural options to start growing limited cash reserves, while retirees prioritize asset preservation and stable yields over high-risk market investments.



 Section 2: Project Architecture & Execution (Track A Context)

 3. Key Design Decisions:
 Data Processing: Data is dynamically ingested using the semicolon delimiter (`sep=';'`). Missing entries explicitly labeled as `"unknown"` were deliberately kept as structural sub-categories to transparently monitor data collection gaps without introducing demographic imputation bias.

 Interactive Interface: Streamlit was deployed as the frontend to give Relationship Managers (RMs) a self-service tool. They can cross-filter client data cohorts dynamically by job, marital status, or housing liabilities without needing to query a database or alter python scripts.

 4. How to Execute the Project

1. Install Dependencies:
   ```bash
   pip install streamlit pandas matplotlib seaborn

  a. Generate Baseline Analysis Plots:
python eda_analysis.py

b.Launch the Interactive RM Dashboard Server:
python -m streamlit run app.py

The default web browser will automatically load the live interactive system application at http://localhost:8501