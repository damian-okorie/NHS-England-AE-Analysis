``` r
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

``` r
##Package Installation

# Before we can begin the analysis, we first need to ensure that we have all the necessary R packages installed. 
# These packages contain tools and functions that we'll use throughout the analysis.

# Here's a list of the packages we'll be using:
# - tidyverse: a collection of packages for data manipulation and visualization
# - data.table: provides high-performance versions of base R functions, like `rep` and `cbind`
# - caret: short for _Classification And REgression Training_, caret is a set of functions that attempt to streamline the process for creating predictive models
# - lubridate: makes dealing with dates a little easier
# - shiny: makes it easy to build interactive web applications straight from R
# - rmarkdown: dynamic report generation in R
# - knitr: provides a general-purpose tool for dynamic report generation in R
# - randomForest: Breiman and Cutler's random forests for classification and regression
# - e1071: functions for latent class analysis, short time Fourier transform, fuzzy clustering, support vector machines, shortest path computation, bagged clustering, naive Bayes classifier etc.
# - ggplot2: creates elegant data visualisations using the Grammar of Graphics
# - RODBC: an ODBC database interface

# The lapply function applies the install.packages function to each element of the packages vector. 
# In other words, it installs each package one by one.
```

``` r
# Load the libraries
libraries <- c("tidyverse", "data.table", "caret", "lubridate", "shiny", "rmarkdown", "knitr", "randomForest", "dplyr", "ggplot2", "RODBC")
lapply(libraries, library, character.only = TRUE)
```

    ## Warning: package 'tidyverse' was built under R version 4.3.1

    ## Warning: package 'ggplot2' was built under R version 4.3.1

    ## Warning: package 'lubridate' was built under R version 4.3.1

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.2     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.1     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

    ## Warning: package 'data.table' was built under R version 4.3.1

    ## 
    ## Attaching package: 'data.table'
    ## 
    ## The following objects are masked from 'package:lubridate':
    ## 
    ##     hour, isoweek, mday, minute, month, quarter, second, wday, week,
    ##     yday, year
    ## 
    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     between, first, last
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     transpose

    ## Warning: package 'caret' was built under R version 4.3.1

    ## Loading required package: lattice
    ## 
    ## Attaching package: 'caret'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     lift

    ## Warning: package 'shiny' was built under R version 4.3.1

    ## Warning: package 'rmarkdown' was built under R version 4.3.1

    ## Warning: package 'randomForest' was built under R version 4.3.1

    ## randomForest 4.7-1.1
    ## Type rfNews() to see new features/changes/bug fixes.
    ## 
    ## Attaching package: 'randomForest'
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine
    ## 
    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     margin

    ## Warning: package 'RODBC' was built under R version 4.3.1

    ## [[1]]
    ##  [1] "lubridate" "forcats"   "stringr"   "dplyr"     "purrr"     "readr"    
    ##  [7] "tidyr"     "tibble"    "ggplot2"   "tidyverse" "stats"     "graphics" 
    ## [13] "grDevices" "utils"     "datasets"  "methods"   "base"     
    ## 
    ## [[2]]
    ##  [1] "data.table" "lubridate"  "forcats"    "stringr"    "dplyr"     
    ##  [6] "purrr"      "readr"      "tidyr"      "tibble"     "ggplot2"   
    ## [11] "tidyverse"  "stats"      "graphics"   "grDevices"  "utils"     
    ## [16] "datasets"   "methods"    "base"      
    ## 
    ## [[3]]
    ##  [1] "caret"      "lattice"    "data.table" "lubridate"  "forcats"   
    ##  [6] "stringr"    "dplyr"      "purrr"      "readr"      "tidyr"     
    ## [11] "tibble"     "ggplot2"    "tidyverse"  "stats"      "graphics"  
    ## [16] "grDevices"  "utils"      "datasets"   "methods"    "base"      
    ## 
    ## [[4]]
    ##  [1] "caret"      "lattice"    "data.table" "lubridate"  "forcats"   
    ##  [6] "stringr"    "dplyr"      "purrr"      "readr"      "tidyr"     
    ## [11] "tibble"     "ggplot2"    "tidyverse"  "stats"      "graphics"  
    ## [16] "grDevices"  "utils"      "datasets"   "methods"    "base"      
    ## 
    ## [[5]]
    ##  [1] "shiny"      "caret"      "lattice"    "data.table" "lubridate" 
    ##  [6] "forcats"    "stringr"    "dplyr"      "purrr"      "readr"     
    ## [11] "tidyr"      "tibble"     "ggplot2"    "tidyverse"  "stats"     
    ## [16] "graphics"   "grDevices"  "utils"      "datasets"   "methods"   
    ## [21] "base"      
    ## 
    ## [[6]]
    ##  [1] "rmarkdown"  "shiny"      "caret"      "lattice"    "data.table"
    ##  [6] "lubridate"  "forcats"    "stringr"    "dplyr"      "purrr"     
    ## [11] "readr"      "tidyr"      "tibble"     "ggplot2"    "tidyverse" 
    ## [16] "stats"      "graphics"   "grDevices"  "utils"      "datasets"  
    ## [21] "methods"    "base"      
    ## 
    ## [[7]]
    ##  [1] "knitr"      "rmarkdown"  "shiny"      "caret"      "lattice"   
    ##  [6] "data.table" "lubridate"  "forcats"    "stringr"    "dplyr"     
    ## [11] "purrr"      "readr"      "tidyr"      "tibble"     "ggplot2"   
    ## [16] "tidyverse"  "stats"      "graphics"   "grDevices"  "utils"     
    ## [21] "datasets"   "methods"    "base"      
    ## 
    ## [[8]]
    ##  [1] "randomForest" "knitr"        "rmarkdown"    "shiny"        "caret"       
    ##  [6] "lattice"      "data.table"   "lubridate"    "forcats"      "stringr"     
    ## [11] "dplyr"        "purrr"        "readr"        "tidyr"        "tibble"      
    ## [16] "ggplot2"      "tidyverse"    "stats"        "graphics"     "grDevices"   
    ## [21] "utils"        "datasets"     "methods"      "base"        
    ## 
    ## [[9]]
    ##  [1] "randomForest" "knitr"        "rmarkdown"    "shiny"        "caret"       
    ##  [6] "lattice"      "data.table"   "lubridate"    "forcats"      "stringr"     
    ## [11] "dplyr"        "purrr"        "readr"        "tidyr"        "tibble"      
    ## [16] "ggplot2"      "tidyverse"    "stats"        "graphics"     "grDevices"   
    ## [21] "utils"        "datasets"     "methods"      "base"        
    ## 
    ## [[10]]
    ##  [1] "randomForest" "knitr"        "rmarkdown"    "shiny"        "caret"       
    ##  [6] "lattice"      "data.table"   "lubridate"    "forcats"      "stringr"     
    ## [11] "dplyr"        "purrr"        "readr"        "tidyr"        "tibble"      
    ## [16] "ggplot2"      "tidyverse"    "stats"        "graphics"     "grDevices"   
    ## [21] "utils"        "datasets"     "methods"      "base"        
    ## 
    ## [[11]]
    ##  [1] "RODBC"        "randomForest" "knitr"        "rmarkdown"    "shiny"       
    ##  [6] "caret"        "lattice"      "data.table"   "lubridate"    "forcats"     
    ## [11] "stringr"      "dplyr"        "purrr"        "readr"        "tidyr"       
    ## [16] "tibble"       "ggplot2"      "tidyverse"    "stats"        "graphics"    
    ## [21] "grDevices"    "utils"        "datasets"     "methods"      "base"

\##Loading the Dataset(CSV File) into R Environment and saving it as a
Dataframe

In this step, we’re using the read_csv() function from the readr package
to load our dataset, which is stored as a CSV file on the local machine.
The path to the file is provided as a string argument to this function.
At this point, the data is stored in the R environment as a data frame,
which we can manipulate and analyze using other functions. This is the
first step of our analysis because we need to load the data before we
can do anything else with it.

``` r
#Read the CSV file
df <- read_csv("C:/Users/damia/OneDrive/Desktop/A&E+Synthetic+Data/A&E Synthetic Data.csv", show_col_types = FALSE)
```

\##Data Sampling and Inspection

In these steps, we are subsetting the original dataset by randomly
selecting 600,000 rows using the sample_n() function from the dplyr
package. This is useful when working with large datasets, as working
with a smaller subset of data can be computationally less intensive and
speed up the analysis.

The head() function is then used to print the first few rows (by
default, 6 rows) of the new data frame. This allows us to inspect the
subsetted data and ensure the sampling process was successful.

``` r
##Data Sampling and Inspection

