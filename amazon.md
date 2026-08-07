# Amazon — Applied Scientist 2 🏢

## Overview

Amazon is one of the toughest AI/ML interview loops out there. They test both **depth and breadth** — and they will find the gaps. A lot also depends on your interviewer's background. If they have worked in computer vision for years, they will go deep there. Pro tip: if you know your interviewer's name beforehand, look them up on LinkedIn and get a sense of what they have worked on.

Amazon conducts interviews on their own platform called **Amazon Chime**. Make sure your setup — camera, audio, internet — is tested at least a day before. Do not leave this for one hour before the interview.

**Structure:** Screening Round → 3 loop rounds (run in parallel, not elimination based)

| Round | Focus |
|---|---|
| Screening | Project discussion + ML fundamentals |
| Round 1 — ML Depth | Deep dive into one project, system design |
| Round 2 — ML Breadth | Broad ML/DL/LLM concepts, image processing, agentic AI |
| Bar Raiser | Leadership principles, behavioural deep dive |

Note: A DSA round may also be part of the loop depending on the role and team.

---

## 🔍 Screening Round

Project discussion first — problem statement, which LLMs were used and why.

Then straight into fundamentals. They are checking if you actually understand what you built or just ran experiments.

- Walk through your project — problem statement, approach, results
- Which LLM did you use and why?
- What is Batch Normalisation?
- What is Layer Normalisation?
- When do you use each?
- Transformer math basics — attention mechanism, Q/K/V matrices

💡 *Tip: Amazon interviews happen on their own platform called Chime/Amazon's internal interview tool. Test your setup — camera, mic, internet — at least a day before.*

---

## 🤖 Round 1 — ML Depth

This round went very deep into one specific project. My project was on finding top similar images in a database of food images using Vision Transformers.

They will pick one project from your resume and go extremely deep. Know every design decision you made and why.

### Vision Transformer & Similarity Search
- How does a Vision Transformer process images internally?
- How do you create patches from an image?
- How do you create embeddings from image patches?
- How does attention work in image transformers?
- What are Siamese Networks?
- What is triplet loss? Walk through the math
- Instead of using a deep learning model for similarity search, could you have used image hashing methods? Why or why not?

### System Design — Inventory Forecasting for Dark Stores
Design a demand forecasting model for item inventory prediction at a dark store (like Blinkit).

**How to approach this question:**

**Step 1 — Clarify scope**
- Are we forecasting at a national level, state level, or PIN code level?
- PIN code level will have high fluctuation. National level will be smooth. State level somewhere in between.
- This determines model complexity and granularity.

**Step 2 — Define inventory scope**
- Are we forecasting for all inventory or a specific category? (fruits & vegetables vs all SKUs)

**Step 3 — Understand data available**
- What historical data do we have? How far back?
- Do we have external signals — weather, festivals, local events?

**Step 4 — Baseline model**
- Start simple: average of previous 7 days demand
- This is your baseline. Everything is measured against this.

**Step 5 — Improved model (XGBoost)**
- Features to consider:
  - Previous N days demand
  - Moving averages (7 day, 30 day)
  - Current shelf capacity
  - Day of week, month, season
  - Festive calendar
  - Local population density

**Step 6 — Evaluation**
- RMSE, MAE on holdout data
- Track overstock vs understock separately — business impact is asymmetric

**Step 7 — Monitoring & Retraining**
- Monitor data distribution shift
- Monitor prediction distribution over time
- Set retraining triggers based on model drift

---

## 🔬 Round 2 — ML Breadth

This round covered a lot of ground. No single deep dive — they jumped across topics.

### Image Processing
- How do you handle image shear and distortion?
- What image preprocessing techniques did you use?

### LLMs & Prompting
- Which LLM did you use in your project and why?
- Have you worked with auto prompting / automatic prompt tuning?
- How do you decide which LLM to use?
  - Step 1: Define the type of task
  - Step 2: Evaluate cost
  - Step 3: Evaluate latency (offline vs real time)

### Agentic AI
- What is agentic AI?
- How do you define tools for an AI agent?

### Transformer Math
- Similar questions to other rounds — be consistent and thorough

💡 *Tip: A lot depends on your interviewer's background. Look them up on LinkedIn beforehand if you can. If they have worked in CV, expect depth there. If LLMs, expect depth there.*

---

## ⚖️ Bar Raiser Round

The Bar Raiser is a specially trained Amazon interviewer whose job is to maintain hiring standards across the company. This round is purely behavioural.

Amazon has 16 Leadership Principles. HR will send you the list before the interview.

📄 [Official Amazon Leadership Principles](https://www.amazon.jobs/content/en/our-workplace/leadership-principles)

**The 16 Principles:**
1. Customer Obsession
2. Ownership
3. Invent and Simplify
4. Are Right, A Lot
5. Learn and Be Curious
6. Hire and Develop the Best
7. Insist on the Highest Standards
8. Think Big
9. Bias for Action
10. Frugality
11. Earn Trust
12. Dive Deep
13. Have Backbone; Disagree and Commit
14. Deliver Results
15. Strive to be Earth's Best Employer
16. Success and Scale Bring Broad Responsibility

### How it works
They pick a project from your resume and ask which leadership principle you demonstrated. Then they dig deeper.

**The counter question will always come:**
*"That's just part of your job. What extra did you do?"*

Have a second layer ready for every story. The more specific and concrete, the better.

### Tips
- Prepare a **different story for each leadership principle** — they will ask across multiple rounds too, and repeating the same story is a red flag
- Use the STAR format — Situation, Task, Action, Result
- The action and result need to show something **beyond the obvious expectation** of your role
- Leadership principle questions can also come up in technical rounds as small questions — always be ready

---

## 🎯 Overall Takeaway

Amazon Applied Scientist interviews are genuinely tough. They cover a lot of depth and breadth, and they will probe every part of your resume.

What helps:
- Know your projects cold — every design decision, every tradeoff
- Know your fundamentals — transformer math, batch norm, layer norm, triplet loss
- Prepare your LP stories in advance with a second layer for each
- Research your interviewer's background if you can — they will go deep in their area of expertise

---

*🔙 [Back to main repo](./README.md)*
