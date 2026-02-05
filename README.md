# 📜 The Translation Wars: LLM vs. Google Translate

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Domain](https://img.shields.io/badge/Domain-NLP_%7C_Linguistics-purple?style=for-the-badge)
![Metric](https://img.shields.io/badge/Metric-Levenshtein_%26_Jaccard-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Audit_Complete-success?style=for-the-badge)

## 📌 Project Overview
**"When machines speak, do they say the same thing?"**

Roman Urdu (Urdu written in English script) is a notoriously noisy and low-resource language format. This project conducts a **Linguistic Audit** comparing how two giants—**Google Translate** and a **Large Language Model (LLM)**—interpret and translate Roman Urdu into English.

Using a dataset of **4,000 parallel sentences**, we analyze consensus, divergence, and hallucination patterns to determine which engine handles the nuances of this informal script better.

**Author:** Muhammad Atif

## 📂 Dataset
The analysis is based on a rich parallel corpus covering 20 distinct topics (e.g., Sports, Politics, Technology).
* **Input:** Roman Urdu (e.g., *"Kya haal hai?"*)
* **Target 1:** Google Translate Output
* **Target 2:** LLM Output
* **Reference:** Urdu Script (optional context)

## 🛠 Tech Stack
* **Language:** Python
* **NLP & Metrics:** `difflib` (Sequence Matching), `collections` (N-Grams)
* **Data Manipulation:** `pandas`, `numpy`
* **Visualization:** `seaborn`, `matplotlib`, `wordcloud`

## 📊 Methodology: The Metrics of Disagreement

To quantify the "War" between the two models, we engineering specific linguistic features:

### 1. Levenshtein Distance (Edit Distance) 📏
Measures the minimum number of single-character edits required to change the LLM's translation into Google's translation.
* *High Distance* = Total Disagreement (Different interpretation of meaning).
* *Low Distance* = Consensus.

### 2. Jaccard Similarity 🔗
Measures the intersection over the union of the set of words.

$$J(A, B) = \frac{|A \cap B|}{|A \cup B|}$$

* Allows us to see if both models used the same vocabulary, even if the sentence structure differed.

### 3. Length Complexity 📝
Comparing word counts to see if LLMs suffer from "verbosity" (over-explaining) compared to Google's literal approach.

## 🔍 Key Insights & Visuals

### ☁️ Linguistic Fingerprints

We generated **Word Clouds** for both outputs.
* **Google:** Tends to use direct, simpler English vocabulary.
* **LLM:** Often infers context, using more descriptive or formal synonyms.

### 📉 The Consensus Gap
Our density plots of Jaccard Similarity reveal that while both models agree on simple sentences (e.g., "Hello", "Good Morning"), they diverge significantly on **idiomatic expressions** and **slang**, where Roman Urdu is most ambiguous.

## 🚀 How to Run

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/translation-wars.git](https://github.com/your-username/translation-wars.git)
    ```
2.  **Install dependencies:**
    ```bash
    pip install pandas numpy seaborn matplotlib wordcloud
    ```
3.  **Run the Analysis:**
    Open `the-translation-wars-llm-vs-google.ipynb` to view the comparative metrics.

## 💻 Code Teaser
Here is how we calculated the similarity consensus between the AI giants:

```python
from difflib import SequenceMatcher

def calculate_similarity(text1, text2):
    """Calculates similarity ratio between two translation outputs."""
    return SequenceMatcher(None, str(text1), str(text2)).ratio()

df['Consensus_Score'] = df.apply(lambda x: calculate_similarity(x['Google_Translate'], x['LLM_Translate']), axis=1)