# Randomly select 600,000 rows
subset_df <- df %>% sample_n(600000)

# Check the first few rows of your new dataframe
print(head(subset_df))
```

    ## # A tibble: 6 × 18
    ##   IMD_Decile_From_LSOA Age_Band   Sex AE_Arrive_Date      AE_Arrive_HourOfDay
    ##                  <dbl> <chr>    <dbl> <dttm>              <chr>              
    ## 1                    1 65-84        2 2014-06-06 00:00:00 09-12              
    ## 2                    7 25-44        2 2016-09-23 00:00:00 17-20              
    ## 3                    4 18-24        1 2017-09-10 00:00:00 13-16              
    ## 4                    6 1-17         2 2015-12-20 00:00:00 17-20              
    ## 5                    6 45-64        1 2017-03-29 00:00:00 01-04              
    ## 6                    1 65-84        2 2014-09-04 00:00:00 13-16              
    ## # ℹ 13 more variables: AE_Time_Mins <dbl>, AE_HRG <chr>,
    ## #   AE_Num_Diagnoses <dbl>, AE_Num_Investigations <dbl>,
    ## #   AE_Num_Treatments <dbl>, AE_Arrival_Mode <dbl>,
    ## #   Provider_Patient_Distance_Miles <dbl>, ProvID <dbl>, Admitted_Flag <dbl>,
    ## #   Admission_Method <chr>, ICD10_Chapter_Code <chr>,
    ## #   Treatment_Function_Code <chr>, Length_Of_Stay_Days <dbl>

``` r
# Print the column names
print(colnames(subset_df))
```

    ##  [1] "IMD_Decile_From_LSOA"            "Age_Band"                       
    ##  [3] "Sex"                             "AE_Arrive_Date"                 
    ##  [5] "AE_Arrive_HourOfDay"             "AE_Time_Mins"                   
    ##  [7] "AE_HRG"                          "AE_Num_Diagnoses"               
    ##  [9] "AE_Num_Investigations"           "AE_Num_Treatments"              
    ## [11] "AE_Arrival_Mode"                 "Provider_Patient_Distance_Miles"
    ## [13] "ProvID"                          "Admitted_Flag"                  
    ## [15] "Admission_Method"                "ICD10_Chapter_Code"             
    ## [17] "Treatment_Function_Code"         "Length_Of_Stay_Days"

``` r
## Familiarizing the names of the columns.
```

``` r
# Generate summary statistics for each column in the subset_df dataframe
summary(subset_df)
```

    ##  IMD_Decile_From_LSOA   Age_Band              Sex       
    ##  Min.   : 1.000       Length:600000      Min.   :1.000  
    ##  1st Qu.: 2.000       Class :character   1st Qu.:1.000  
    ##  Median : 5.000       Mode  :character   Median :2.000  
    ##  Mean   : 4.862                          Mean   :1.506  
    ##  3rd Qu.: 7.000                          3rd Qu.:2.000  
    ##  Max.   :10.000                          Max.   :2.000  
    ##  NA's   :589                             NA's   :1068   
    ##  AE_Arrive_Date                   AE_Arrive_HourOfDay  AE_Time_Mins   
    ##  Min.   :2014-03-23 00:00:00.00   Length:600000       Min.   :   0.0  
    ##  1st Qu.:2015-04-10 00:00:00.00   Class :character    1st Qu.:  70.0  
    ##  Median :2016-04-08 00:00:00.00   Mode  :character    Median : 140.0  
    ##  Mean   :2016-03-31 11:50:57.83                       Mean   : 164.9  
    ##  3rd Qu.:2017-04-01 00:00:00.00                       3rd Qu.: 220.0  
    ##  Max.   :2018-03-22 00:00:00.00                       Max.   :1440.0  
    ##                                                                       
    ##     AE_HRG          AE_Num_Diagnoses  AE_Num_Investigations AE_Num_Treatments
    ##  Length:600000      Min.   : 0.0000   Min.   : 0.00         Min.   : 0.000   
    ##  Class :character   1st Qu.: 0.0000   1st Qu.: 1.00         1st Qu.: 1.000   
    ##  Mode  :character   Median : 1.0000   Median : 1.00         Median : 2.000   
    ##                     Mean   : 0.8457   Mean   : 2.72         Mean   : 2.444   
    ##                     3rd Qu.: 1.0000   3rd Qu.: 4.00         3rd Qu.: 3.000   
    ##                     Max.   :10.0000   Max.   :10.00         Max.   :10.000   
    ##                                                                              
    ##  AE_Arrival_Mode Provider_Patient_Distance_Miles     ProvID     
    ##  Min.   :0.000   Min.   :  0.000                 Min.   :    0  
    ##  1st Qu.:2.000   1st Qu.:  2.000                 1st Qu.:15158  
    ##  Median :2.000   Median :  3.000                 Median :15233  
    ##  Mean   :1.747   Mean   :  7.332                 Mean   :15747  
    ##  3rd Qu.:2.000   3rd Qu.:  6.000                 3rd Qu.:15320  
    ##  Max.   :2.000   Max.   :200.000                 Max.   :32721  
    ##                  NA's   :589                                    
    ##  Admitted_Flag    Admission_Method   ICD10_Chapter_Code Treatment_Function_Code
    ##  Min.   :0.0000   Length:600000      Length:600000      Length:600000          
    ##  1st Qu.:0.0000   Class :character   Class :character   Class :character       
    ##  Median :0.0000   Mode  :character   Mode  :character   Mode  :character       
    ##  Mean   :0.1991                                                                
    ##  3rd Qu.:0.0000                                                                
    ##  Max.   :1.0000                                                                
    ##  NA's   :3                                                                     
    ##  Length_Of_Stay_Days
    ##  Min.   :  0.0      
    ##  1st Qu.:  1.0      
    ##  Median :  2.0      
    ##  Mean   :  5.5      
    ##  3rd Qu.:  6.0      
    ##  Max.   :180.0      
    ##  NA's   :481584

\#Encoding AE_Arrive_HourOfDay column

The goal of these steps is to transform the AE_Arrive_HourOfDay column
into a numeric form that can be more easily used for analysis. In the
original data, this column uses strings to denote specific ranges of
hours, like “01-04”, “05-08”, etc. We want to replace these with simpler
numeric codes, where “01-04” becomes “1”, “05-08” becomes “2”, and so
on.

The mutate() function from the dplyr package is used to modify the
AE_Arrive_HourOfDay column in our data frame. Inside this function, the
case_when() function is used to specify what each value in the column
should be replaced with. If a value doesn’t match any of the ones we
specified, it’s replaced with NA, a special value used in R to denote
missing or unknown data.

``` r
# Load the dplyr package
library(dplyr)

