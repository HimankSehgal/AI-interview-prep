# Swiggy — Data Scientist 2 🍔

## Overview

Swiggy has one of the more well rounded interview processes out there. They test product thinking, coding, ML breadth, and ML depth — all in one loop. Unlike most companies that focus on one or two areas, Swiggy wants to see the full picture.

I made it till Round 4 but couldn't clear it. My maths fundamentals were weak at that point and that showed in the breadth round.

**Structure:** 5 rounds

| Round | Focus |
|---|---|
| Round 1 | Product Thinking |
| Round 2 | Coding (SQL + Python + Pandas) |
| Round 3 | ML Breadth |
| Round 4 | ML Depth |
| Round 5 | Hiring Manager |

---

## 🧠 Round 1 — Product Thinking

This round is different from most DS interviews. They give you a real product scenario and test how you think from a user and business perspective — not just an ML perspective.

**What was asked:**

I was given a scenario based on my own project — attribute verification using LLMs for seller onboarding. The question was: if you automate this process, how will you present it to the seller?

**My approach:**

- LLM processing takes ~1 minute but show the seller a 5 minute estimated completion time (buffer for edge cases)
- Show a progress indicator (loading circle) so the seller knows something is happening
- On success: show "everything matched" confirmation
- On failure: show "some issues found, our team will contact you within 24 hours" so the seller knows whether to wait on the platform or not

**What they are really testing:**

- Can you think about the end user experience, not just the model?
- Do you think about edge cases and failure states?
- Can you translate ML outputs into something a non-technical user understands?

💡 *Tip: For product thinking rounds, always think in three layers — happy path, failure path, and what the user feels at each step.*

---

## 💻 Round 2 — Coding

Three questions covering SQL, Python, and Pandas.

### SQL — Delivery Executive Earnings

**Table: de_earnings**

| de_id | date | order_id | earnings |
|---|---|---|---|
| 1 | 2024-01-01 | 1 | 50 |
| 1 | 2024-01-01 | 2 | 45 |
| 1 | 2024-01-02 | 3 | 35 |
| 2 | 2024-01-01 | 5 | 30 |

**Question:** Write a SQL query that outputs all columns plus an additional column `total_earnings` showing total earnings for each de_id and date.

**Answer:**
```sql
SELECT 
    de_id,
    date,
    order_id,
    earnings,
    SUM(earnings) OVER (PARTITION BY de_id, date) AS total_earnings
FROM de_earnings;
```

Concept tested: Window functions — SUM OVER PARTITION BY.

---

### Python — Maximum Stock Profit

**Question:** Given a list of stock prices, find the maximum profit from a single buy and sell.

**Answer:**
```python
def get_max_profit(stock_prices):
    min_val = stock_prices[0]
    max_profit = 0
    for price in stock_prices[1:]:
        candidate_val = price - min_val
        min_val = min(min_val, price)
        max_profit = max(max_profit, candidate_val)
    return max_profit
```

O(n) time, O(1) space. Track minimum seen so far and max profit at each step.

---

### Pandas — Transaction Ranking

**Question:** Given a transactions dataframe, add a `transaction_rank` column ranking transaction amounts in descending order separately for each customer.

```python
df['transaction_rank'] = df.groupby('customer_id')['transaction_amount'].rank(ascending=False, method='dense')
```

Concept tested: groupby + rank with ascending=False for descending order.

---

## 📊 Round 3 — ML Breadth

This round covers a lot of ground across statistics and classical ML. Don't underestimate it — this is where weak fundamentals will catch you.

### Statistics

**Central Limit Theorem**
As sample size increases, the distribution of sample means approaches a normal distribution regardless of the population distribution. Practically useful for hypothesis testing and confidence intervals.

**Bayes Theorem and Conditional Probability**
P(A|B) = P(B|A) * P(A) / P(B)
Used in spam detection, medical diagnosis, recommendation systems.

**A/B Testing**
- Define null hypothesis (no difference between A and B)
- Choose significance level (typically 0.05)
- Run experiment, collect data
- Calculate p-value
- If p-value < significance level, reject null hypothesis
- Key things to watch: sample size, test duration, multiple testing problem

**Bias Variance Tradeoff**
- High bias = underfitting, model too simple
- High variance = overfitting, model too complex
- Goal: find the sweet spot that minimises total error

### Linear Regression — 5 Assumptions and What Happens When Each Breaks

**1. Linearity** — relationship between X and Y is linear
- If breaks: model predictions are systematically wrong, residuals show patterns
- Fix: feature transformation, polynomial features, use non-linear model

**2. Independence of errors** — residuals are independent of each other
- If breaks: standard errors are underestimated, confidence intervals are wrong
- Common in time series data (autocorrelation)
- Fix: add lag features, use time series models

**3. Homoscedasticity** — constant variance of residuals across all values of X
- If breaks: predictions are less reliable for certain ranges, standard errors are biased
- Fix: log transform the target variable, weighted least squares

**4. Normality of residuals** — residuals are normally distributed
- If breaks: p-values and confidence intervals are unreliable
- Fix: transform features or target, use robust regression
- Note: less important with large sample sizes due to CLT

**5. No multicollinearity** — independent variables are not highly correlated with each other
- If breaks: coefficients become unstable and hard to interpret, large standard errors
- Fix: remove correlated features, use PCA, use regularisation (Ridge)

### Classical ML

**CNN vs Traditional ANN**
- CNN uses convolutional layers that share weights across the image
- Captures spatial patterns (edges, textures, shapes) that ANN cannot
- Parameter efficient — fewer parameters than a fully connected network for images
- Translation invariant — recognises patterns regardless of where they appear

---

## 🤖 Round 4 — ML Depth

Deep dive into LLM fundamentals and your projects. They go very deep here — know every decision you made and why.

### LLM Questions

- Fine tuning vs prompt tuning — when to use what?
  - Prompt tuning: task is well defined, data is limited, speed matters
  - Fine tuning: task specific behaviour needed, you have enough labelled data, prompt tuning isn't working
- How do you decide which LLM to use?
  - Task type → cost → latency
- Was your training data representative of real world data? How did you ensure that?
- Did you do manual prompting or auto prompting? Why?

### Transformer Math

- What is the attention matrix?
- What are Q, K, V matrices and what do they represent?
- Mathematical formula: Attention(Q,K,V) = softmax(QKᵀ/√d) × V
- Why divide by √d?
- How do transformers process images? (patch embeddings, ViT approach)

### YOLO

- What is YOLO and what problem does it solve?
- What are bounding boxes?
- How does YOLO predict bounding boxes? (grid cells, anchor boxes, confidence scores)
- Loss function in YOLO — localisation loss + confidence loss + classification loss

---

## 👔 Round 5 — Hiring Manager

Culture fit, past experiences, teamwork, conflict resolution, prioritization.

---

## 🎯 Overall Takeaway

Swiggy tests everything — product thinking, SQL, Python, Pandas, statistics, classical ML, deep learning, LLMs. Breadth is the key differentiator here.

What to focus on:
- **Product thinking** — practice thinking about user experience and failure states, not just model accuracy
- **SQL window functions** — SUM OVER PARTITION BY, RANK OVER PARTITION BY
- **Pandas** — groupby, rank, rolling windows
- **Maths fundamentals** — linear regression assumptions, CLT, Bayes, A/B testing
- **LLM depth** — fine tuning vs prompt tuning, know your design decisions cold
- **YOLO** — if it is on your resume, know the math

---

*🔙 [Back to main repo](./README.md)*
