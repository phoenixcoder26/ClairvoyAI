# ClairvoyAI: Agentic SEC Filing Risk Intelligence System

ClairvoyAI is an end-to-end financial risk intelligence project that transforms SEC 10-K Item 1A Risk Factor disclosures into structured risk signals, normalized disclosure-risk scores, analyst-facing recommendations, machine learning benchmarks, advanced NLP similarity diagnostics, a RAG-style analyst assistant, and interactive dashboard outputs.

The project integrates natural language processing, PostgreSQL database design, SQL analytics, classical machine learning, an experimental TensorFlow/Keras neural network, TF-IDF similarity analysis, risk-theme clustering, retrieval-style evidence ranking, and executive-style dashboarding to demonstrate a complete applied analytics workflow for financial risk intelligence.
---

## Live Demo

View the animated ClairvoyAI dashboard here:

https://phoenixcoder26.github.io/ClairvoyAI/

---

## Project Objective

The objective of ClairvoyAI is to reduce the manual burden of reviewing long-form SEC 10-K risk disclosures by converting unstructured Item 1A text into structured, interpretable, and decision-ready risk intelligence.

The system is designed to answer three analytical questions:

1. Which companies exhibit the highest disclosure-language risk intensity?
2. Which risk themes are driving the score?
3. What should an analyst prioritize for further review?

Rather than treating SEC filings as static documents, ClairvoyAI converts disclosure language into a structured analytical layer that supports ranking, trend analysis, risk-driver diagnosis, machine learning validation, and dashboard-based exploration.

---

## Companies Analyzed

The MVP analyzes 25 SEC 10-K filings across five publicly listed companies from 2021 to 2025.

- Airbnb — ABNB
- Amazon — AMZN
- Boeing — BA
- Pfizer — PFE
- Tesla — TSLA

This company set was selected to provide cross-sector variation across technology, aerospace, healthcare, consumer marketplace, and electric vehicle/manufacturing risk profiles.

---

## Current Project Status

Completed components include:

- SEC 10-K Item 1A Risk Factor extraction
- Text cleaning and preprocessing
- NLP-based risk-driver signal engineering
- Risk-driver normalization per 10,000 words
- SEC filing risk score creation on a 0–100 scale
- Risk-level classification into Low, Moderate, Elevated, and High
- Top risk-driver identification
- Evidence snippet extraction from risk-factor language
- Analyst-style explanation generation
- Recommended analyst action generation
- PostgreSQL database design and loading
- SQL analytics and validation queries
- Classical machine learning benchmarking
- Experimental TensorFlow/Keras neural network modeling
- Advanced NLP similarity and risk-theme clustering
- TF-IDF cosine similarity analysis across company-year filings
- RAG-style analyst assistant for grounded filing-level Q&A
- Saved ML artifacts and prediction outputs
- Interactive Streamlit dashboard
- Animated HTML dashboard concept for portfolio presentation
- Planned AWS cloud architecture design

---

## Data Pipeline