# Convert the AE_Arrive_HourOfDay column to character type to ensure string manipulations are allowed
subset_df$AE_Arrive_HourOfDay <- as.character(subset_df$AE_Arrive_HourOfDay)

# Encode AE_Arrive_HourOfDay using a conditional statement
# Each time period is assigned a specific number
# Any other value not within the specified time periods is assigned NA
subset_df <- subset_df %>% mutate(AE_Arrive_HourOfDay = case_when(
  AE_Arrive_HourOfDay == "01-04" ~ "1",
  AE_Arrive_HourOfDay == "05-08" ~ "2",
  AE_Arrive_HourOfDay == "09-12" ~ "3",
  AE_Arrive_HourOfDay == "13-16" ~ "4",
  AE_Arrive_HourOfDay == "17-20" ~ "5",
  AE_Arrive_HourOfDay == "21-24" ~ "6",
  TRUE ~ NA_character_  # for all other values not specified above
))

# Convert the column back to numeric for further numerical computations
subset_df$AE_Arrive_HourOfDay <- as.numeric(subset_df$AE_Arrive_HourOfDay)
```

``` r
#Checking for Missing Values in the DataFrame.
# Apply a function to each column of the dataframe to count the number of missing values
missing_values <- sapply(subset_df, function(x) sum(is.na(x)))
```

\#Handling Missing Values

This part of the code is dedicated to handling missing values in various
ways according to the nature of the column.

For the IMD_Decile_From_LSOA, AE_Arrive_HourOfDay, and
Provider_Patient_Distance_Miles columns, missing values are replaced
with the median of the column values. The median is a good choice for
replacement as it is not affected by outliers and gives a “middle” value
of the data.

The Sex and AE_HRG columns are categorical, thus missing values are
replaced with a new category, ‘Unknown’ and ‘nothing’, respectively.

For the Admitted_Flag column, missing values are replaced with the most
common (modal) value in the column.

Lastly, due to a large number of missing values or other reasons, some
columns like Admission_Method, ICD10_Chapter_Code,
Treatment_Function_Code, and Length_Of_Stay_Days are dropped from the
data frame.

``` r
# For numerical variables, replace missing values with the median of the column
subset_df$IMD_Decile_From_LSOA[is.na(subset_df$IMD_Decile_From_LSOA)] <- median(subset_df$IMD_Decile_From_LSOA, na.rm = TRUE)
subset_df$AE_Arrive_HourOfDay[is.na(subset_df$AE_Arrive_HourOfDay)] <- median(subset_df$AE_Arrive_HourOfDay, na.rm = TRUE)
subset_df$Provider_Patient_Distance_Miles[is.na(subset_df$Provider_Patient_Distance_Miles)] <- median(subset_df$Provider_Patient_Distance_Miles, na.rm = TRUE)

# For categorical variables, replace missing values with a new category ('Unknown' or 'nothing')
subset_df$Sex[is.na(subset_df$Sex)] <- 'Unknown'
subset_df$AE_HRG[is.na(subset_df$AE_HRG)] <- 'nothing'

# For binary variables, replace missing values with the most frequent value (mode)
most_common <- as.numeric(names(which.max(table(subset_df$Admitted_Flag))))
subset_df$Admitted_Flag[is.na(subset_df$Admitted_Flag)] <- most_common

