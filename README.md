# Project-2 - Startup Investments
## 1. Problem Statement ##
When managing a finite $10M seed-stage fund, relying on gut instinct often leads to capital stagnation in portfolio companies that burn through initial cash without securing follow-on rounds. This project leverages historical venture capital data to engineer operational velocity metrics and uncover the financial, sector, and geographic markers that predict long-term startup viability and successful Series A graduation.

---

## 2. Executive Summary ##
This project analyzes historical startup investment trajectories to transition a venture capital firm’s deployment strategy from subjective intuition to data-driven intelligence. The analytical process involved deep programmatic cleaning of unparsed funding metrics, cross-pillar alignment of fragmented capital records, and the engineering of time-delta velocity features (such as the exact chronological gap between company founding and initial institutional backing). By isolating a dedicated cohort of seed-funded startups, we mapped the core operational friction points that cause early-stage businesses to stall out.

The analysis yielded several critical, counterintuitive findings. First, an ultra-rapid jump to initial seed funding is a statistical trap; failed startups historically secure checks faster than their long-term surviving peers, indicating that premature capitalization often precedes poor structural alignment. Second, there is a clear financial "sweet spot" for seed rounds where standard and mid-tier checks (500k–5M dollars) optimize a startup's runway-to-graduation ratio far better than hyper-fractionalized micro-checks. Finally, market congestion frequently masks low realization ceilings, as some of the most heavily crowded industry sectors suffer from dismal acquisition or IPO exit rates.

Based on these insights, it is recommended that the fund avoid chasing immediate post-incorporation rounds and instead enforce a "maturity mask," evaluating teams that have bootstrapped for roughly 1.3 to 1.5 years. The finite $10M capital should be concentrated into 7 to 8 high-conviction checks within the identified capitalization sweet spot rather than being over-diversified across dozens of micro-seed tranches. Furthermore, capital allocation should prioritize sectors with proven exit momentum and actively hedge portfolio risk across international ecosystems like USA and Germany, which demonstrate superior structural advancement rates.

---

## 3. File Directory
| Directory / File | Description |
|:---|:---|
| `Projects/Project-2/README.md` | Core overview document outlining the problem statement, investment takeaways, data framework, and recommendations. |
| `Projects/Project-2/4.project 2/DSB-FT-EDA Project/Startup Investments/startup_investments.csv` | Project folder containing the raw source files dataset. |
| `Projects/Project-2/4.project 2/cleaned_startup_investments.csv` |the cleaned baseline dataset. |
| `Projects/Project-2/4.project 2/seed_cleaned_startup.csv` | the cleaned isolated seed startup dataset. |
| `Projects/Project-2/4.project 2/EDA_Report_Template.ipynb` | A fully documented, step-by-step Jupyter Notebook detailing the data ingestion, cleaning , and visual analysis (EDA). |
| `Projects/Project-2/4.project 2/Startup_Investments_EDA_Presentation.pdf` | A clean, high-impact PDF slide deck built to present these findings directly to non-technical investment partners. |

---

## 4. Data & Data Dictionary
Our data comes directly from historical startup ecosystem ledgers that track global funding milestones and company operational lifecycles. The dictionary below contains the final clean schema and custom metrics engineered specifically to solve our $10M fund allocation problem.