```text
SEC 10-K HTML filings
        ↓
Item 1A Risk Factor extraction
        ↓
Text cleaning and disclosure preprocessing
        ↓
Keyword-based NLP risk-signal extraction
        ↓
Risk-driver counts
        ↓
Normalization per 10,000 words
        ↓
SEC filing risk score, 0–100
        ↓
Risk-level classification
        ↓
Evidence snippets + analyst explanation
        ↓
PostgreSQL storage
        ↓
SQL analytics + ML benchmarking
        ↓
Advanced NLP similarity + risk-theme clustering
        ↓
RAG-style evidence retrieval and analyst Q&A
        ↓
Streamlit dashboard / animated portfolio page

---

## Risk Drivers Used

ClairvoyAI tracks nine normalized risk-driver features. Each feature is calculated per 10,000 words so filings can be compared despite differences in Item 1A text length.

### 1. Liquidity Risk

Captures references to cash constraints, funding pressure, liquidity access, working capital risk, and capital availability.

### 2. Debt / Credit Risk

Captures leverage, debt obligations, credit exposure, borrowing constraints, refinancing risk, and covenant-related pressure.

### 3. Interest Rate Risk

Captures financing-cost sensitivity, interest-rate exposure, rate volatility, and debt-service implications.

### 4. Inflation / Cost Risk

Captures inflationary pressure, input-cost increases, labor-cost pressure, supplier cost escalation, and operating-cost inflation.

### 5. Revenue / Demand Risk

Captures demand uncertainty, sales volatility, revenue pressure, customer demand shifts, and market adoption risk.

### 6. Profitability / Margin Risk

Captures margin compression, earnings pressure, profitability deterioration, cost-to-margin exposure, and operating leverage risk.

### 7. Supply Chain Risk

Captures supplier disruption, production constraints, logistics bottlenecks, delivery delays, inventory pressure, and manufacturing dependency.

### 8. Macroeconomic Risk

Captures economic cycle exposure, recession risk, market volatility, geopolitical uncertainty, and broad macroeconomic demand shocks.

### 9. Regulatory / Litigation Risk

Captures legal exposure, compliance risk, regulatory scrutiny, investigations, lawsuits, enforcement actions, and litigation uncertainty.

---

## PostgreSQL Database

A PostgreSQL database named `clairvoyai` was created and populated using a Dockerized PostgreSQL environment.

The database design follows a normalized relational structure with five core tables:

- `companies` — company-level metadata
- `sec_filings` — filing-level metadata by company and fiscal year
- `risk_scores` — risk score, risk level, and text-length metrics
- `risk_driver_counts` — long-format risk-driver signal counts
- `agent_recommendations` — top drivers, evidence, explanation, and recommended action

Final loaded row counts:

- `companies`: 5 rows
- `sec_filings`: 25 rows
- `risk_scores`: 25 rows
- `risk_driver_counts`: 225 rows
- `agent_recommendations`: 25 rows

The SQL layer supports portfolio-level analysis, company-level trend analysis, risk-driver aggregation, year-over-year score movement, and analyst action review.

---

## SQL Analytics Layer

The PostgreSQL layer was used to validate the structured risk outputs and generate analytical views for dashboarding.

Example SQL analyses included:

- Average risk score by company
- Highest-risk filings by ticker and fiscal year
- Top risk drivers by company-year
- Year-over-year risk score movement
- Risk-level distribution across the portfolio
- Analyst recommendation review
- Risk-driver aggregation across companies
- Company-level trend ranking

This SQL layer strengthens the project by demonstrating relational data modeling, database normalization, query-based validation, and analytical reporting.

---

## Machine Learning Benchmark

The machine learning phase evaluated whether the engineered NLP risk-driver features could reproduce ClairvoyAI’s four risk-level classifications.

The task was formulated as a multiclass classification problem.

Target classes:

```text
Low
Moderate
Elevated
High
```

Models benchmarked:

1. Logistic Regression
2. Random Forest
3. Gradient Boosting
4. TensorFlow/Keras Neural Network

The input matrix contained nine normalized risk-driver features. The target variable was the filing-level `risk_level`.

The TensorFlow/Keras model was included as an experimental neural-network extension. The final compact architecture used:

```text
9 input features → Dense 16 → Dropout → Dense 8 → Output 4 classes
```

The architecture was intentionally kept compact because the current MVP dataset contains only 25 filings. This design reduces unnecessary model complexity and makes the neural-network component more defensible as a proof-of-concept extension.

---

## ML Interpretation Note

The machine learning results should be interpreted with appropriate caution.

Because the current MVP includes only 25 filings, and the risk-level labels are derived from the same rule-based scoring framework used to create the engineered features, the ML benchmark should be viewed as internal feature-validation rather than production-grade predictive modeling.

The results indicate that the engineered risk-driver features are highly separable across the current ClairvoyAI risk tiers. However, a larger and more diverse dataset would be required before making claims about real-world generalization, external predictive performance, or production deployment.

---


---

## Advanced NLP Similarity and Risk-Theme Clustering

Phase 4B extends ClairvoyAI beyond keyword-based risk scoring by adding TF-IDF similarity analysis and risk-theme clustering.

The advanced NLP layer converts filing-level evidence, top risk drivers, and analyst explanations into TF-IDF vectors. Cosine similarity is then used to compare risk language across company-year filings and across companies. K-Means clustering and PCA are used to identify disclosure-language groupings and visualize risk-theme patterns in two dimensions.

Advanced NLP outputs include:

- Filing-level TF-IDF cosine similarity matrix
- Company-level risk-language similarity matrix
- PCA-based risk-theme clustering
- Top TF-IDF terms by risk level
- Evidence-strength diagnostics by company
- NLP cluster composition by risk level

This phase helps evaluate whether filings with similar risk levels also share similar disclosure-language patterns. Because the MVP contains only 25 filings, the advanced NLP outputs are interpreted as exploratory diagnostics rather than production-grade semantic modeling.

## RAG-Style Analyst Assistant

Phase 4C adds a lightweight RAG-style analyst assistant to ClairvoyAI.

The assistant converts filing-level risk scores, top risk drivers, evidence snippets, analyst explanations, and recommended actions into searchable text records. A TF-IDF retriever ranks the most relevant company-year filings for a user question using cosine similarity. The system then produces evidence-backed analyst responses grounded in the retrieved filing records.

Example questions supported by the prototype include:

- Why is Boeing classified as High risk?
- What evidence supports Tesla’s Elevated risk level?
- Which companies show the strongest supply chain risk?
- Compare Amazon and Pfizer risk disclosures.
- What are the main regulatory and litigation risks across filings?

This first version is described as a RAG-style prototype because it uses processed filing evidence and TF-IDF retrieval. A future version can connect the retrieved evidence to an LLM for full retrieval-augmented generation.

## Key Findings

### 1. Boeing exhibited the highest disclosure-risk intensity

Boeing was the highest-risk company in the sample and appeared consistently in the High-risk category across the analyzed filing years.

Primary contributing drivers included:

- Supply Chain Risk
- Revenue / Demand Risk
- Regulatory / Litigation Risk

This suggests that Boeing’s Item 1A disclosures contained substantially higher risk-signal density than the other companies in the MVP portfolio.

### 2. Tesla remained consistently Elevated

Tesla was generally classified as Elevated risk. Its disclosure-risk profile was below Boeing but clearly higher than lower-risk companies such as Airbnb and Pfizer.

Tesla’s filings showed meaningful exposure to:

- Supply Chain Risk
- Revenue / Demand Risk
- Regulatory / Litigation Risk

### 3. Amazon remained Moderate

Amazon was generally classified as Moderate risk. Its risk signals were present but less concentrated than Boeing or Tesla, resulting in a more balanced disclosure-risk profile.

### 4. Airbnb and Pfizer remained Low

Airbnb and Pfizer generally appeared in the Low-risk category in the current MVP sample. Their normalized risk-driver signals were comparatively lower across the selected risk categories.

### 5. Supply Chain Risk emerged as a major discriminating feature

Feature importance analysis showed that Supply Chain Risk was one of the strongest variables for separating higher-risk filings from lower-risk filings.

This effect was especially driven by Boeing’s high supply-chain signal density relative to other companies in the portfolio.

### 6. Frequent risk themes were not always the most predictive

Regulatory / Litigation Risk appeared across multiple filings, but it was not always the strongest discriminating feature.

This highlights an important machine learning principle: a feature can be frequent without being highly useful for separating classes. Predictive value depends not only on frequency, but also on how well a feature differentiates one risk class from another.

---

## Dashboard

The project includes an interactive dashboard layer designed for executive risk review and analyst exploration.

Dashboard components include:

- Executive KPI cards
- Company × year risk heatmap
- Highest-risk filing leaderboard
- Average risk score by company
- Risk trajectory line chart
- Year-over-year risk movement
- Portfolio percentile ranking
- Risk-driver signal-density heatmap
- Driver composition analysis
- Filing-level explorer with evidence snippets
- Analyst explanation and recommended action
- ML model benchmarking panel
- Feature importance panel
- Neural-network confidence visualization

Run locally:

```bash
streamlit run app.py
```

The Streamlit dashboard is the main analytical interface for exploring the structured risk outputs.

---

## Animated Portfolio Page

An animated HTML dashboard concept was also created for portfolio presentation and visual storytelling.

It includes:

- Animated risk-score distribution
- 3D interactive risk cube
- Company scorecards
- Risk-level donut chart
- Top risk-driver bar chart
- Deep-ocean / iceberg visual theme

This animated page is intended as a visual landing page or demo mode. The Streamlit dashboard remains the primary analytical product.

---

## Planned AWS Cloud Architecture

ClairvoyAI was developed locally as an end-to-end analytics MVP using Python, PostgreSQL, machine learning, TensorFlow/Keras, and Streamlit. A future cloud deployment would extend the system into AWS for scalable storage, managed relational analytics, automated monitoring, and analyst alerting.

The proposed AWS architecture includes:

- Amazon S3 for storing raw SEC filings, processed CSV outputs, model artifacts, and dashboard assets.
- Amazon RDS PostgreSQL to replace the local Docker PostgreSQL database with a managed relational database.
- Amazon EC2 or AWS App Runner to host the Streamlit dashboard.
- AWS Lambda for scheduled filing checks and automated risk-monitoring workflows.
- Amazon CloudWatch for pipeline logs, dashboard monitoring, and operational observability.
- Amazon SNS for analyst email alerts when a filing crosses an Elevated or High-risk threshold.

Target architecture:

```text
SEC EDGAR / Processed Filing Inputs
        ↓
