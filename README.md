# Portfolio_Project_PeopleAnalytics: In this project, I analyze and integrate employee demographic and survey data to uncover insights into workforce engagement, tenure, and turnover. The goal is to demonstrate capabilities in data cleaning, exploration, & People Analytics storytelling.

#STEP 1: Cleaning/Merging/Data Wrangling. I used the following AI prompt:
#"You are a data scientist working in R. Using the attached datasets:
1.	Clean each dataset:
    • Remove duplicate rows
    • Replace missing values (NA or blanks) in numeric columns with column averages
2.	Merge the datasets based on a common key (e.g., Employee_ID)
Return the cleaned, merged dataset.

#STEP 2: I downloaded the merged dataset titled "Cleaned_Merged_Dataset" 

#STEP 3: I uploaded the cleaned & merged dataset titled "Cleaned_Merged_Dataset" into R 

#STEP 4: Within R Studio, I explored the data with the following; summary stats, correlation matrix, visualizing key relationships. See below: 

> summary(Cleaned_Merged_Dataset)
  employee_id         age         department         tenure_years       turnover       engagement    manager_relationship work_life_balance career_growth 
 Min.   :  1.0   Min.   :22.00   Length:500         Min.   : 0.000   Min.   :0.000   Min.   :1.000   Min.   :1.000        Min.   :1.000     Min.   :1.00  
 1st Qu.:125.8   1st Qu.:32.00   Class :character   1st Qu.: 0.800   1st Qu.:0.000   1st Qu.:2.000   1st Qu.:2.000        1st Qu.:2.000     1st Qu.:2.00  
 Median :250.5   Median :43.00   Mode  :character   Median : 2.100   Median :0.000   Median :3.000   Median :3.000        Median :3.000     Median :3.00  
 Mean   :250.5   Mean   :41.32                      Mean   : 3.047   Mean   :0.194   Mean   :3.018   Mean   :3.044        Mean   :3.022     Mean   :2.96  
 3rd Qu.:375.2   3rd Qu.:51.00                      3rd Qu.: 4.300   3rd Qu.:0.000   3rd Qu.:4.000   3rd Qu.:4.000        3rd Qu.:4.000     3rd Qu.:4.00  
 Max.   :500.0   Max.   :59.00                      Max.   :18.500   Max.   :1.000   Max.   :5.000   Max.   :5.000        Max.   :5.000     Max.   :5.00  

> cor(Cleaned_Merged_Dataset[sapply(Cleaned_Merged_Dataset, is.numeric)])
                     employee_id          age tenure_years     turnover   engagement manager_relationship work_life_balance career_growth
employee_id           1.00000000  0.066858200   0.05414824 -0.039018747 -0.031938385          -0.04308779      -0.036574751   0.112519094
age                   0.06685820  1.000000000   0.03755944  0.015010436 -0.003500400          -0.01970912      -0.086913743   0.009055435
tenure_years          0.05414824  0.037559445   1.00000000 -0.024196938 -0.056175618           0.03617139       0.035901727  -0.029123833
turnover             -0.03901875  0.015010436  -0.02419694  1.000000000  0.008189831           0.02020870       0.034821997  -0.081823686
engagement           -0.03193838 -0.003500400  -0.05617562  0.008189831  1.000000000           0.05068096      -0.074393085   0.031527902
manager_relationship -0.04308779 -0.019709119   0.03617139  0.020208699  0.050680959           1.00000000      -0.073435561   0.075972444
work_life_balance    -0.03657475 -0.086913743   0.03590173  0.034821997 -0.074393085          -0.07343556       1.000000000  -0.007382991
career_growth         0.11251909  0.009055435  -0.02912383 -0.081823686  0.031527902           0.07597244      -0.007382991   1.000000000

> ggplot(Cleaned_Merged_Dataset, aes(x = engagement, y = turnover)) +
+     geom_jitter() +
+     geom_smooth(method = "lm") +
+     labs(title = "Engagement vs Turnover")
`geom_smooth()` using formula = 'y ~ x'

#STEP 5: I generated insights based on questions like; Ask questions like: "Do low engagement scores correlate with turnover?", "are certain departments more at risk of attrition?", "What are the predictors of turover from the survey results?" 

> aggregate(engagement ~ tenure_years, data = Cleaned_Merged_Dataset, FUN = mean)
    tenure_years engagement
