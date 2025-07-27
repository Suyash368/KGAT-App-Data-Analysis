## KGAT App Data Analysis
A data-driven case study to uncover agricultural insights from mobile app usage by farmers — focused on Chilli Disease & Variety Trends using R and Microsoft Excel.  
This project analyzes real-world data collected through the KGAT (Khamma Ghani Agro Tech) mobile application, developed to empower farmers with actionable knowledge. Using usage logs and disease/variety access data for chilli crops, this analysis helps uncover key insights on: 

Disease prevalence (especially Leaf Curl).  
User growth trends.  
Weekly app engagement patterns.  
Statistical validation of farmer behavior and disease-weather relations.

## Dataset Description  
The dataset contains multiple sheets from an Excel workbook:  
Data Sheet: Main sheet with records of user activity and disease/variety access.  
Jodhpur_Weather & Alwar_Weather: Contain temperature/humidity and disease access data for two districts.  
Disease Index: Lists weather thresholds for disease outbreaks.  

Variables include:  

Month-Year, Week, No.of.users, Usage  
Disease columns: D1 to D11 (e.g., D6 = Leaf Curl)  
Variety columns: V1 to V10  
Micronutrient, P, F, I, etc.  

## Tools & Technologies
- R  
- Microsoft Excel  
- Data Cleaning & Management  
- Statistical Hypothesis Testing (t-test, proportion test, ANOVA)  

## Key Hypotheses Tested
 1. Leaf Curl Disease Outbreak  
Claim: Leaf Curl (D6) was accessed more than 60 times/month on average since Oct’17.  
Test: One-sample t-test  

 2. Disease Popularity  
Claim: More than 15% of disease-related accesses were for Leaf Curl.  
Test: Proportion test  

 3. User Growth Over Time  
Claim: App users significantly increased from 2015–16 to 2017–18.  
Test: Two-sample t-test (unequal variance)  

 4. Weekly Usage Patterns  
Claim: App usage differs across the 4 weeks of a month.  
Test: One-way ANOVA  

## Insights from the Analysis  

- Leaf Curl disease shows significantly higher access post-Oct'17, suggesting an outbreak.   
- >15% of all disease-related queries were for Leaf Curl, validating product diversification.  
- User base significantly grew between 2015–16 and 2017–18, indicating greater farmer adoption.  
- App usage varied significantly across weeks, hinting at time-specific behavior.  
- Tests were designed to relate disease access with weather conditions (to be explored further).  

##  Code Snapshot (R)

# Load data and filter
data4 <- read.xlsx("Chilli.xlsx", sheet = "Data Sheet")
data_filtered <- data4[95:123, ]

# Hypothesis test for Leaf Curl disease access
t.test(data_filtered$D6, mu = 60, alternative = "greater")

# Proportion test
data4$sum_of_diseases <- rowSums(data4[, 5:15])
prop.test(sum(data4$D6), sum(data4$sum_of_diseases), p = 0.15, alternative = "greater", correct = FALSE)

# Growth analysis
first_period <- data4[1:73, ]
second_period <- data4[74:123, ]
t.test(second_period$No.of.users, first_period$No.of.users, alternative = "greater", var.equal = FALSE)

# ANOVA on weekly usage
data_filtered2 <- data4[26:123, ]
anova_result <- aov(Usage ~ Week, data = data_filtered2)
summary(anova_result)


## Use Case 
This project serves as a practical example of applying data science for agricultural impact, specifically:  

Supporting data-backed decisions in agri-product planning  
Identifying temporal disease trends  
Understanding app engagement behavior  
Aligning digital interventions with farmer needs  