Amazon S3
        ↓
Python NLP Risk-Scoring Pipeline
        ↓
Amazon RDS PostgreSQL
        ↓
Streamlit Dashboard on EC2 / App Runner
        ↓
CloudWatch Monitoring
        ↓
SNS Analyst Alerts
```

This planned architecture would allow ClairvoyAI to scale from a local proof of concept into a cloud-ready financial risk intelligence platform.

---

## Advanced NLP Roadmap

The current MVP uses an interpretable keyword-based NLP framework to extract and normalize risk-driver signals from SEC 10-K Item 1A disclosures. This approach was selected for transparency, auditability, and explainability.

Future NLP enhancements may include:

- FinBERT or transformer-based classification for finance-specific risk language.
- Sentence-level embedding search to retrieve the most relevant evidence for each risk driver.
- Topic modeling to identify emerging or unexpected risk themes.
- Semantic clustering of risk-factor language across companies and years.
- Uncertainty and sentiment scoring to measure cautionary or negative disclosure tone.
- Named entity recognition to identify regulators, suppliers, geographies, products, and litigation-related entities.
- Retrieval-augmented analyst summaries using filing-level evidence snippets.

These enhancements would move ClairvoyAI from keyword-based signal extraction toward deeper semantic risk intelligence.

---

## Product Analytics and A/B Testing Roadmap

A future product analytics layer could evaluate how different dashboard designs affect analyst decision-making.

Potential A/B testing design:

- Version A: risk-score leaderboard and company trend charts only.
- Version B: risk-score leaderboard, evidence snippets, top risk drivers, and recommended analyst actions.

Potential evaluation metrics:

- Time required to identify the highest-priority filing.
- Analyst confidence in the recommendation.
- Accuracy of risk-prioritization decisions.
- Click-through rate on filing-level evidence sections.
- Usage of filters, drill-downs, and ML intelligence panels.

This would extend ClairvoyAI beyond modeling into decision-support product analytics.

---

## Technical Stack

### Data Processing

- Python
- Pandas
- NumPy

### NLP and Feature Engineering

- Keyword-based risk-signal extraction
- Text cleaning and preprocessing
- Risk-driver normalization per 10,000 words
- Rule-based risk scoring

### Database and SQL

- PostgreSQL
- Docker
- pgAdmin
- SQLAlchemy
- psycopg2

### Machine Learning

- scikit-learn
- Logistic Regression
- Random Forest
- Gradient Boosting
- Train/test evaluation
- Feature importance analysis

### Deep Learning

- TensorFlow
- Keras
- Dense neural network classifier
- Softmax multiclass output
- One-hot encoded labels

### Visualization and Dashboarding

- Plotly
- Streamlit
- HTML
- CSS
- JavaScript

### Planned Cloud Architecture

- Amazon S3
- Amazon RDS PostgreSQL
- Amazon EC2 / AWS App Runner
- AWS Lambda
- Amazon CloudWatch
- Amazon SNS

### Project Management

- GitHub
- Reproducible project structure
- Processed analytical outputs

---

## Project Files

Important files planned for this repository:

```text
README.md
index.html
app.py
requirements.txt

