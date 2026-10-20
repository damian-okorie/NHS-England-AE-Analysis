# NHS England A&E Analysis

Exploratory and statistical analysis of 600,000 accident and emergency attendances, written in R.

## The data

NHS England A&E synthetic dataset. 600,000 records sampled from the full file, covering 23 March 2014 to 22 March 2018 across 238 providers.

Eighteen fields, including index of multiple deprivation decile, age band, sex, arrival date, arrival hour band, time in department, counts of diagnoses, investigations and treatments, arrival mode, distance from patient to provider, and whether the attendance ended in admission.

The data is synthetic. The patterns are realistic but no record describes a real patient.

## Questions

How long do people spend in A&E, and how much does that vary?

When do people arrive, by hour band, day of week and month?

Which age groups attend most?

Does the way someone arrives predict whether they are admitted?

Do counts of diagnoses, investigations and treatments move together?

## Preparation

Arrival hour recoded from text bands to ordered numeric values.

Median imputation for deprivation decile, arrival hour and distance to provider.

An explicit Unknown category for missing sex, and a nothing category for missing HRG.

Modal imputation for the admission flag.

Four fields dropped for severe missingness. Length of stay was absent on 481,584 of 600,000 rows.

Outliers identified using the interquartile range method.

## What the data shows

Mean time in department is 164.9 minutes, median 140, standard deviation 139.0, maximum 1,440. The distribution is right skewed, so a minority of long stays pull the mean above the median.

The 25 to 44 age band attends most, at 148,625 attendances, followed by 1 to 17 at 126,713. The 85 plus band attends least, at 49,093.

Arrivals peak between 9am and noon, at 163,749, and fall to their lowest between 1am and 4am, at 42,399.

Saturday is the busiest day of the week and Wednesday the quietest.

Arrival mode is strongly associated with admission. Chi-squared is 100,499 on 2 degrees of freedom, with p below 2.2e-16. Admission rates range from roughly 12 per cent for one arrival mode to roughly 50 per cent for another.

Investigations and treatments correlate at 0.45. Diagnoses correlate only weakly with either, at 0.12 and 0.17.

The period averages 411 attendances per day.

## Limitations

The sample is drawn without a fixed seed, so re-running the script produces a different 600,000 rows and the figures shift slightly.

Outlying values of time in department were replaced with the median. This flattens the right tail that the analysis itself identifies as meaningful, and the histogram after replacement should be read with that in mind.

Because the data is synthetic, nothing here is a clinical or operational finding about a real hospital. The purpose is to demonstrate method.

## Files

AE_Analysis.Rmd is the source.

AE_Analysis.md is the rendered output and is the one to read.

## Tools

R, tidyverse, dplyr, ggplot2, lubridate, data.table.
