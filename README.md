<img src="docs/keet-logo-color-white.png" height="25"/>  

## Keet Outcomes - Qualified Clinical Data Registry (QCDR)
This repo provides access to Keet Outcomes (IROMS) Measures, and the risk adjustment models used in predicting failure to progress (FTP).

## Getting Started
Keet Outcomes (IROMS) Measures are multi-performance rate measures consisting of both observed and risk adjusted data which are further stratified by Treatment (e.g. 'Conservative' vs. 'Surgical'). The [measure definitions](docs/measures-overview.md) define the six strata expected by CMS for each Keet Outcomes measure. **All quality data submitted to CMS-QPP MUST include both risk adjusted data along with the observed patient outcomes for the reporting period**.

### Risk Adjusting Patient Outcomes Data
There are several ways to use the risk adjustment models. The first approach uses an Excel Workbook. The second approach uses the set of CSV (coefficients) tables. A third approach uses SQL. We'll walk through using all three methods.

* [Risk Adjustment - Method 1 - Excel Workbook](docs/risk-adjustment-workbook-example.md)
* [Risk Adjustment - Method 2 - CSV Tables](docs/risk-adjustment-csv-example.md)
* [Risk Adjustment - Method 3 - SQL Example](docs/risk-adjustment-sql-example.md)

### Preparing Data for Submission
The repo also provides the **measures descriptions** and **measures schemas** published by CMS every year since the IROMS measures were approved by CMS. CMS publishes the **measures descriptions** and **measures schemas** every year on the QPP-CMS Github. Keet copies both the definitions and schema for each year and loads them here for ease.

* [Measures Overview](docs/measures-overview.md)
* [Measures Definitions/Schemas](measures)