# For columns with large missing values or other reasons, drop them from the data frame
subset_df <- subset_df %>% select(-c(Admission_Method, ICD10_Chapter_Code, Treatment_Function_Code, Length_Of_Stay_Days))
```

``` r
#Checking for Missing Values in the DataFrame.
# Apply a function to each column of the dataframe to count the number of missing values
missing_values <- sapply(subset_df, function(x) sum(is.na(x)))
```

``` r
# Display the structure of the dataframe to understand the data types and preview the first few values
str(subset_df)
```

    ## tibble [600,000 × 14] (S3: tbl_df/tbl/data.frame)
    ##  $ IMD_Decile_From_LSOA           : num [1:600000] 1 7 4 6 6 1 2 2 2 8 ...
    ##  $ Age_Band                       : chr [1:600000] "65-84" "25-44" "18-24" "1-17" ...
    ##  $ Sex                            : chr [1:600000] "2" "2" "1" "2" ...
    ##  $ AE_Arrive_Date                 : POSIXct[1:600000], format: "2014-06-06" "2016-09-23" ...
    ##  $ AE_Arrive_HourOfDay            : num [1:600000] 3 5 4 5 1 4 5 5 2 3 ...
    ##  $ AE_Time_Mins                   : num [1:600000] 40 100 240 120 830 150 230 60 170 50 ...
    ##  $ AE_HRG                         : chr [1:600000] "Low" "Low" "Nothing" "Nothing" ...
    ##  $ AE_Num_Diagnoses               : num [1:600000] 1 1 2 1 0 1 1 1 0 1 ...
    ##  $ AE_Num_Investigations          : num [1:600000] 1 2 3 10 6 2 2 1 1 1 ...
    ##  $ AE_Num_Treatments              : num [1:600000] 2 1 1 10 1 1 2 1 3 5 ...
    ##  $ AE_Arrival_Mode                : num [1:600000] 2 2 2 2 1 2 2 2 2 2 ...
    ##  $ Provider_Patient_Distance_Miles: num [1:600000] 1 0 3 2 8 2 1 5 1 1 ...
    ##  $ ProvID                         : num [1:600000] 15334 15287 15217 15310 15323 ...
    ##  $ Admitted_Flag                  : num [1:600000] 0 0 1 0 1 0 0 0 0 0 ...

``` r
# Apply a function to each column of the dataframe to count the number of unique values
unique_counts <- sapply(subset_df, function(x) length(unique(x)))
# Print the counts
print(unique_counts)
```

    ##            IMD_Decile_From_LSOA                        Age_Band 
    ##                              10                               6 
    ##                             Sex                  AE_Arrive_Date 
    ##                               3                            1461 
    ##             AE_Arrive_HourOfDay                    AE_Time_Mins 
    ##                               6                             145 
    ##                          AE_HRG                AE_Num_Diagnoses 
    ##                               5                              11 
    ##           AE_Num_Investigations               AE_Num_Treatments 
    ##                              11                              11 
    ##                 AE_Arrival_Mode Provider_Patient_Distance_Miles 
    ##                               3                             201 
    ##                          ProvID                   Admitted_Flag 
    ##                             238                               2

\#Outlier Detection and Visualization

\##Insights: By analyzing the results from the outlier detection
function and the boxplots, you can identify columns with a large number
of outliers that might require further cleaning or transformation. It
also gives you a visual understanding of the distribution of data in
each column, including the range of most values (the box) and potential
outliers (the points outside the box).

From the result of this analysis, it can be observed that there are no
outliers in the columns experiment on for outliers. This entails that we
can carry on with the analysis.

``` r
# List of columns to check for outliers
columns <- c("IMD_Decile_From_LSOA", "AE_Time_Mins", 
             "AE_Num_Diagnoses", "AE_Num_Investigations", "AE_Num_Treatments",
             "Provider_Patient_Distance_Miles")

# Function to calculate outliers using IQR method
outliers <- function(x) {
  quartile1 <- quantile(x, 0.25, na.rm = TRUE)
  quartile3 <- quantile(x, 0.75, na.rm = TRUE)
  iqr <- quartile3 - quartile1
  lower.bound <- quartile1 - 1.5 * iqr
  upper.bound <- quartile3 + 1.5 * iqr
  # Return the count of values below the lower bound or above the upper bound
  return(sum(x < lower.bound | x > upper.bound, na.rm = TRUE))
}

# Apply the function to each selected column and print the count of outliers
sapply(subset_df[columns], outliers)
```

    ##            IMD_Decile_From_LSOA                    AE_Time_Mins 
    ##                               0                           23255 
    ##                AE_Num_Diagnoses           AE_Num_Investigations 
    ##                            5975                           47446 
    ##               AE_Num_Treatments Provider_Patient_Distance_Miles 
    ##                           28471                           62852

``` r
# Set the layout for the plots
par(mfrow=c(2,3))  # adjust depending on the number of plots
# Loop over the selected columns and create a boxplot for each
for (col in columns) {
  boxplot(subset_df[[col]], main=col, ylab="Value", outline=FALSE)
}
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->
\#Calculating Basic Statistics for AE_Time_Mins

Insight: From the analysis, you should be able to understand the central
tendency and dispersion of the AE_Time_Mins column. For example, the
mean value gives an average time a patient spends in the A&E, the median
gives the middle value when the times are sorted in order, the minimum
and maximum values give the range of the times, and the standard
deviation measures the amount of variation or dispersion in the times.

``` r
# Compute and print the mean of AE_Time_Mins, ignoring missing values
mean(subset_df$AE_Time_Mins, na.rm = TRUE)  
```

    ## [1] 164.8593

``` r
# Compute and print the median of AE_Time_Mins, ignoring missing values
median(subset_df$AE_Time_Mins, na.rm = TRUE)  
```

    ## [1] 140

``` r
# Compute and print the minimum value of AE_Time_Mins, ignoring missing values
min(subset_df$AE_Time_Mins, na.rm = TRUE)  
```

    ## [1] 0

``` r
# Compute and print the maximum value of AE_Time_Mins, ignoring missing values
max(subset_df$AE_Time_Mins, na.rm = TRUE)  
```

    ## [1] 1440

