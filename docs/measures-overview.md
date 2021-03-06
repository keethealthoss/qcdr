## MIPS Submission Schemas

Every year CMS publishes the submission schema for all measures approved by CMS for MIPS. You can access all schemas for all measures for each year by going to the [measures directory](https://github.com/CMSgov/qpp-measures-data/blob/develop/measures/) in the qpp-cms github repo.

The schemas published in this repo are json files that contain only the relevant pieces for submitting IROMS measures to CMS. Each file contains the definitions for all IROMS measures for a given year. All submissions must conform to this specification. Each measure is represented by an **observed and expected (risk adjusted) population**. Both groups are stratified by **Treatment**:

- Conservative,
- Surgical and
- Overall

This results in a total of 6 strata for a single measure.

```
"strata": [
  {
    "name": "notachieving",
    "description": "Overall proportion of patients not achieving an MCID in the NPRS change score will be reported."
  },
  {
    "name": "overall",
    "description": "A risk-adjusted MCID proportional difference will be reported where the difference between the risk model predicted and observed MCID proportion will reported."
  },
  {
    "name": "operativeMCID",
    "description": "The proportion of patients not achieving an MCID in the NPRS change score will be reported."
  },
  {
    "name": "operativeRisk",
    "description": "A risk-adjusted MCID proportional difference will be reported where the difference between the risk model predicted and observed MCID proportion will reported."
  },
  {
    "name": "nonOpMCID",
    "description": "The proportion of patients not achieving an MCID in the NPRS change score will be reported."
  },
  {
    "name": "nonOpRisk",
    "description": "A risk-adjusted MCID proportional difference will be reported where the difference between the risk model predicted and observed MCID proportion will reported."
  }
]
```

For each stratum, tally the population counts for each population category:

```
{
  "measurementId": string,
  "performanceMet": integer,
  "performanceNotMet": integer,
  "eligiblePopulationExclusion": integer,
  "eligiblePopulationException": integer,
  "eligiblePopulation": integer,
  "stratum": string
}
```
See: [Multi-Performance Rate Stratum](https://cmsgov.github.io/qpp-submissions-docs/measurements#stratum) for more information.

Note because the IROMS measures are inverse by design, the "performanceMet" category represents those patients who failed to meet the MCID. Patients who met or exceeded the MCID are counted in "performanceNotMet" category. For more information about submitting measures to CMS, please checkout the [QPP Submission API Docs](https://cmsgov.github.io/qpp-submissions-docs/)


[BACK](../README.md)
