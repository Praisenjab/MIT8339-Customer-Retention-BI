# Customer Attrition & Retention Intelligence | Power BI

**MIT 8339 - Business Intelligence and Decision Support Systems (Virtual Lab)**  
**MIVA Open University | Coursework demonstration**

A two-page Power BI decision-support report examining credit-card customer attrition, transactional activity, product depth, inactivity and rule-based retention-priority groups. The brief frames a **hypothetical Nigerian retail bank**; the underlying BankChurners dataset is a public demonstration dataset and **must not be interpreted as Nigerian banking data**.

> **Repo description for GitHub:** `Power BI banking customer attrition dashboard with verified KPIs, behavioural segmentation, rule-based retention risk, and evidence-led interventions.`

## Dashboard preview

### Executive Overview
![Executive dashboard](screenshots/Executive_Overview_Public.png)

### Retention Analysis
![Retention analysis](screenshots/Retention_Analysis_Public.png)

## Key findings (unfiltered sample)

| Metric | Verified result |
|---|---:|
| Customer records | 10,127 |
| Attrited customers | 1,627 |
| Existing customers | 8,500 |
| Observed attrition rate | **16.07%** |
| Mean annual transaction count | 64.86 |
| Mean annual transaction amount | 4,404.09 (source monetary units) |
| Mean credit utilisation | 27.49% |
| 4+ months inactive: attrition rate | **24.56%** (181/737) |
| 0–1 months inactive: attrition rate | 5.08% (115/2,262) |
| 2 products: attrition rate | **27.84%** (346/1,243) |
| 4+ products: attrition rate | 11.43% (648/5,669) |
| Existing customers in High Risk band | **135** |

The **Platinum** card tier has a 25.00% observed attrition rate, but this is only **5 of 20 customers**. By absolute count, **Blue** accounts for 1,519 of 1,627 attritions. Avoid prioritising solely by a small-segment percentage.

## Contents

```text
.
├── dashboard/
│   └── MIT_8339_CA_Public_Redacted.pbix
├── screenshots/
│   ├── Executive_Overview_Public.png
│   ├── Retention_Analysis_Public.png
│   └── Power_Query_Applied_Steps.png
├── data/
│   ├── BankChurners_cleaned_public.csv
│   ├── segment_summary.csv
│   ├── behaviour_comparison.csv
│   └── quality_audit.csv
├── code/
│   ├── reproduce_clean_dataset.py
│   ├── DAX_Reconstructed_Reference.dax
│   └── POWER_QUERY_NOTES.md
├── report/
│   ├── analytical_report.md
│   ├── MIT8339_Analytical_Report_Public.docx
│   └── MIT8339_Analytical_Report_Public.pdf
├── presentation/
│   ├── MIT8339_Five_Minute_Presentation.pptx
│   └── Speaker_Notes.md
└── docs/
    ├── assessment_requirements.md
    ├── data_quality_and_model_review.md
    └── public_release_checklist.md
```

## Reproduce the data preparation

1. Install **Python 3.10+**, `pandas` and `numpy` (`pip install pandas numpy`).
2. Download the original dataset from [Kaggle - Credit Card customers](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers) or use the included exported data.
3. From the repository root, run:

```bash
python code/reproduce_clean_dataset.py --input data/BankChurners_cleaned_public.csv --out data/BankChurners_rebuilt.csv
```

The script validates labels and identifiers, removes two unused precomputed classifier columns, rebuilds six analytical fields and reproduces the current risk scores. It will reject a version with unexpected customer totals rather than silently altering the findings.

**Important reproducibility caveat:** this Python script and `DAX_Reconstructed_Reference.dax` are *reconstructed equivalents*, not exact code extracted from the PBIX. The attached Power Query screenshot shows only `Source`, `Promoted Headers` and `Changed Type`. To document the actual Power BI code, export the original Advanced Editor M script and all DAX definitions from Power BI Desktop (steps in `code/POWER_QUERY_NOTES.md`).

## Open in Power BI

1. Download `dashboard/MIT_8339_CA_Public_Redacted.pbix` and open it in Power BI Desktop.
2. Use **Transform Data → Data source settings** to update the source CSV path if necessary; refresh.
3. Check that the headline cards show 10,127 total customers, 1,627 attrited, and 16.07% attrition with all slicers reset.
4. Verify both report pages, slicer interactions, the age-band sort and red top-rate highlighting.

The public `.pbix` was modified only to replace student name/ID text within the report layout. Its ZIP structure was checked, **but the modified file has not been reopened and validated in Power BI Desktop**. You should open and save it yourself before publishing. The dashboard contains one extra placeholder page; remove it in Desktop if not needed.

## Risk score: correct interpretation

The supplied risk score (0–4) can be exactly reproduced using one point each for: (i) at least four inactive months, (ii) at most 41 annual transactions, (iii) at most two product relationships, and (iv) a Q4/Q1 transaction-count change ratio below one. The observed within-sample attrition rates are 69.87% (High), 20.67% (Medium) and 9.37% (Low). **These are not out-of-sample churn predictions.**

The threshold of 41 corresponds to the 25th percentile across **distinct transaction-count values** (41.25); the customer-weighted 25th percentile is **45**. This difference should be understood before calling the condition a customer-quartile rule.

## Management use and limitations

The recommendations are to pilot intervention among the **135 existing high-risk customers**, monitor inactivity and falling transaction engagement, investigate shallow product relationships, review customer service-contact causes, and balance segment rates against portfolio volumes. Prioritisation is an analytical hypothesis. Treatment effects must be tested and costs measured before operational claims are made.

The source data have no authenticated Nigerian geographic context, no individual attrition-event dates, no treatment outcomes, and no causal evidence. Privacy, consent, demographic fairness and access controls must be addressed before deploying a similar workflow on real banking data.

## Assignment evidence and remaining author actions

See `docs/assessment_requirements.md` for the official 40-mark checklist. This repo includes two report screenshots, Power Query step evidence, analytical report, reconstructed code, cleaned export, data audit and a five-minute slide deck. **Still to supply from Power BI:** the exact original M script, the exact full DAX definitions, and screenshots of measure/formula execution if requested. **Still to record:** the five-minute audiovisual narration; the slide deck is not itself a narrated audiovisual file. The assessment requires a master PDF as the formal submission, potentially supplemented by support files/links according to lecturer/LMS instructions.

## Data provenance and licence

Goyal, S. (n.d.). *Credit Card customers* [Data set]. Kaggle. https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers

The dataset page lists **CC0: Public Domain**. The dataset is redistributed here for reproducibility; verify any changed upstream terms before further redistribution. Student project analyses and code are distinct from source-data licensing. This repository is not an official MIVA publication or bank product.

## Notes on public disclosure

The public screenshot versions and public `.pbix` layout have student-identifying header text removed. Review `.pbix` file properties, data-source connection paths, annotations and exported files **locally before pushing**; some embedded model metadata cannot be comprehensively audited without opening Power BI Desktop. Keep the identity-bearing final assessment PDF outside the public repo.