| Feature / Column | Data Type | Source | Description |
|:---|:---|:---|:---|
| name | String| Original | The official operating name of the startup entity. Filled with 'Unknown Startup' where missing. |
| status | String | Original | The current operational state of the company (`operating`, `acquired`, `closed`, `ipo`). Serves as a target variable. |
| market | String | Original | The primary industry vertical or market sector classification. Crucial for sector performance evaluation. |
| category_list | String | Original | A pipe-separated string containing multiple associated sub-industry tags for the company. |
| country_code | String | Original | Three-letter ISO country code representing corporate headquarters location. Missing entries imputed as 'Unknown'. |
| state_code | String | Original | Two-letter state identifier code for US-based companies. Non-US or missing entries imputed as 'Non-US/Unknown'. |
| region | String | Original | Metropolitan region location metadata where the company operates. Missing entries imputed as 'Unknown'. |
| funding_total_usd | Float64 | Original / Imputed | Total aggregate funding raised across all lifecycle stages in USD. Missing values backfilled using row-wise round sums. |
| funding_rounds | Float64 | Original | The absolute count of independent investment rounds logged by the company. |
| founded_at | Datetime64 | Original | The official timestamp denoting when the company was incorporated or founded. |
| first_funding_at | Datetime64 | Original | The timestamp highlighting the company's first recorded institutional check or capital injection. |
| last_funding_at | Datetime64 | Original | The timestamp tracking the company's most recent funding milestone. |
| seed | Float64 | Original | Total capital secured specifically during early-stage seed rounds in USD. Used to filter our primary analytical cohort. |
| venture | Float64 | Original | Total institutional venture capital funding captured over the company's lifecycle in USD. |
| angel | Float64 | Original | Total angel investment funding raised from high-net-worth individuals in USD. |
| round_A | Float64 | Original | Total capital secured during the Series A institutional round in USD. |
| round_B | Float64 | Original | Total capital secured during the Series B institutional round in USD. |
| round_C | Float64 | Original | Total capital secured during the Series C institutional round in USD. |
| days_to_first_check | Float64 | Imputed | Total calendar days elapsed from company founding to its first funding event (first_funding_at - founded_at). Used to measure early velocity. |
| time_between_rounds | Float64 | Imputed | Total calendar days elapsed between the first and last recorded funding rounds (last_funding_at - first_funding_at). Used to evaluate momentum. |
| seed_bin | Category | Imputed | Capitalization tiers binned using pd.cut() (Micro (<500k dollars), Standard (500k-1.5M dollars), Mid-Tier (1.5M-5M dollars), Mega (>5M dollars). |
| raised_round_a | Bool | Imputed | Boolean success flag indicating whether the startup successfully graduated to capture follow-on Round A funding (True / False). |

---

## 5. Conclusions & Recommendations
*   **Enforce a Maturity Buffer:** Stop chasing teams trying to raise capital within months of incorporation. Focus on startups that have successfully operated or bootstrapped for roughly 1.3 to 1.5 years (~500 days), as they exhibit structurally better survival patterns.
*   **Avoid Micro-Check Fragmentation:** Do not dilute our finite 10M dollars pool into dozens of tiny 200k dollar checks. Write 7 to 8 high-conviction checks in the Standard/Mid-Tier capital window (500k–5M dollars) to ensure our companies have enough actual runway to achieve major scale milestones.
*   **Filter Out Market Hype:** Ignore sector density and media noise alone. Use our historical exit rate rankings to actively target market sectors with clear, proven corporate acquisition pipelines rather than sectors that are simply crowded with seed-stage noise.
*   **Look Beyond Domestic Borders:** Build geographic resilience into our portfolio by expanding our deal pipeline internationally. Allocating capital toward top-performing global ecosystems like Israel and Germany allows us to leverage regions with superior baseline Series A graduation rates.

---

## 6. Areas for Further Research/Study
*   **Tracking Non-Dilutive Lifelines:** Future updates should ingest non-equity funding channels—like small business innovation research (SBIR) grants, venture debt, or revenue-based financing—to evaluate if alternative cash injections help underfunded micro-seed companies survive longer.
*   **Uncovering Silent Portfolio Mortality:** A valuable next step involves scraping state business registries to identify startups that simply went dark without ever filing an official "closed" status, helping us completely eliminate any remaining survival bias in our active data.

---

## 7. Important Visualizations
### 7.1. Funding Velocity Analysis (Boxplot)
This plot tracks the number of days from a company's founding to its first check, broken out by final market outcomes. It visualizes our core velocity insight: closed companies often raise their first round faster than companies that go on to achieve long-term operations or strategic acquisitions.

### 7.2. Series A Graduation Window (Bar Chart)
This chart displays the percentage of seed startups that successfully scale to a Series A across distinct check-size categories. It serves as the foundation for our fund sizing model, demonstrating exactly where early capital injections yield the highest graduation rate before hitting diminishing returns.


---

## 8. Sources
*   *Startup Investment Ecosystem Transaction Ledgers (Historical Cohort Data).*
*   *Venture Capital Executive Portfolio Evaluation Frameworks for Seed-to-Scale Asset Classes.*
*   * *Source 1: startup_investments.csv
* *Source 2: cleaned_startup_investments.csv
* *Source 3: seed_cleaned_startup.csv
## 8. Sources
* **Primary Dataset:** Historical Startup Investments (`startup_investments.csv`) provided for the EDA project..
* **Python Libararies:** Python Data Science Stack (`pandas`,`seaborn`, `matplotlib`) utilized for data engineering and exploratory visualization.