## Risk Adjustment - Method 2
Using the CSV tables to generate risk adjusted patient data.

1. Download ALL CSV files listed in the coefficients subdirectory for a specific reporting year (typically this is the current reporting year).

* [2019 - Risk Adjustment Tables](../coefficients/2019)
* [2020 - Risk Adjustment Tables](../coefficients/2020)
* [2021 - Risk Adjustment Tables](../coefficients/2021)

2. Open each file. You will notice there are 2 columns for each outcome measure, the column labels consist of the name of the outcome measure (MDQ, NECK, KOS, LEFS, or DASH) followed by a period (&quot;.&quot;) and then either &quot;prob.mcd&quot; or &quot;prob.pain&quot;. The &quot;prob.mcd&quot; columns are used to predict failure to progress (achieve a minimal clinically important difference, scale specific to the measure) on the outcome measure scale and the &quot;prob.pain&quot; is used to predict a change in the pain scale of at least 2 points (the MCID for pain).

The first column(s) are used to look up the appropriate row for a specific patient.

The duration is for duration of symptom, the number of days from injury or surgery to admission. Use the row where the patient&#39;s value lies between the &quot;lower&quot; and &quot;upper&quot; values, if the patients number matches exactly then use the row for which they match the &quot;upper&quot; value, e.g. if the duration is 14 days then use the row for 7 to 14 days rather than the 14 to 30-day row. If this value is missing/unknown because the exact date of injury is not known, then use the row with &quot;Missing&quot; in the lower and upper columns. All other tables have a single row for each possible value, use the row that matches.

The &quot;intercepts&quot; table has only 1 row of values, use the value from this row (and the appropriate column) for all patients.

Look up the appropriate value for each patient on each table, you should get 1 number from each table for each patient and sum up these values. Then put the sum into the following formula:

This is the predicted probability for failure to progress for that patient.

3. Set your sample patient population. In this case you can specify a single patient (row) for risk adjustment.
For example, if we have a patient who is a 43 year old Male, admitted with an MDQ score of 48 and a pain score of 7, who has commercial insurance, has 14 days since injury, and conservative treatment, then we would use the following values (these screenshots are for the example, the actual numbers may differ in the tables if the tables have been updated):

  Intercepts:

    ![](/docs/intercepts.png)

  Age:

    ![](/docs/age.png)

  Sex:

    ![](/docs/gender.png)

  Admit Score:

    ![](/docs/admit_score.png)

  Pain Score (at admit):

    ![](/docs/admit_pain.png)

  Payer (Insurance) type:

    ![](/docs/payer.png)

  Duration (days since injury/surgery):

    ![](/docs/duration.png)

  Treatment type:

    ![](/docs/treatment.png)

4. Predict Patient FTP Rate.  So for this example the sum would be:

```
-2.65904 + -1.16585 + 0.063434 + 4.3049793 + -0.1756 + -0.0825 + -0.00981 + 0 = 0.2756133
```

So the final probability for failure to progress for this patient is or 43% chance of failure to progress.

5. Predict Patient FTP Rate for Entire Sample Population. Once you have tested and verified that you can generate predictions, you can now apply the same method to all patients.

6. Assess Performance Rate Difference. Once we have a predicted failure to progress, we can now look at an actual patient population and determine how the predicted, or &quot;adjusted&quot; failure to progress compares to actual failure to progress, both at the individual patient level as well in the aggregate.

Calculate the mean of the predicted probabilities and the mean of the indicators (this second mean is just the proportion who failed to progress). Subtract the mean predicted value from the mean observed value and this is the adjusted value.

```
'Performance Rate Difference' = 'Observed FTP Rate' - 'Predicted FTP Rate'
```

[Back Home](../README.md)