Data/processed/sec_filing_risk_scores.csv
Data/processed/sec_filing_agent_results.csv
Data/processed/ml_model_comparison.csv
Data/processed/ml_feature_importance.csv
Data/processed/ml_prediction_detail.csv

models/clairvoyai_nn.keras
src/load_to_postgres.py
notebooks/
reports/charts/
```

Raw SEC filing files, environment files, local database credentials, and cache folders are excluded from GitHub when needed.

---

## Important Limitations

- The current MVP includes only 25 filings.
- The model is not a financial distress prediction model.
- The risk score measures disclosure-language risk intensity, not stock performance, default probability, credit risk, or investment attractiveness.
- TensorFlow/Keras results are experimental and should not be interpreted as production-grade deep learning performance.
- The ML labels are derived from the project’s rule-based scoring framework.
- The AWS layer is currently documented as a planned cloud architecture rather than a fully deployed production system.
- Future work should expand the dataset across more companies, sectors, and filing years.

---

## Future Enhancements

Planned improvements include:

- Expand the dataset from 25 filings to 75–150+ filings.
- Add additional sectors and companies.
- Connect Streamlit directly to PostgreSQL analytical views.
- Extend the planned AWS deployment architecture using S3, Lambda, RDS PostgreSQL, SNS, and CloudWatch.
- Add FinBERT or transformer-based raw-text modeling.
- Add automated SEC filing ingestion.
- Add alerting for newly identified High-risk filings.
- Add model monitoring and versioning.
- Improve dashboard deployment and public demo access.
- Add product analytics and A/B testing to evaluate dashboard decision-support effectiveness.

---

## Portfolio Summary

ClairvoyAI demonstrates a full-cycle applied analytics workflow for financial risk intelligence.

The project combines financial text analytics, structured database design, SQL-based validation, machine learning benchmarking, neural-network experimentation, planned cloud architecture, and executive dashboard design.

It is designed as a portfolio-ready project for roles involving applied analytics, financial data science, risk intelligence, machine learning, and decision-support systems.
