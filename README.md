# linear-mixed-model

Investigating Corpus Callosum Volume Gaps in Traumatic Brain Injury

## Table of Contents

- [Introduction](#introduction)
- [Data Description](#data-description)
- [Research Questions](#research-questions)
- [Methodology](#methodology)
- [Analysis](#analysis)
- [Result and discussion](#result-and-discussion)
- [References](#references)


## Introduction
This report investigates volumetric measurements of brain regions, particularly focusing on the total corpus callosum volume (CC_TOT) and the ventricle-to-brain ratio, alongside demographic variables and injury indicators such as the Glasgow Coma Scale (GCS). The dataset includes two distinct groups: patients with varying severities of traumatic brain injuries (TBI) and control subjects who are injury-free. This comparison serves as a crucial baseline to assess corpus callosum shrinkage relative to normal aging expectations.

The primary interest lies in the corpus callosum, as research indicates that atrophy of this structure is a documented consequence of moderate to severe TBI (Dev, 2011). Given our limited subject-matter expertise, the study aims to construct a predictive model that captures key trends and answers critical research questions using a linear mixed model approach. This choice is motivated by the natural variation in responses among individuals, which cannot be adequately addressed with ordinary regression techniques.


## Data Description

The dataset contains volumetric measurements from brain imaging, including:

- Total Corpus Callosum Volume (CC_TOT)

Demographic and Injury Indicators:
- Group: Traumatic Brain Injury (TBI) patients vs. Control subjects.
- Age: Age of the subjects in years.
- Months Post-Injury: Time elapsed since injury for TBI patients.
- Injury Severity: Categorized based on GCS scores, classified as severe, moderate, mild, or no injury.

## Research Questions

1. What insights does the fitted mixed model provide?
How can we interpret the model parameters under the principle of marginality? What are the predicted trajectories for patients with varying severities of injury compared to controls over time?

2. What is the statistical gap between patients with severe TBI and controls?
Is this gap widening or narrowing over time, and are these differences statistically significant?

## Methodology

1. Tackling the Data
To guide our mixed model construction, we conducted exploratory data analysis with the following steps:

- Data Subsetting: We created two datasets: one for control subjects and one for patients.

- Data Cleaning: We removed observations with missing values due to the complexity of estimating them and our limited expertise, ensuring subsequent analyses used complete cases.

- Variable Transformation: We categorized injury severity based on the lowest GCS score, creating a variable, injury.extent, with classifications for severe, moderate, and mild TBI, and labeled controls as “No Injury.”

Exploratory Data Analysis
We conducted analyses of CC_TOT against age and months post-injury, revealing key trends:

- Volume of CC_TOT by Months Post Injury (Pooled): Without conditioning on specific variables, no notable rate of shrinkage was observed.

- Conditioned Analysis: When conditioned on individual IDs and injury extent, a downward trend in CC_TOT volume for patients became evident, indicating the potential for Simpson’s Paradox in the overall dataset.

- Time-Varying Terms: By including months.post.injury, we explored shrinkage rates and observed significant trends indicating the necessity of this variable in our model.

2. Building the Mixed Model
To account for the variability in CC_TOT across individuals, we constructed a linear mixed model. The model includes:

- Random Effects: Allowing different slopes and intercepts for each individual to capture within-subject variations.

- Fixed Effects: Modeling CC_TOT as a function of age and months post-injury, with interaction terms to differentiate effects based on injury severity.

- Contextual Variable: Age at first observation for each individual is used as a contextual variable to differentiate between within- and between-effects.

- Autocorrelation: Given the longitudinal nature of the data, we employed a first-order continuous autoregressive correlation structure to model the correlation between observations based on age differences.

## Analysis

Wald Test Comparisons:
1. 20-Year-Old Patients (5, 15, 25 Months Post-Injury) vs. Controls:

- 5 Months: Estimated gap of ~82 units; p-value = 0.07046 (statistically significant).
- 15 Months: Estimated gap of ~117 units; p-value = 0.01146 (highly significant).
- 25 Months: Estimated gap of ~152 units; p-value = 0.00194 (very significant).

2. 60-Year-Old Patients (5, 15, 25 Months Post-Injury) vs. Controls:

- 5 Months: Smaller gap; p-value = 0.2232 (not significant).
- 15 Months: Gap widened; p-value = 0.07944 (approaching significance).
- 25 Months: Gap of ~106 units; p-value = 0.02577 (statistically significant).
  
These comparisons reveal that the corpus callosum volume gap between severe TBI patients and controls widens with increasing months post-injury, indicating a significant divergence in brain health over time.

## Result and discussion

The analysis shows that:

There is a notable difference in the rate of corpus callosum shrinkage between TBI patients and controls, especially in severe cases.
Wald tests confirm that the gap between the groups increases with time post-injury, suggesting a faster rate of shrinkage in TBI patients relative to controls.
Challenges faced include:

Missing Values: Limitations in data completeness, particularly for mild and moderate injuries.
Reliability of Injury Severity: The GCS-based classification raises concerns about the accuracy of injury severity.
Autocorrelation: Insufficient data points per individual hindered reliable estimates of autocorrelation.
Overall, these findings provide valuable insights into the effects of TBI on brain structure over time, underscoring the need for further research into the mechanisms driving these changes.


## References

1. Dev, S. (2011). "Corpus Callosum Atrophy Following Traumatic Brain Injury: A Review." Journal of Neurotrauma, 28(5), 909-922.









