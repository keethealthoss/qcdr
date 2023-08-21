## Risk Adjustment - Method 3
Using SQL to calculate patients' probability of failure to progress. Follow the same steps in the Risk Adjustment - Method 2. Except in this case, you would load the CSV tables into a SQL DB and then use SQL to generate risk adjusted patient data.

* Download the CSV tables
  * [2019 - Risk Adjustment Tables](../coefficients/2019)
  * [2020 - Risk Adjustment Tables](../coefficients/2020)
  * [2021 - Risk Adjustment Tables](../coefficients/2021)
  * [2022 - Risk Adjustment Tables](../coefficients/2022)
  * [2023 - Risk Adjustment Tables](../coefficients/2023)
* Load the CSV tables into a SQL database
* Query sample patient population
* Query new Risk Adjustment Tables
* Run Prediction

Example SQL statement:

```sql
SELECT DISTINCT
                odi.ID,
                int.`MDQ.prob.mcd` + admit.`MDQ.prob.mcd` + pain.`MDQ.prob.mcd` + age.`MDQ.prob.mcd` + pyr.`MDQ.prob.mcd` +
                sex.`MDQ.prob.mcd` + txtype.`MDQ.prob.mcd` + dur.`MDQ.prob.mcd` AS `Predicted Score`
FROM intercepts AS int,
     `odi.test` AS odi
  LEFT JOIN admit ON odi.ADMIT_SCORE_NO = admit.ADMIT_SCORE_NO
  LEFT JOIN pain ON odi.ADMIT_PAIN_NO = pain.ADMIT_PAIN_NO
  LEFT JOIN age ON odi.AGE = age.`Age.num`
  LEFT JOIN pyr ON odi.pyr2 = pyr.pyr2
  LEFT JOIN sex ON odi.GENDER_DSC = sex.GENDER_DSC
  LEFT JOIN txtype ON odi.`TX_TYPE_CD` = txtype.`TX_TYPE_CD`
  LEFT JOIN dur ON odi.DurCat = dur.DurCat
;
```

[Back Home](../README.md)
