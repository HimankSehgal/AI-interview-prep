# InMobi — Applied Scientist 2 📱

## Overview

InMobi is one of the world's largest independent mobile advertising platforms. They process billions of ad requests daily across global mobile inventory. The ML problems here are genuinely hard — real time bidding, audience targeting, fraud detection, all at massive scale.

One thing to know going in: InMobi is heavily focused on **classical ML**, not LLMs. If you go in expecting to talk about GenAI, you will be caught off guard.

**Structure:** 5 rounds

| Round | Focus |
|---|---|
| Round 1 | Intro + Coding + ML Fundamentals |
| Round 2 | Coding |
| Round 3 | Applied ML System Design |
| Round 4 | ML Breadth |
| Round 5 | Hiring Manager |

---

## 🔍 Round 1 — Intro + Coding + ML Fundamentals

### Project Discussion
Walk through one of your projects in STAR format. Know your design decisions cold.

### Coding — Generate Well Formed Parentheses

**Problem:** Given integer n, generate all combinations of well formed parentheses.

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

**Approach:** Recursion with backtracking. At each step, decide whether to add an open or close bracket based on counts.

```python
result = []

def count_all_ps(curr_string, open_count, closed_count, result):
    # Base case: string is full
    if len(curr_string) == 2 * n:
        result.append(curr_string)
        return
    # Add open bracket if we haven't used all n
    if open_count < n:
        count_all_ps(curr_string + "(", open_count + 1, closed_count, result)
    # Add close bracket only if it won't make string invalid
    if closed_count < open_count:
        count_all_ps(curr_string + ")", open_count, closed_count + 1, result)

count_all_ps("", 0, 0, result)
```

### ML Fundamentals
- What is Batch Normalisation vs Layer Normalisation?
- When do you use each?
- What is Bias Variance Tradeoff?

---

## 💻 Round 2 — Coding

Three questions in this round.

### Question 1 — Find Original Array from Doubled Array

**Problem:** An array was transformed by appending twice the value of every element and shuffling. Given the resulting array, return the original.

```
Input: changed = [1,3,4,2,6,8]
Output: [1,3,4]
```

**Approach:** Sort + frequency counter

```python
from collections import Counter

def double_array(inp_array):
    if len(inp_array) % 2 != 0:
        return []
    
    count_dict = Counter(inp_array)
    ans_array = []
    inp_array.sort()
    
    for element in inp_array:
        if count_dict[element] == 0:
            continue
        elif count_dict[2 * element] != 0:
            ans_array.append(element)
            count_dict[2 * element] -= 1
            count_dict[element] -= 1
        else:
            return []
    
    return ans_array
```

### Question 2 — First Missing Positive

**Problem:** Given unsorted array, return smallest positive integer not present. O(n) time, O(1) space.

```
Input: [3,4,-1,1] → Output: 2
Input: [7,8,9,11,12] → Output: 1
```

**Approach v1 (O(n) time, O(n) space):** Counter dict, iterate 1 to n+1

**Approach v2 (O(n) time, O(1) space):** Index as hash map — swap elements to their correct positions, then find first index where value != index+1

```python
def find_num_v2(inp_array):
    n = len(inp_array)
    
    for i in range(n):
        while (inp_array[i] >= 1 and 
               inp_array[i] <= n and 
               inp_array[inp_array[i] - 1] != inp_array[i]):
            correct_pos = inp_array[i] - 1
            inp_array[i], inp_array[correct_pos] = inp_array[correct_pos], inp_array[i]
    
    for i in range(n):
        if inp_array[i] != i + 1:
            return i + 1
    
    return n + 1
```

### Question 3 — Max Stock Profit

**Problem:** Given stock prices, find maximum profit from single buy and sell.

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

---

## 🤖 Round 3 — Applied ML System Design

**Problem Statement:** InMobi operates as a Supply Side Platform (SSP). They receive millions of bid requests per second from publishers. They have ~200 Demand Side Platforms (DSPs) with varying capacity (1K to 500K requests/sec). Sending all requests to all DSPs is prohibitively expensive. How do you decide which requests to route to which DSPs to maximise revenue?

