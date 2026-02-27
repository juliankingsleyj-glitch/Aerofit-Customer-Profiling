# Consumer Demographics & Probability Profiling: Aerofit

# Summary
This project utilizes descriptive statistics and probability theory to construct detailed customer profiles for a leading fitness equipment brand. By analyzing demographic metrics (income, age, education) and behavioral metrics (expected usage, fitness level) using Python, the analysis predicts consumer purchasing behavior across three distinct product tiers. The insights generated enable highly targeted marketing campaigns and optimized product recommendation engines.

# Business Problem
Aerofit sells three treadmills: the entry-level KP281, mid-level KP481, and premium KP781. The marketing and sales teams were struggling to recommend the correct product to incoming customers, resulting in lost upsell opportunities and inefficient marketing spend. The objective was to:
Perform Exploratory Data Analysis (EDA) to find correlations between customer traits and product choice.
Use Marginal and Conditional Probabilities to calculate the likelihood of a specific customer buying a specific treadmill.
Deliver actionable customer profiles to the sales team.

# Technical Stack
Language: Python 3
Data Manipulation: Pandas, NumPy
Statistical Analysis: Descriptive Statistics, Outlier Detection, Probability Matrices (Cross-tabulation)
Data Visualization: Seaborn, Matplotlib (Boxplots, Heatmaps, Countplots)

# Part 1: Descriptive Analytics & Customer Profiling
To understand the data, I first conducted Univariate and Bivariate analysis to see how variables like Income and Fitness Level affected product choice.

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

- Load dataset
df = pd.read_csv('Aerofit_treadmill.csv')

- Bivariate Analysis: Income vs Product Purchased
plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='Product', y='Income', palette='Set2')
plt.title('Income Distribution by Product Tier')
plt.show()

- Insight: The boxplot analysis revealed a massive income disparity. The premium KP781 is exclusively purchased by customers with an annual income greater than $70,000, whereas the KP281 and KP481 have heavily overlapping income distributions clustered around $45,000 - $55,000.

# Part 2: Probability Matrices (Marginal & Conditional)
Instead of guessing what a customer might buy, I used Cross-Tabulation to calculate the exact mathematical probability of a purchase based on gender and fitness level.
Marginal Probability (Overall Likelihood):

# What is the overall probability of a customer buying the premium KP781?
product_counts = df['Product'].value_counts(normalize=True) * 100
print(product_counts)
Result: Only 22% of all customers buy the premium KP781. 44% buy the entry-level KP281.

Conditional Probability (Likelihood Given a Condition):

- GIVEN that a customer rates their fitness a 5/5, what is the probability they buy the KP781?
contingency_table = pd.crosstab(df['Fitness'], df['Product'], normalize='index') * 100
print(contingency_table)
Result: If a customer rates their fitness as a 5 (Excellent), there is a 95% probability they will purchase the premium KP781 treadmill.

# Strategic Recommendations

- Targeted Upselling: Sales associates should immediately ask new customers for their "expected weekly mileage" and "self-rated fitness." If a customer states they plan to run >100 miles/week or rates their fitness a 4 or 5, the associate should bypass the entry-level models and pitch the premium KP781 exclusively.
- Marketing Allocation: Demographic profiling shows the KP781 is highly popular among the 24-29 age group with 16+ years of education (College Graduates). Recommend partnering with university alumni networks and premium local gyms for targeted digital ad placement.
- Entry-Level Positioning: The KP281 is predominantly purchased by beginners with lower usage expectations (<3 times a week). Marketing for this product should focus on "ease of use" and "starting your fitness journey" rather than high-performance metrics.
