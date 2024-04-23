MTHCS Teacher Retention Case Study
================
EShaw
2024-04-20

**Background**  
This case studies a medium sized school district in Southwest Ohio that
has been experiencing a high rate of teacher turnover recently. The
purpose of this investigation is to see what trends can be noticed from
data that is publicly available before using additional resources to
collect more data. I have pulled data from the Ohio Department of
Education’s (ODE) public data repository. This information would be
presented to the school principals as well as other stakeholders in the
district.

**Problem**  
Between the 2022-2023 and 2023-2024 school years, this school district
had 23% of its teaching staff leave the district.

**Analysis**  
The data we have from the state will not give us the whole picture, but
it gives us a good place to start. By examining the correlations between
years of experience, teacher attendance, salary, highest degree earned,
and whether the teacher returned the following year; we hope to spot
some trends. With this information, we can either collect more data or
start to take steps to help improve the problem.

*Limitations*  
*As this is a case study rather than a real request from a client, there
were some limitations to my analysis.The data took some cleaning to be
able to produce visualizations, and in that process it became clear that
there are at least a few teachers missing from the ODE public data sets.
There is no clear reason why they are missing. Since we are doing a
surface level analysis to find trends, it seemed appropriate to analyze
without these teachers in the data. If I had actually received a request
from the school board to do an analysis, however, I would make sure that
these teachers were accounted for.*

Let’s explore the data together!

## R Markdown

``` r
library(tidyverse)
library(ggplot2)
```

``` r
teacher_info <- read.csv("MTHCS Teacher Info.csv")
names(teacher_info)[7] <- "Years_of_Experience"
head(teacher_info)
```

    ##   State.License Gender      Race.Ethnicity Degree.Type Yearly.Salary Staff.FTE
    ## 1            OH Female White, Non-Hispanic     Masters         32165         1
    ## 2            OH Female White, Non-Hispanic   Bachelors         35307         1
    ## 3            OH Female White, Non-Hispanic   Bachelors         39834         1
    ## 4            OH Female White, Non-Hispanic   Bachelors         42520         1
    ## 5            OH   Male White, Non-Hispanic   Bachelors         42520         1
    ## 6            OH   Male White, Non-Hispanic   Bachelors         42520         1
    ##   Years_of_Experience Teacher.Attendance Returned.in.2023
    ## 1                   4               0.82            FALSE
    ## 2                   0               0.97             TRUE
    ## 3                   0               0.70             TRUE
    ## 4                   0               0.95             TRUE
    ## 5                   0               0.95             TRUE
    ## 6                   0               0.84             TRUE

First, we check the correlation between teacher experience, teacher
salary, and retention for trends.

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20experience%20vs.%20salary-1.png)<!-- -->

There does not appear to be correlation between salary and retention,
but teachers with less experience do appear to have a lower retention
rate.

Next we’ll check to see if there are any trends between years of
experience, teacher attendance, and retention.

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20experience%20vs.%20attendance-1.png)<!-- -->

There appear to be plenty of teachers with higher and lower attendance
rates that were not retained. In teachers with an attendance rate less
than 75%, there is a very low rate of retention.

The last data attributes we can check for trends are gender and degree
type:

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20experience%20vs.%20degree%20type-1.png)<!-- -->

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20experience%20vs.%20gender-1.png)<!-- -->

While degree type and gender do not seem to factor into retention, these
charts do help illustrate that retention appears to be lower in teachers
with less than ten years of experience. Let’s see if there are any
trends we can spot with the subset of teachers who have less than ten
years of experience.

``` r
teachers_under_ten <- subset(teacher_info, Years_of_Experience <= 10)
```

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20under%2010%20years%20experience%20vs.%20salary-1.png)<!-- -->

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20under%2010%20years%20experience%20vs.%20attendance-1.png)<!-- -->

![](Teacher-Retention_files/figure-gfm/make%20correlation%20charts%20for%20under%2010%20years%20experience%20vs.%20degree%20type-1.png)<!-- -->

There do not appear to be any discernible patterns when we focus on the
subset of teachers with less than ten years of experience.

**Solutions and Next Steps**  
There seem to be two groups that appear to trend towards quitting more
often than the others: those with very low attendance (less than 75%),
and teachers that have less than 10 years of experience.

Since there were only six teachers with less than 75% attendance it
likely does not make sense to focus on that subgroup when trying to find
solutions. Teachers that miss this much school are often on medical or
family leave, which are both situations that could affect retention but
the school has no influence over.

The group to focus on would be the teachers with less than ten years of
experience. There are a few next steps that would help the school
district retain more teachers in this subgroup:

1.  Collect More Data:
    - Conduct exit interviews and collect the following information:
      - Reason for leaving
      - Are you staying in education?
      - Where are you going next?
    - Track teacher evaluation scores for those who stay in education
      - Are the teachers who are leaving high or low performers?
      - Are they scoring better in a new district?
    - Do a case study on the best teachers that have less than 10 years
      of experience
      - What qualities do they have that make them a good fit?
      - How can we adjust our hiring practices to ensure we have
        teachers who are a good fit?
    - Request historical data and state-wide data
      - How does the retention this year compare to other years?
      - How does the retention of this school district compare to
        similar districts?
2.  Actively seek feedback to help retain teachers that have less than
    10 years of experience:
    - Survey teachers with less than 10 years of experience or conduct
      focus groups
      - These are the teachers who will be able to tell the principals
        what issues they are dealing with, and what support they could
        receive to help them stay in the district
    - Make a committee of teachers and district leaders to create an
      action plan based on the results of these surveys

**Conclusion**  
It is difficult to retain teachers, and there are a myriad of factors
that can affect a teacher’s decision to stay in a certain district. By
focusing the district’s efforts on not only retaining but developing
their less experienced teachers, they can hopefully keep more of their
teachers going forward.
