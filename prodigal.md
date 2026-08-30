# Prodigal — Data Scientist 🎯

## Overview

Prodigal is a consumer finance intelligence company. They analyze debt collection calls to predict consumer disposition outcomes and help agents improve their performance. The interview process is one of the most elaborate I went through — 6 rounds including a full take-home assignment.

Fair warning: the process is very long and they take their time at every stage.

**Structure:** 6 rounds

| Round | Focus |
|---|---|
| Round 1 | Intro + Background |
| Round 2 | Coding |
| Round 3 | Puzzles |
| Round 4 | Assignment Discussion 1 |
| Round 5 | Assignment Discussion 2 |
| Round 6 | CEO Round |

---

## 🔍 Round 1 — Intro (30 mins)

Very conversational. No technical questions.

- Walk through your background
- What does Prodigal do? (Know this before going in — they analyze debt collection calls using AI)
- Are you open to relocation?
- Why do you want to join Prodigal?

💡 *Tip: Understand their core product before the intro. They work specifically in consumer finance call analysis — it's a niche domain and showing awareness signals genuine interest.*

---

## 💻 Round 2 — Coding

Two questions.

### Question 1 — Number of Islands

Same as [LC 200](https://leetcode.com/problems/number-of-islands/) — graph traversal using DFS/BFS.

```python
def num_islands(grid):
    def dfs(i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]):
            return
        if grid[i][j] != '1':
            return
        grid[i][j] = '0'
        dfs(i+1, j); dfs(i-1, j); dfs(i, j+1); dfs(i, j-1)
    
    count = 0
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                dfs(i, j)
                count += 1
    return count
```

### Question 2 — Binary Search (Server Min Time)

Classic binary search problem reframed as: given a set of servers each taking different time, find the minimum time to complete N tasks.

Similar to: [LC 875 — Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) or [LC 1011 — Capacity to Ship Packages](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

**Key insight:** Binary search on the answer — search on "time", check if all tasks can be completed within that time.

---

## 🧩 Round 3 — Puzzles

Two puzzles.

### Puzzle 1 — 8 Balls, 1 Heavier

**Problem:** You have 8 balls, one is heavier. Find the heavy ball in minimum weighings using a balance scale.

**Answer:** 2 weighings minimum.

- Weigh 3 vs 3
  - If one side heavier: take those 3, weigh 1 vs 1 (heavier one found, or third is heavy)
  - If balanced: heavy ball is in remaining 2, weigh 1 vs 1

**Extension:** What if you don't know whether the odd ball is heavier or lighter?

- Now you need 3 weighings minimum
- Split into 3 groups of 3
- First weighing tells you which group, subsequent weighings narrow down and identify heavier/lighter

### Puzzle 2 — Triangle Probability

**Problem:** Three ants are placed on corners of a triangle. Each randomly picks a direction to walk along an edge. What is the probability they don't collide?

**Answer:** P(no collision) = 2/8 = 1/4

- Each ant has 2 choices (clockwise or anticlockwise) → 2³ = 8 total combinations
- No collision only if all go clockwise OR all go anticlockwise → 2 favourable outcomes
- P = 2/8 = 0.25

---

## 📊 Round 4 & 5 — Assignment Discussion

Prodigal gives a take-home assignment before these rounds.

**The assignment:** Sentiment classification on debt collection call transcripts.

- 2000 call transcripts with agent and borrower utterances
- Task: Build sentiment scores for agent and borrower
- Predict consumer disposition outcomes (0-6 scale)

### What I built

**Feature engineering approach:**
- Agent sentiment features: payment commitment language, dispute handling, empathy signals
- Borrower sentiment features: resistance level, engagement, payment intent signals
- Used Twitter-RoBERTa for turn-level sentiment
- 70+ engineered features across 3 categories
- Ridge regression for interpretable weights

**Key finding:** Domain-specific keywords (payment commitment language, dispute words) were 3x more predictive than generic sentiment scores.

**Strongest predictor:** Agent dispute words (coefficient -0.77)

### Deep dive questions asked

**On the approach:**
- Why did you choose Ridge regression over other models?
- Your composite scores had weak correlation (r=0.143 agent, r=-0.011 borrower) — why?
- How would you improve the sentiment scoring?

**On improvements:**
- Use LLM as feature extractor — prompt for structured features per turn
- Fine-tune domain-specific transformer on collections language
- Phase-aware sentiment — negative sentiment during negotiation ≠ bad outcome
- Recency weighting — later turns matter more than earlier ones

**On classical ML:**
- What is bagging vs boosting?
- What is the difference between Random Forest and XGBoost?
- How do you handle class imbalance?
- Overfitting — how do you detect and handle it?

**On transformers:**
- Attention mechanism math
- Why do transformers work better than RNNs for longer sequences?
- What is fine-tuning vs prompting?

💡 *Tip: Know your assignment cold. Every design decision you made will be questioned. Have a second layer ready — what you would do differently.*

---

## 👔 Round 6 — CEO Round

Breadth oriented. CEO wanted to understand the variety of things you've worked on.

- Walk through different types of projects — research vs production
- Graph Neural Networks — what is your paper about? Walk through the approach
- What is bagging? What is boosting? What is the difference?
- Classical ML — feature engineering, model selection, evaluation
- Broad discussion on where you see AI going

💡 *Tip: This round is more of a conversation. The CEO is evaluating whether you can think broadly and communicate clearly, not just whether you know specific algorithms.*

---

## 🎯 Overall Takeaway

Prodigal has one of the most thorough processes I went through. If you make it to the assignment stage — take it seriously. The assignment discussion rounds go very deep into every decision you made.

What to focus on:
- **The assignment** — this is the centrepiece of the process
- **Classical ML depth** — bagging, boosting, Random Forest, XGBoost, class imbalance
- **Logical puzzles** — 8 balls problem, probability puzzles
- **Your projects inside out** — every number, every design decision

---

*🔙 [Back to main repo](./README.md)*