``` r
# Compute and print the standard deviation of AE_Time_Mins, ignoring missing values
sd(subset_df$AE_Time_Mins, na.rm = TRUE)  
```

    ## [1] 139.0448

\##Basic Statistics for AE_Time_Mins

Insights:

Mean: The average time a patient spends in the A&E department is
approximately 165.22 minutes. This gives us a general idea of how long a
typical visit to A&E might last.

Median: The median time spent in the A&E department is 140 minutes. This
means that half of the patients spend less than 140 minutes, and the
other half spend more than this time. Since the mean is higher than the
median, this indicates that there are some patients who spend a
significantly longer time in the A&E department, pulling the average up.

Minimum: The shortest time spent by a patient in the A&E department is 0
minutes. This could possibly indicate that the patient left immediately
after arrival, or it might be due to some data recording issues.

Maximum: The longest time spent by a patient in the A&E department is
1440 minutes or a full day (24 hours). This suggests that there are
cases where patients spend a very long time in the A&E department,
perhaps due to severe conditions or complex treatment procedures.

Standard Deviation: The standard deviation is approximately 139.98
minutes. This relatively large standard deviation indicates a high level
of variation in the time patients spend in the A&E department. This is
likely due to the diverse nature of cases seen in the A&E department.

``` r
hist(subset_df$AE_Time_Mins, main = "Histogram of AE_Time_Mins", xlab = "AE_Time_Mins")
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
# Calculate IQR
Q1 <- quantile(subset_df$AE_Time_Mins, 0.25, na.rm = TRUE)
Q3 <- quantile(subset_df$AE_Time_Mins, 0.75, na.rm = TRUE)
IQR <- Q3 - Q1

# Define lower and upper threshold for outliers
lower_threshold <- Q1 - 1.5 * IQR
upper_threshold <- Q3 + 1.5 * IQR

# Calculate median
median_AE_Time_Mins <- median(subset_df$AE_Time_Mins, na.rm = TRUE)

# Replace outliers with the median
subset_df$AE_Time_Mins[subset_df$AE_Time_Mins < lower_threshold | subset_df$AE_Time_Mins > upper_threshold] <- median_AE_Time_Mins

hist(subset_df$AE_Time_Mins, main = "Histogram of AE_Time_Mins", xlab = "AE_Time_Mins")
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->
\#Histogram of Patient’s Stay Time in A&E Department

Insights:

The histogram shows the distribution of the time patients spend in the
A&E department.

The distribution appears to be right-skewed, indicating that while most
patients spend a relatively short amount of time in A&E, there is a long
tail of patients who spend a significantly longer time.

There is a peak at around the 0-240 minutes mark, indicating that most
patients spend around this much time in the A&E department.

The long tail to the right suggests that there are some cases where
patients have to spend a very long time in the department, possibly due
to more complex or severe medical conditions.

This kind of distribution could indicate a need for resource planning
and management, in order to effectively serve both the majority of
patients who require shorter stays, and the smaller number of patients
who require long stays. It might be useful to further investigate the
reasons behind extremely long stays, and whether there are ways to
manage these cases more effectively.

``` r
table(subset_df$Age_Band)  # Frequency counts
```

    ## 
    ##   1-17  18-24  25-44  45-64  65-84    85+ 
    ## 126713  63439 148625 117029  95101  49093

``` r
barplot(table(subset_df$Age_Band), main = "Bar Plot of Age Band", ylab = "Count", xlab = "Age Band")
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->
\#Distribution of Patient Age Bands in A&E Department

Insights:

The age band with the highest number of A&E department visits is the
“25-44” band, with 147,825 visits. This group includes individuals who
are in their prime working years. The high number of visits could be
related to work-related injuries, stress, or lifestyle factors that
contribute to health issues requiring emergency care.

The second most frequent group visiting the A&E department is the “1-17”
band, with 126,741 visits. This suggests that young people, likely due
to physical activities and injuries, also represent a significant
proportion of emergency department visits.

The “45-64” band and “65-84” band also show significant visit numbers,
with 117,451 and 95,420 visits respectively. These age bands may include
individuals with more chronic health conditions, which require more
frequent emergency care.

The age band “18-24” shows a relatively lower number of visits (63,785).
This could be due to a generally healthier age group, and thus less
likely to require emergency care.

The age band “85+” has the least visits at 48,778. This might be due to
the smaller population size in this age band, or it might indicate that
the oldest individuals are being cared for in other ways, such as
through primary care or long-term care facilities.

In summary, the distribution shows that all age bands make use of A&E
services, but there is a clear concentration in the “25-44” age band.
Understanding the specific reasons behind these trends could help in
planning and resource allocation for A&E services.

``` r
table(subset_df$AE_Arrive_HourOfDay)  # Frequency counts
```

    ## 
    ##      1      2      3      4      5      6 
    ##  42399  45972 163749 151861 136415  59604

``` r
# Load the ggplot2 package
library(ggplot2)

# Convert AE_Arrive_HourOfDay to factor to preserve the order in the plot
subset_df$AE_Arrive_HourOfDay <- as.factor(subset_df$AE_Arrive_HourOfDay)

# Create the bar chart with colors
ggplot(subset_df, aes(x=AE_Arrive_HourOfDay, fill=AE_Arrive_HourOfDay)) +
  geom_bar() +
  xlab("Arrival Hour of Day") +
  ylab("Count") +
  ggtitle("Bar Chart of Arrival Hour of Day") +
  scale_fill_viridis_d(
    labels=c("1" = "1am-4am", 
                            "2" = "5am-8am", 
                            "3" = "9am-12noon", 
                            "4" = "1pm-4pm",
                            "5" = "5pm-8pm", 
                            "6" = "9pm-12midnight"))  # add custom x-axis labels
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-20-1.png)<!-- --> \#Bar
Chart of Patient Arrival Time Ranges at A&E Department

Insights:

The bar chart provides a clear visual representation of when most
patients arrive at the A&E department.

There are significantly more patient arrivals during the midday hours
(9am-12noon), followed by the early afternoon hours (1pm-4pm) and then
the evening hours (5pm-8pm).

The periods of 1am-4am and 9pm-12midnight have the lowest number of
patient arrivals, which is to be expected as these are generally
non-peak hours.

Given the substantial difference in patient arrivals across these time
ranges, the healthcare facility could consider allocating resources
accordingly. For instance, more staff could be scheduled to work during
peak hours to manage the higher patient volume. Similarly, services
could be scaled down during non-peak hours.

Further, this information could be communicated to patients, advising
them that wait times may be longer during peak hours and suggesting
non-peak times to visit for non-emergency situations.

This kind of temporal information is very valuable for operations and
resource planning in healthcare settings.

``` r
# Load the necessary packages
library(dplyr)

