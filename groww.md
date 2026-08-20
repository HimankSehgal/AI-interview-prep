# Groww — ML Engineer 📈

## Overview

Groww is one of India's fastest growing fintech platforms, known for a clean product and a sharp tech team. Their interview process is structured and tests both classical ML depth and DSA.

**Structure:** 3 rounds

| Round | Focus |
|---|---|
| Round 1 | DSA + ML Fundamentals |
| Round 2 | Classical ML Depth |
| Round 3 | Hiring Manager (Culture Fit) |

---

## 💻 Round 1 — DSA + ML Fundamentals

Two DSA questions followed by ML fundamentals.

### DSA

| Question | Difficulty | Link |
|---|---|---|
| Non Overlapping Intervals | Medium | [LC 435](https://leetcode.com/problems/non-overlapping-intervals/) |
| Minimum characters to make a string palindrome | Medium | Classic string problem |

**Non Overlapping Intervals approach:**
- Sort intervals by end time
- Greedily keep the interval that ends earliest
- Count removals needed to eliminate all overlaps
- O(n log n) time complexity

### ML Fundamentals

- What is a CNN?
- What are the advantages of CNN over a traditional neural network?
- What is Batch Normalisation?
- What is Bias Variance Tradeoff?

💡 *Tip: Groww tests classical ML fundamentals heavily. Don't go in only prepped for GenAI.*

---

## 🤖 Round 2 — Classical ML Depth

Deep dive into a classical ML project from your resume.

- Walk through your problem statement
- Which models did you use and why?
- How did you design your experiments?
- How did you do hyperparameter tuning?

### SMOTE Discussion

They asked several questions on SMOTE (Synthetic Minority Oversampling Technique):

- What does SMOTE stand for?
- When do you use it? (class imbalance problems)
- How does it work? (generates synthetic samples by interpolating between minority class examples)
- What is the difference between SMOTE and simple oversampling?

💡 *If you have worked on any imbalanced dataset problem, expect questions on how you handled class imbalance. SMOTE is a common technique that often comes up.*

---

## 👔 Round 3 — Hiring Manager

Culture fit and past experience discussion.

- Your background and motivations
- Teamwork experiences
- How do you handle conflict?
- How do you prioritize when multiple things demand attention?

---

## 🎯 Overall Takeaway

Groww is clean and structured. They balance DSA, classical ML, and culture fit across the rounds.

Key things to prepare:
- DSA — interval problems, string problems
- Classical ML fundamentals — CNN, Batch Norm, Bias Variance
- Know your classical ML projects well — hyperparameter tuning, experiment design, handling imbalanced data
- SMOTE and class imbalance techniques

---

*🔙 [Back to main repo](./README.md)*