1            0.0   2.166667
2            0.1   3.400000
3            0.2   3.133333
4            0.3   2.894737
5            0.4   3.333333
6            0.5   3.133333
7            0.6   2.928571
8            0.7   2.857143
9            0.8   3.222222
10           0.9   2.615385
11           1.0   3.333333
12           1.1   4.333333
13           1.2   2.444444
14           1.3   3.300000
15           1.4   3.166667
16           1.5   2.666667
17           1.6   3.250000
18           1.7   3.625000
19           1.8   3.666667
20           1.9   1.200000
21           2.0   2.222222
22           2.1   3.250000
23           2.2   3.166667
24           2.3   3.000000
25           2.4   3.400000
26           2.5   3.000000
27           2.6   3.000000
28           2.7   4.000000
29           2.8   2.666667
30           2.9   3.111111
31           3.0   3.000000
32           3.1   1.500000
33           3.2   2.888889
34           3.3   2.600000
35           3.4   3.000000
36           3.5   2.500000
37           3.6   2.857143
38           3.7   3.800000
39           3.8   3.000000
40           3.9   2.500000
41           4.0   3.000000
42           4.1   2.000000
43           4.2   3.666667
44           4.3   3.000000
45           4.4   2.800000
46           4.5   3.000000
47           4.6   5.000000
48           4.7   2.500000
49           4.8   2.666667
50           4.9   3.500000
51           5.0   4.000000
52           5.1   3.333333
53           5.2   4.500000
54           5.3   3.666667
55           5.4   4.333333
56           5.6   1.000000
57           5.7   1.666667
58           5.8   2.000000
59           5.9   4.250000
60           6.0   4.000000
61           6.1   2.400000
62           6.2   2.571429
63           6.3   4.000000
64           6.4   4.000000
65           6.5   3.500000
66           6.6   3.000000
67           6.7   3.666667
68           6.8   2.000000
69           6.9   5.000000
70           7.4   3.500000
71           7.5   3.000000
72           7.6   3.000000
73           7.7   2.000000
74           7.8   1.000000
75           7.9   2.000000
76           8.1   3.000000
77           8.3   2.333333
78           8.4   2.000000
79           8.6   1.000000
80           8.7   2.333333
81           8.8   5.000000
82           8.9   4.000000
83           9.0   2.000000
84           9.3   1.000000
85           9.7   3.000000
86           9.9   3.000000
87          10.3   1.000000
88          10.4   2.000000
89          10.6   3.000000
90          10.9   3.000000
91          11.0   5.000000
92          11.2   3.000000
93          11.9   3.000000
94          12.4   3.500000
95          12.5   4.000000
96          13.0   5.000000
97          13.2   3.500000
98          14.2   4.000000
99          15.8   1.000000
100         16.8   1.000000
101         17.3   2.000000
102         17.6   5.000000
103         18.5   1.000000



#Produced bar graph that shows turnover rate by department: 

> library(dplyr)
library(ggplot2)

> Cleaned_Merged_Dataset %>%
+     group_by(department) %>%
+     summarise(turnover_rate = mean(turnover)) %>%
+     ggplot(aes(x = department, y = turnover_rate)) +
+     geom_col(fill = "steelblue") +
+     labs(title = "Turnover Rate by Department", y = "Turnover Rate")


#Analyzed Drivers of Turnover by running a bomial logistic regression using survey responses (e.g., engagement, satisfaction) as predictors

> model <- glm(turnover ~ engagement + manager_relationship + work_life_balance,
+              data = Cleaned_Merged_Dataset, family = "binomial")
> summary(model)

Call:
glm(formula = turnover ~ engagement + manager_relationship + 
    work_life_balance, family = "binomial", data = Cleaned_Merged_Dataset)

Coefficients:
                     Estimate Std. Error z value Pr(>|z|)    
(Intercept)          -1.80281    0.45641  -3.950 7.81e-05 ***
engagement            0.01792    0.08166   0.219    0.826    
manager_relationship  0.03990    0.07948   0.502    0.616    
work_life_balance     0.06600    0.07971   0.828    0.408    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 491.97  on 499  degrees of freedom
Residual deviance: 491.05  on 496  degrees of freedom
AIC: 499.05

Number of Fisher Scoring iterations: 4


#Visualized the Bionomial Logistic Regression to find out predictors of turnover from survey responses 

> library(broom)

> tidy(model) %>%
+     filter(term != "(Intercept)") %>%
+     ggplot(aes(x = reorder(term, estimate), y = estimate)) +
+     geom_col() +
+     coord_flip() +
+     labs(title = "Impact of Survey Responses on Turnover Odds",
+          x = "Survey Item", y = "Log Odds Estimate")
