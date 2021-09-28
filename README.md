<img src="docs/keet-logo-color-white.png" height="25"/>  **Keet Outcomes - Qualified Clinical Data Registry (QCDR)**

## Overview
This repo provides access to Keet Outcomes (IROMS) Measures, and the risk adjustment models used in predicting failure to progress (FTP).
The repo also provides the **measures descriptions** and **measures schemas** published by CMS every year since the IROMS measures were approved by CMS. CMS publishes the **measures descriptions** and **measures schemas** every year on the QPP-CMS Github. Keet copies both the definitions and schema for each year and loads them here for ease.

* [Measures Overview](docs/measures-overview.md)
* [Measures Definitions](../measures)
* [Measures Schema](../measures)
* [Risk Adjustment Overview](docs/risk-adjustment.md)

## Getting Started
Keet Outcomes (IROMS) Measures are multi-performance rate measures consisting of both observed and risk adjusted data which are further stratified by Treatment (e.g. 'Conservative' vs. 'Surgical'). The measure definitions define the six strata expected by CMS for each Keet Outcomes measure. All quality data submitted to CMS-QPP MUST include both risk adjusted data along with the observed patient outcomes for the reporting year.

### Risk Adjusting Patient Outcomes Data
There are two ways to use the risk adjustment models. The first approach uses the Excel Workbook. The second approach uses the coefficient tables. We'll walk through using both methods.

### Risk Adjustment - Method 1
Using the Excel Workbook.

1. Download the workbook for the current reporting year.

2. Open the workbook and look at the first sheet named, 'Patient'. This is where you input patient record data.

![](docs/patient_data.png)

The existing data shown here are synthetic data generated for the purpose of example. Each row represents a patient record, and each record consists of of both patient reported outcome measure response (e.g. the survey score), along with supplemntal patient data. There are a set of corresponding spreadsheets that map to predictors of FTP, these include:

* Intercepts
* Age
* Admit Score
* Admit Pain
* Gender
* Payer
* Treatment Type
* Duration

Each sheet of coefficients has 2 columns for each outcome measure, the column labels consist of the name of the outcome measure (MDQ, NECK, KOS, LEFS, or DASH) followed by a period (&quot;.&quot;) and then either &quot;prob.mcd&quot; or &quot;prob.pain&quot;. The &quot;prob.mcd&quot; columns are used to predict failure to progress (achieve a minimal clinically important difference, scale specific to the measure) on the outcome measure scale and the &quot;prob.pain&quot; is used to predict a change in the pain scale of at least 2 points (the MCID for pain).

The first column(s) are used to look up the appropriate row for a specific patient.

The duration is for duration of symptom, the number of days from injury or surgery to admission. Use the row where the patient&#39;s value lies between the &quot;lower&quot; and &quot;upper&quot; values, if the patients number matches exactly then use the row for which they match the &quot;upper&quot; value, e.g. if the duration is 14 days then use the row for 7 to 14 days rather than the 14 to 30-day row. If this value is missing/unknown because the exact date of injury is not known, then use the row with &quot;Missing&quot; in the lower and upper columns.

All other tables have a single row for each possible value, use the row that matches.

3. Next, set the measure in the 'Patient' spreadsheet. There are 10 measure options numbered 2 through 11

![](docs/set_measure.png)

In this example, we set the measure to 2 which maps to the Functional ODI/MDQ measure.

4. Load a sample of patient records. The patients included should have completed at least 1 patient reported outcome measure. Note: you can risk adjust patients who have completed at least 1 PRO, but assessing performance rates requires patients who have completed 2 or more PROs.

5. Predict FTP rate for the sample population. Once the patient data has been inputted and the measure has been set, click enter on the spreadsheet to generate the predicted outcomes. The spreadsheet uses a VLOOKUP to map the patient data to the appropriate coefficient values, and calculate a risk adjusted FTP rate.

6. Calculate Performance Rate Difference. Once we have a predicted failure to progress, we can now look at an actual patient population and determine how the predicted, or &quot;adjusted&quot; failure to progress compares to actual failure to progress, both at the individual patient level as well in the aggregate.

Calculate the mean of the predicted probabilities and the mean of the indicators (this second mean is just the proportion who failed to progress). Subtract the mean predicted value from the mean observed value and this is the adjusted value.

A value of 0 (zero) is neutral and means that the failure to progress rate matched the predicted failure to progress rate exactly, a negative value means that the actual failure to progress rate was lower than predicted, so more patients in that group progressed than predicted. A positive value means that the observed rate was higher than predicted, so more patients failed to progress than would be predicted by their baseline scores. Below is an example group of patients:

![](docs/patient_data.png)

Column B is the predicted values for each patient based on the formula and lookup tables above. Column C just indicates whether each patient failed to progress. For this clinic the predicted failure rate is 0.383 (38.3%) and the actual failure rate is 0.3 (30%) for a difference of -0.083 (-8.3%) meaning that they out performed expectation by 8.3%.
