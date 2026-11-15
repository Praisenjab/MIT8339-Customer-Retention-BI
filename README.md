# Customer Attrition & Retention Intelligence | Power BI

**MIT 8339 - Business Intelligence and Decision Support Systems (Virtual Lab)**  
**MIVA Open University | Coursework demonstration**

A two-page Power BI decision-support report examining credit-card customer attrition, transactional activity, product depth, inactivity and rule-based retention-priority groups. The brief frames a **hypothetical Nigerian retail bank**; the underlying BankChurners dataset is a public demonstration dataset and **must not be interpreted as Nigerian banking data**.


## Open in Power BI

1. Download the 'pbix' file and open it in Power BI Desktop.
2. Use **Transform Data → Data source settings** to update the source CSV path if necessary; refresh.
3. Check that the headline cards show 10,127 total customers, 1,627 attrited, and 16.07% attrition with all slicers reset.
4. Verify both report pages, slicer interactions, the age-band sort and red top-rate highlighting.

## Risk score: correct interpretation

The supplied risk score (0–4) can be exactly reproduced using one point each for: (i) at least four inactive months, (ii) at most 41 annual transactions, (iii) at most two product relationships, and (iv) a Q4/Q1 transaction-count change ratio below one. The observed within-sample attrition rates are 69.87% (High), 20.67% (Medium) and 9.37% (Low). **These are not out-of-sample churn predictions.**

The threshold of 41 corresponds to the 25th percentile across **distinct transaction-count values** (41.25); the customer-weighted 25th percentile is **45**. This difference should be understood before calling the condition a customer-quartile rule.

## Management use and limitations

The recommendations are to pilot intervention among the **135 existing high-risk customers**, monitor inactivity and falling transaction engagement, investigate shallow product relationships, review customer service-contact causes, and balance segment rates against portfolio volumes. Prioritisation is an analytical hypothesis. Treatment effects must be tested and costs measured before operational claims are made.

The source data have no authenticated Nigerian geographic context, no individual attrition-event dates, no treatment outcomes, and no causal evidence. Privacy, consent, demographic fairness and access controls must be addressed before deploying a similar workflow on real banking data.


## Data provenance and licence

Goyal, S. (n.d.). *Credit Card customers* [Data set]. Kaggle. https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers

The dataset page lists **CC0: Public Domain**. The dataset is redistributed here for reproducibility; verify any changed upstream terms before further redistribution. Student project analyses and code are distinct from source-data licensing. This repository is not an official MIVA publication or bank product.

## Notes on public disclosure

The public screenshot versions and public `.pbix` layout have student-identifying header text removed. Review `.pbix` file properties, data-source connection paths, annotations and exported files **locally before pushing**; some embedded model metadata cannot be comprehensively audited without opening Power BI Desktop. Keep the identity-bearing final assessment PDF outside the public repo.