### The Core Challenge
- You cannot send all requests to all DSPs — too expensive, exceeds their capacity
- Ground truth revenue only exists for DSPs that were actually sent requests — observability problem
- Decisions need to be made in real time (100ms latency budget)

### Solution Approach

**Stage 1 — Filter: Predict probability of DSP response**
- For each request-DSP pair, predict: will this DSP respond to this request?
- Features: publisher quality, geography, device type, time patterns, historical DSP behaviour
- Model: Gradient Boosted Trees (fast inference, works well on tabular data)

**Stage 2 — Rank: Predict expected revenue given response**
- Given DSP will respond, what is the expected bid value?
- Combine: P(response) × E(revenue | response) = Expected Revenue

**Features to use:**
- Publisher signals: app category, user demographics, placement type
- DSP signals: historical response rate, average bid per category, capacity utilisation
- Contextual: time of day, geography, device OS

**Evaluation challenge:**
- Can't backtest easily — no counterfactual data for DSPs not shown requests
- Use: response rate prediction accuracy + ranking correlation on observable overlap
- A/B test in production with gradual rollout

💡 *Tip: This problem is about constrained optimisation under uncertainty. The key insight is the two stage model — filter first, then rank. Mention latency budget explicitly.*

---

## 📊 Round 4 — ML Breadth

### Recommendation Systems — Product vs Ads

**Product Recommendation Metrics:**
- Click Through Rate (CTR)
- Conversion Rate
- Revenue per recommendation
- Long term engagement (repeat purchase)

**Ads Recommendation Metrics:**
- CTR — primary metric
- Cost Per Click (CPC) / Cost Per Mille (CPM)
- Return on Ad Spend (ROAS) for advertiser
- Fill rate — % of ad slots successfully filled

Key difference: In ads, you optimise for both user relevance AND advertiser value. In product recommendations, you primarily optimise for user satisfaction and conversion.

### Batch Norm vs Layer Norm

**Batch Normalisation:**
- Normalises across the batch dimension
- Works well for CNNs and fixed batch sizes
- Problematic for small batches, RNNs, online inference

**Layer Normalisation:**
- Normalises across the feature dimension for each sample independently
- Works well for transformers, RNNs, variable length sequences
- Better for inference where batch size = 1

### Linear Regression Assumptions (and what breaks when each fails)

See [Swiggy breakdown](./swiggy.md) for full detailed answers on all 5 assumptions.

### Classical ML Questions
- Dropout — what it is, when to use it
- Regularisation — L1 vs L2, how to choose lambda
- Class imbalance — SMOTE, class weights, threshold tuning
- Probability calibration — when do you need it vs when ranking suffices

---

## 👔 Round 5 — Hiring Manager

**System Design: Article Recommendation with Embeddings**

Started simple, then complexity kept increasing:

**Base problem:** Given a corpus of articles, recommend similar articles to a user.

**Approach:**
- Generate article embeddings using sentence transformers
- Store in vector DB (FAISS, Pinecone)
- At query time, embed user's current article, retrieve top-k similar

**Complexity increases:**
- Cold start: new article with no interaction history → use content embeddings directly
- Data drift: embedding distribution shifts over time → monitor cosine similarity distributions, retrain periodically
- Evaluation without labels: use proxy metrics (CTR, dwell time), embedding space visualisation (t-SNE/UMAP), A/B testing

**Data drift detection without labels:**
- Compare embedding mean and variance between training and production data
- Use KL divergence or KS test on embedding distributions
- Sample production data and compare to training distribution statistically

---

## 🎯 Overall Takeaway

InMobi is heavy on classical ML, statistics, and system design. They are not looking for LLM expertise — they want people who understand ML fundamentals deeply.

What to focus on:
- **Classical ML** — linear regression assumptions, regularisation, class imbalance, calibration
- **Statistics** — bias variance tradeoff, batch norm vs layer norm
- **System design** — real time ML systems, latency constraints, evaluation under observability challenges
- **Ad tech domain** — understand RTB, DSPs, SSPs at a high level
- **Coding** — medium to hard DSA, frequency counters, index based tricks

---

*🔙 [Back to main repo](./README.md)*