# Create a new column for arrival day
subset_df <- subset_df %>%
  mutate(Arrival_Day = weekdays(AE_Arrive_Date))

# Check the first few rows of the updated dataframe
head(subset_df)
```

    ## # A tibble: 6 × 15
    ##   IMD_Decile_From_LSOA Age_Band Sex   AE_Arrive_Date      AE_Arrive_HourOfDay
    ##                  <dbl> <chr>    <chr> <dttm>              <fct>              
    ## 1                    1 65-84    2     2014-06-06 00:00:00 3                  
    ## 2                    7 25-44    2     2016-09-23 00:00:00 5                  
    ## 3                    4 18-24    1     2017-09-10 00:00:00 4                  
    ## 4                    6 1-17     2     2015-12-20 00:00:00 5                  
    ## 5                    6 45-64    1     2017-03-29 00:00:00 1                  
    ## 6                    1 65-84    2     2014-09-04 00:00:00 4                  
    ## # ℹ 10 more variables: AE_Time_Mins <dbl>, AE_HRG <chr>,
    ## #   AE_Num_Diagnoses <dbl>, AE_Num_Investigations <dbl>,
    ## #   AE_Num_Treatments <dbl>, AE_Arrival_Mode <dbl>,
    ## #   Provider_Patient_Distance_Miles <dbl>, ProvID <dbl>, Admitted_Flag <dbl>,
    ## #   Arrival_Day <chr>

\#Creating a New Column for Arrival Day

Insights:

By adding a new column for the day of the week, we can perform further
analysis and generate insights based on the day of the week of patient
arrivals.

For example, we can now calculate the average number of patient arrivals
by day of the week, which could help in understanding patterns of
patient visits and in planning staffing levels for different days of the
week.

Additionally, we could perform further analysis to examine if there are
any significant differences in metrics such as average time spent in the
A&E department, number of diagnoses, treatments, etc. based on the day
of the week.

This new column, Arrival_Day, provides an additional level of
granularity to the data, which could be valuable for uncovering patterns
and trends that were not apparent before.

``` r
# Turn Arrival_Day into a factor with ordered levels
subset_df$Arrival_Day <- factor(subset_df$Arrival_Day, levels = c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
```

``` r
# Load the necessary packages
library(ggplot2)
library(viridis)
```

    ## Loading required package: viridisLite

``` r
# Create the bar plot
ggplot(subset_df, aes(x = Arrival_Day)) +
  geom_bar(aes(fill = Arrival_Day)) +
  scale_fill_viridis_d() +   # Add this line to change color palette
  labs(x = "Day of the Week", y = "Count", title = "Number of Arrivals by Day of the Week") +
  theme_minimal()
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->
Insights:

The generated bar chart provides a visual representation of the count of
patient arrivals on each day of the week. From the chart, we can see
that Saturday has the highest number of patient arrivals, followed by
Sunday. This could be due to various reasons, like more accidents
happening over the weekend or people having more free time to visit the
hospital. Wednesday has the least number of arrivals.

This information can be helpful for hospital management to allocate
resources more efficiently based on the days of the week. For instance,
they may need to allocate more staff and resources on Saturdays to cater
to the high volume of patients. Conversely, they could potentially save
on resources during less busy days like Wednesdays.

This chart emphasizes the importance of considering temporal factors in
healthcare management and planning.

``` r
library(dplyr)
library(lubridate)

# Add month column
subset_df$Month_Num <- month(subset_df$AE_Arrive_Date)
subset_df$Month <- factor(month.name[subset_df$Month_Num], levels = month.name)


# Add season column based on the month
subset_df$Season <- case_when(
  subset_df$Month %in% c("Dec", "Jan", "Feb") ~ "Winter",
  subset_df$Month %in% c("Mar", "Apr", "May") ~ "Spring",
  subset_df$Month %in% c("Jun", "Jul", "Aug") ~ "Summer",
  subset_df$Month %in% c("Sep", "Oct", "Nov") ~ "Autumn",
  TRUE                                        ~ NA_character_
)
```

``` r
ggplot(subset_df, aes(x = Month)) +
  geom_bar(aes(fill = Month)) +
  scale_fill_viridis_d() +
  labs(x = "Month", y = "Count", title = "Number of Arrivals by Month") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

``` r
# Aggregate the data by Month
monthly_counts <- subset_df %>%
  group_by(Month) %>%
  summarise(Count = n())

# Plot a line graph with points for each month
ggplot(monthly_counts, aes(x = Month, y = Count)) +
  geom_line(aes(group = 1), color = "blue") +
  geom_point(aes(color = Month), size = 3) +
  scale_fill_viridis_d() +
  scale_color_viridis_d() +
  labs(x = "Month", y = "Count", title = "Number of Arrivals by Month") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
#install.packages("hexbin")
library(hexbin)
```

    ## Warning: package 'hexbin' was built under R version 4.3.1

``` r
# Create the hexbin plot
ggplot(subset_df, aes(x=AE_Num_Treatments, y=AE_Num_Diagnoses)) +
  stat_binhex(aes(fill = ..count..), bins = 30) +
  scale_fill_gradient(low = "white", high = "red") +
  theme_minimal() +
  xlab("Number of Treatments") +
  ylab("Number of Diagnoses") +
  ggtitle("Hexbin Plot of Number of Treatments vs Number of Diagnoses")
```

    ## Warning: The dot-dot notation (`..count..`) was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `after_stat(count)` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

![](AE_Analysis_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->
Insights:

The generated hexbin plot provides a visual representation of the
relationship between the number of treatments and diagnoses. From the
plot, it’s clear that most patients have 1 treatment and 1 diagnosis,
followed by patients having 2 treatments and 1 diagnosis. There are also
a few instances where the number of treatments goes up to around 10 or
11, but these are relatively rare.

This could suggest that for most patients, a single diagnosis leads to a
single treatment, but in some complex cases, multiple treatments might
be needed. This is valuable information for healthcare providers as it
helps them understand patient needs and the complexity of cases they are
likely to encounter.

``` r
# Contingency table
contingency_table <- table(subset_df$AE_Arrival_Mode, subset_df$Admitted_Flag)

# Chi-square test
chisq_test <- chisq.test(contingency_table)
print(chisq_test)
```

    ## 
    ##  Pearson's Chi-squared test
    ## 
    ## data:  contingency_table
    ## X-squared = 100499, df = 2, p-value < 2.2e-16

The Chi-squared test is a statistical test that’s used to determine if
there’s a significant association between two categorical variables. In
this case, the test is used to see if there’s an association between the
AE_Arrival_Mode and Admitted_Flag variables.

Here’s what each part of the test result means:

X-squared: This is the chi-square statistic. It’s a measure of how much
observed frequencies differ from expected frequencies. In this case, the
chi-square statistic is 101278, which is quite high.

df: This stands for “degrees of freedom”. It’s calculated as (number of
rows - 1) \* (number of columns - 1) in the contingency table. Here, df
= 2, meaning your contingency table likely had 3 rows and 3 columns (or
some other combination that would result in 2 degrees of freedom when
the above formula is used).

p-value: The p-value is a measure of the probability that an observed
difference could have occurred just by random chance. In this case, the
p-value is less than 2.2e-16, which is effectively zero. This is less
than 0.05, which is typically used as the threshold for statistical
significance in many fields.

So, in simple terms, the output of the chi-square test is saying that
there is a statistically significant association between AE_Arrival_Mode
and Admitted_Flag variables in this dataset, as the p-value is less than
0.05. That is, the mode of arrival at the hospital appears to be
associated with whether or not a patient is admitted.

Remember, this test doesn’t tell you anything about the nature or
strength of the relationship, just that the variables are not
independent.

``` r
ggplot(subset_df, aes(x = AE_Arrival_Mode, fill = factor(Admitted_Flag))) +
  geom_bar(position = "fill") +   # Use "dodge" for a grouped bar plot
  labs(x = "Arrival Mode", y = "Proportion", fill = "Admitted") +
  scale_fill_discrete(name = "Admitted", labels = c("No", "Yes"))
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->
Insights:

The stacked bar chart provides a visualization of the proportion of
admitted cases by arrival mode. From the chart, it can be observed that
the proportion of admitted cases varies with the arrival mode:

For arrival mode 0, around 25% of the cases are admitted. For arrival
mode 1, approximately half of the cases are admitted. For arrival mode
2, a smaller proportion (around 12%) of the cases are admitted. This
suggests that the arrival mode could be a significant factor in the
likelihood of admission. Specifically, arrival mode 1 appears to have a
higher proportion of admissions, which could be due to the severity of
the conditions associated with this mode. It would be interesting to
investigate further what each arrival mode signifies and if certain
conditions or emergencies are more commonly associated with each mode.

``` r
#install.packages("forecast")

library(forecast)
```

    ## Warning: package 'forecast' was built under R version 4.3.1

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

``` r
# Convert AE_Arrive_Date to Date object
subset_df$AE_Arrive_Date <- as.Date(subset_df$AE_Arrive_Date)

# Combine Date and Hour to create a DateTime column
subset_df$AE_Arrive_DateTime <- subset_df$AE_Arrive_Date + hours(subset_df$AE_Arrive_HourOfDay)
```

``` r
# Count number of arrivals each day
subset_df_daily <- subset_df %>%
  group_by(AE_Arrive_Date) %>%
  summarise(Arrivals = n(), .groups = "drop")
```

``` r
# Create time series object
ts_daily <- ts(subset_df_daily$Arrivals, start = min(subset_df_daily$AE_Arrive_Date), frequency = 365)
```

``` r
ggplot(subset_df_daily, aes(x = AE_Arrive_Date, y = Arrivals)) +
  geom_line() +
  labs(x = "Date", y = "Number of Arrivals", title = "Daily Patient Arrivals")
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

``` r
# Load necessary libraries
library(lubridate)
library(dplyr)

# Convert AE_Arrive_Date to Date format if it's not already
subset_df$AE_Arrive_Date <- as.Date(subset_df$AE_Arrive_Date)

# Calculate daily averages
daily_averages <- subset_df %>%
  group_by(AE_Arrive_Date) %>%
  summarise(daily_cases = n()) %>%
  summarise(avg_daily_cases = mean(daily_cases))

# Calculate weekly averages
weekly_averages <- subset_df %>%
  mutate(week = week(AE_Arrive_Date)) %>%
  group_by(week) %>%
  summarise(weekly_cases = n()) %>%
  summarise(avg_weekly_cases = mean(weekly_cases))

# Calculate monthly averages
monthly_averages <- subset_df %>%
  mutate(month = month(AE_Arrive_Date)) %>%
  group_by(month) %>%
  summarise(monthly_cases = n()) %>%
  summarise(avg_monthly_cases = mean(monthly_cases))

# Calculate yearly averages
yearly_averages <- subset_df %>%
  mutate(year = year(AE_Arrive_Date)) %>%
  group_by(year) %>%
  summarise(yearly_cases = n()) %>%
  summarise(avg_yearly_cases = mean(yearly_cases))

# Print results
print(paste("Average daily cases: ", daily_averages$avg_daily_cases))
```

    ## [1] "Average daily cases:  410.677618069815"

``` r
print(paste("Average weekly cases: ", weekly_averages$avg_weekly_cases))
```

    ## [1] "Average weekly cases:  11320.7547169811"

``` r
print(paste("Average monthly cases: ", monthly_averages$avg_monthly_cases))
```

    ## [1] "Average monthly cases:  50000"

``` r
print(paste("Average yearly cases: ", yearly_averages$avg_yearly_cases))
```

    ## [1] "Average yearly cases:  120000"

``` r
class(subset_df$AE_Arrive_HourOfDay)
```

    ## [1] "factor"

``` r
# Calculate average AE cases for each category
hourly_averages <- subset_df %>%
  group_by(AE_Arrive_HourOfDay) %>%
  summarise(hourly_cases = n()) %>%
  mutate(avg_hourly_cases = hourly_cases / n())

# Print the hourly averages
print(hourly_averages)
```

    ## # A tibble: 6 × 3
    ##   AE_Arrive_HourOfDay hourly_cases avg_hourly_cases
    ##   <fct>                      <int>            <dbl>
    ## 1 1                          42399            7066.
    ## 2 2                          45972            7662 
    ## 3 3                         163749           27292.
    ## 4 4                         151861           25310.
    ## 5 5                         136415           22736.
    ## 6 6                          59604            9934

``` r
# Correlation between diagnoses and investigations
cor(subset_df$AE_Num_Diagnoses, subset_df$AE_Num_Investigations, use = "pairwise.complete.obs")
```

    ## [1] 0.1233873

``` r
# Correlation between diagnoses and treatments
cor(subset_df$AE_Num_Diagnoses, subset_df$AE_Num_Treatments, use = "pairwise.complete.obs")
```

    ## [1] 0.1659091

``` r
# Correlation between investigations and treatments
cor(subset_df$AE_Num_Investigations, subset_df$AE_Num_Treatments, use = "pairwise.complete.obs")
```

    ## [1] 0.4497278

``` r
# Recode the Sex variable
subset_df$Sex <- recode(subset_df$Sex, `1` = "Male", `2` = "Female")

# Count the number of each gender
gender_counts <- subset_df %>%
  group_by(Sex) %>%
  summarise(Count = n(), .groups = "drop")

# Plot the bar chart
ggplot(gender_counts, aes(x = Sex, y = Count, fill = Sex)) +
  geom_bar(stat = "identity") +
  scale_fill_manual(values = c("Male" = "blue", "Female" = "pink", "Unknown" = "grey")) +
  labs(x = "Gender", y = "Count", fill = "Gender", title = "Bar Chart of Gender") +
  theme_minimal() 
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

``` r
# Frequency table for the Sex variable
gender_freq_table <- table(subset_df$Sex)

# Print the frequency table
print(gender_freq_table)
```

    ## 
    ##  Female    Male Unknown 
    ##  302770  296162    1068

``` r
# Summary statistics for Provider_Patient_Distance_Miles
summary(subset_df$Provider_Patient_Distance_Miles)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   0.000   2.000   3.000   7.328   6.000 200.000

``` r
# Correlation with Length_Of_Stay_Days
cor(subset_df$Provider_Patient_Distance_Miles, subset_df$AE_Time_Mins, use = "pairwise.complete.obs")
```

    ## [1] -0.02741544

``` r
# Correlation with AE_Num_Treatments
cor(subset_df$Provider_Patient_Distance_Miles, subset_df$AE_Num_Treatments, use = "pairwise.complete.obs")
```

    ## [1] -0.008730695

``` r
# Group by ProvID and calculate average metrics
provider_metrics <- subset_df %>%
  group_by(ProvID) %>%
  summarise(
    avg_num_diagnoses = mean(AE_Num_Diagnoses, na.rm = TRUE),
    avg_num_treatments = mean(AE_Num_Treatments, na.rm = TRUE),
    avg_patient_distance = mean(Provider_Patient_Distance_Miles, na.rm = TRUE)
  )

# Print the first few rows of the resulting dataframe
head(provider_metrics)
```

    ## # A tibble: 6 × 4
    ##   ProvID avg_num_diagnoses avg_num_treatments avg_patient_distance
    ##    <dbl>             <dbl>              <dbl>                <dbl>
    ## 1      0             0.497               1.83                 1.05
    ## 2  13034             0                   1.47                 5.83
    ## 3  13099             0                   1.02                 8.92
    ## 4  13100             0                   1                    5.25
    ## 5  13101             0                   1                    7.16
    ## 6  13438             1.06                1.99                 3.82

``` r
# Summary statistics for provider metrics
summary(provider_metrics)
```

    ##      ProvID      avg_num_diagnoses avg_num_treatments avg_patient_distance
    ##  Min.   :    0   Min.   :0.0000    Min.   : 0.000     Min.   : 1.051      
    ##  1st Qu.:15157   1st Qu.:0.7165    1st Qu.: 1.747     1st Qu.: 5.030      
    ##  Median :15254   Median :0.9969    Median : 2.137     Median : 6.630      
    ##  Mean   :18028   Mean   :0.8493    Mean   : 2.260     Mean   : 9.243      
    ##  3rd Qu.:15375   3rd Qu.:1.0560    3rd Qu.: 2.664     3rd Qu.: 9.782      
    ##  Max.   :32721   Max.   :2.7602    Max.   :10.000     Max.   :86.500

``` r
# Boxplots of provider metrics
par(mfrow = c(1, 3))
boxplot(avg_num_diagnoses ~ ProvID, data = provider_metrics, main = "Average Diagnoses by Provider")
boxplot(avg_num_treatments ~ ProvID, data = provider_metrics, main = "Average Treatments by Provider")
boxplot(avg_patient_distance ~ ProvID, data = provider_metrics, main = "Average Patient Distance by Provider")
```

![](AE_Analysis_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

``` r
# ANOVA tests
anova(lm(avg_num_diagnoses ~ ProvID, data = provider_metrics))
```

    ## Analysis of Variance Table
    ## 
    ## Response: avg_num_diagnoses
    ##            Df Sum Sq  Mean Sq F value Pr(>F)
    ## ProvID      1  0.026 0.026221  0.1378 0.7108
    ## Residuals 236 44.913 0.190309

``` r
anova(lm(avg_num_treatments ~ ProvID, data = provider_metrics))
```

    ## Analysis of Variance Table
    ## 
    ## Response: avg_num_treatments
    ##            Df Sum Sq Mean Sq F value    Pr(>F)    
    ## ProvID      1   16.8 16.8047  11.143 0.0009799 ***
    ## Residuals 236  355.9  1.5081                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
anova(lm(avg_patient_distance ~ ProvID, data = provider_metrics))
```

    ## Analysis of Variance Table
    ## 
    ## Response: avg_patient_distance
    ##            Df  Sum Sq Mean Sq F value   Pr(>F)   
    ## ProvID      1   797.5  797.46  9.2517 0.002619 **
    ## Residuals 236 20342.1   86.20                    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
