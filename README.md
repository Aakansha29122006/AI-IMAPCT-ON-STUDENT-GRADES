# 🎓 AI Impact on Student Grades: Predictive Analysis & Insights

Dataset source - https://www.kaggle.com/datasets/rakeshkapilavai/ai-tool-usage-by-indian-college-students-2025?select=Students.csv

---

## 📖 Introduction & Abstract
Artificial Intelligence (AI) has rapidly transitioned from a niche technology to a fundamental component of the educational landscape. This research project investigates the multi-faceted impact of AI tools—such as ChatGPT, Gemini, and GitHub Copilot—on student academic performance. 

By utilizing a robust dataset of over **3,600 survey responses**, this project moves beyond simple correlation to develop a predictive classification model. We explore not just "if" AI affects grades, but "how" specific usage behaviors, tools, and demographic factors contribute to either academic enhancement or degradation.

---

## 📌 Project Objectives
The primary goals of this analysis are:
1.  **Behavioral Mapping:** Identify the most common AI use cases among students (e.g., assignment writing vs. doubt solving).
2.  **Predictive Modeling:** Develop a high-accuracy classifier using K-Nearest Neighbors (KNN) to predict student outcomes.
3.  **Data-Driven Recommendations:** Provide actionable insights for educators on how to integrate AI responsibly into the curriculum.
4.  **Bias & Imbalance Mitigation:** Demonstrate advanced ML techniques like SMOTE and PCA to handle real-world, skewed survey data.

---

## 📂 Project Structure
```text
├── data/
│   └── (Dataset files used for training)
├── notebooks/
│   └── AI IMPACT ON STUDENT GRADES.ipynb  # Comprehensive analysis & ML pipeline
├── visualizations/
│   ├── confusion_matrix.png               # Final model performance check
│   ├── metrics_summary.png                # Precision, Recall, F1 comparison
│   ├── ai_usage_distribution.png          # Tool-wise usage breakdown
│   └── grade_impact_heatmap.png           # Feature correlation matrix
├── models/
│   └── knn_model_final.pkl                # Serialized model (if applicable)
├── requirements.txt                       # Dependency list
└── README.md                              # Project documentation
```

---

## 📊 Dataset Detail & Feature Engineering
The dataset consists of **3,614 entries** across **16 initial features**.

### Key Features Explained:
| Feature Name | Description | Data Type |
| :--- | :--- | :--- |
| `Stream` | The academic field of the student (Engineering, Arts, Science, etc.) | Categorical |
| `AI_Tools_Used` | Specific platforms used (ChatGPT, Gemini, Copilot, etc.) | Multi-label |
| `Daily_Usage_Hours` | Time spent on AI tools per day | Numeric |
| `Use_Cases` | Primary intent (Assignments, MCQ practice, Learning, Doubt Solving) | Multi-label |
| `Trust_in_AI` | Level of confidence in AI-generated content (Scale 1-5) | Numeric |
| `Awareness_Level` | Self-reported knowledge of AI capabilities | Numeric |
| `Professor_Guidance` | Whether a teacher encouraged/guided the student in using AI | Boolean |

---

## 🔍 Detailed EDA Insights (What We Found)
The Exploratory Data Analysis (EDA) phase was crucial in understanding the underlying data distribution.

### 1. The "Efficacy Gap" between Tools
While **ChatGPT** dominates the market share (~70% usage), our data indicates that students using **Google Gemini** and **Microsoft Copilot** often reported higher scores in the "Positive Impact" category. This suggests that specialized or multi-modal tools may offer better learning support than general-purpose chat.

### 2. Strategic vs. Tactical Usage
Students who utilized AI for **"Doubt Solving"** and **"Coding Help"** were **3.4x more likely** to report a positive impact on grades compared to those who used it primarily for **"Assignment Completion."** This highlights a clear distinction between using AI as a tutor vs. a proxy.

### 3. The 2-Hour Threshold
Academic benefit shows a bell-curve relationship with time. Students using AI for **1-2 hours daily** saw the highest positive shift. Beyond **4 hours**, the impact skewed toward "Negative" or "No Impact," likely due to over-reliance and reduced critical thinking.

---

## 🛠️ Data Preprocessing Methodology
Real-world survey data is rarely clean. Our methodology involved:
1.  **Cleaning & Formatting:** Handled multi-select columns by creating binary dummy variables for each possible tool and use case.
2.  **Target Categorization:** Transformed continuous grade impact scores into three distinct classes: *Negative (0), No Impact (1), and Positive (2).*
3.  **SelectKBest:** Used statistical tests (ANOVA F-value) to select the top 14 features that had the highest mutual information with the target variable.
4.  **SMOTE (Synthetic Minority Over-sampling Technique):** The original data was heavily skewed toward "Positive" impact. We applied SMOTE to balance the "No Impact" and "Negative" classes, ensuring the model doesn't ignore these critical outcomes.
5.  **PCA (Principal Component Analysis):** We reduced our 50+ binary features into **29 orthogonal components**, capturing 95% of the total variance while significantly reducing the "Curse of Dimensionality."

---

## 🤖 Model Training & Hyperparameter Tuning
We selected the **K-Nearest Neighbors (KNN)** algorithm due to its non-parametric nature and effectiveness in multi-class classification.

### Tuning Process:
*   **GridSearchCV:** Iterated through K values from 1 to 30.
*   **Optimal K:** Found at **K=17**, providing the best balance between bias and variance.
*   **Distance Metric:** **Manhattan Distance (L1)** was chosen over Euclidean, as it provided better separation in the high-dimensional PCA space.
*   **Weights:** Used **'distance' weighting**, ensuring that closer neighbors have a larger influence on the prediction than distant ones.

---

## 📈 Model Performance & Validation
The model was validated using an 80-20 stratified split and cross-validation.

### Final Metrics Summary:
*   **Accuracy:** **94.12%**
*   **Precision:** **0.94**
*   **Recall:** **0.94**
*   **F1-Score:** **0.94**

### Graphical Checks:
*   **Confusion Matrix:** Confirmed that the model rarely confuses "Positive" with "Negative" impact, which is critical for educational interventions.
*   **Metrics Bar Graph:** Visualized the consistency of our F1-Score across all three classes, proving the success of our SMOTE balancing.

---

## 📜 Future Work & Limitations
*   **Dataset Expansion:** Include more diverse geographical data beyond the current survey pool.
*   **Longitudinal Study:** Track the same students over multiple semesters to see how AI impact changes over time.
*   **Algorithm Testing:** Explore Random Forests or Gradient Boosting models to compare performance with the current KNN baseline.

---


