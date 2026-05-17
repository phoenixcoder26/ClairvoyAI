# ClairvoyAI: Agentic SEC Filing Risk Intelligence System

ClairvoyAI is an end-to-end financial risk intelligence project that transforms SEC 10-K Item 1A Risk Factor disclosures into structured risk signals, normalized risk scores, analyst-facing recommendations, machine learning benchmarks, and interactive dashboard outputs.

The project integrates natural language processing, PostgreSQL database design, SQL analytics, classical machine learning, an experimental TensorFlow/Keras neural network, and executive-style dashboarding to demonstrate a complete applied analytics workflow for financial risk intelligence.

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
- Saved ML artifacts and prediction outputs
- Interactive Streamlit dashboard
- Animated HTML dashboard concept for portfolio presentation

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
Streamlit dashboard / animated portfolio page
```

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
```

Raw SEC filing files, environment files, local database credentials, and cache folders are excluded from GitHub when needed.

---

## Important Limitations

- The current MVP includes only 25 filings.
- The model is not a financial distress prediction model.
- The risk score measures disclosure-language risk intensity, not stock performance, default probability, credit risk, or investment attractiveness.
- TensorFlow/Keras results are experimental and should not be interpreted as production-grade deep learning performance.
- The ML labels are derived from the project’s rule-based scoring framework.
- Future work should expand the dataset across more companies, sectors, and filing years.

---

## Future Enhancements

Planned improvements include:

- Expand the dataset from 25 filings to 75–150+ filings
- Add additional sectors and companies
- Connect Streamlit directly to PostgreSQL analytical views
- Add AWS deployment architecture using S3, Lambda, RDS PostgreSQL, SNS, and CloudWatch
- Add FinBERT or transformer-based raw-text modeling
- Add automated SEC filing ingestion
- Add alerting for newly identified High-risk filings
- Add model monitoring and versioning
- Improve dashboard deployment and public demo access

---

## Portfolio Summary

ClairvoyAI demonstrates a full-cycle applied analytics workflow for financial risk intelligence.

The project combines financial text analytics, structured database design, SQL-based validation, machine learning benchmarking, neural-network experimentation, and executive dashboard design.

It is designed as a portfolio-ready project for roles involving applied analytics, financial data science, risk intelligence, machine learning, and decision-support systems.