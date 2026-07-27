# Microsoft — Applied Scientist 2 🏢

## Overview

Ek cheez jo Microsoft ko baaki companies se alag karti hai — they test your **intuition**, not just your knowledge. The field is vast and they know that. They want to see how you think and build up, not just what you've memorised.

**Structure:** Screening Round → 4 Loop Rounds (all 4 happen, it's not elimination based)

| Round | Focus |
|---|---|
| Screening | Research paper deep dive + coding |
| Round 1 — DSA | 3 coding questions, brute force to optimal |
| Round 2 — Statistics | Stats fundamentals, linear regression, hypothesis testing |
| Round 3 — ML Depth | Transformers, VLMs, project deep dive |
| Round 4 — Hiring Manager | Behavioural, SQL, role discussion |

---

## 🔍 Screening Round

Microsoft started with a deep dive into my research paper on distilling Graph Transformers into simple MLPs. This was not a surface level discussion — they went into the math, the motivation, and the results. If you have published work, know it inside out.

📄 Paper: [Distilling Graph Transformers into Simple MLPs](https://openreview.net/forum?id=OSPc92gD7k)

### Research Paper Questions
- What is a Graph Neural Network?
- What is a Graph Transformer?
- What are the current problems in Graph Transformers? (N² complexity)
- What was the motivation to distill a Graph Transformer into an MLP?
- Walk through your approach and end results
- Why distill into MLP? (inference speed, deployment simplicity)

### Attention Mechanism
- What are Query, Key, Value matrices?
- What is the mathematical formula for self attention? (Q×Kᵀ / √d × V)
- Why do we divide by √d?
- What is Softmax and where is it used?

### Deep Learning Fundamentals
- What is Batch Normalisation vs Layer Normalisation?
- When do you use each?
- What is Gradient Vanishing and Gradient Explosion?
- How do you deal with both?

### Coding
- First non recurring character in a string

---

## 💻 DSA Round

Focus was not just on getting the correct answer — they wanted to see how you build your approach from brute force to optimal and how you dry run on test cases. Sochne ka tarika matters as much as the final solution.

| Question | Difficulty | Link |
|---|---|---|
| Valid Anagram | Easy | [LC 242](https://leetcode.com/problems/valid-anagram/) |
| Minimum Number of Taps to Open to Water a Garden | Hard | [LC 1326](https://leetcode.com/problems/minimum-number-of-taps-to-open-to-water-a-garden/) |
| Minimum Insertion Steps to Make a String Palindrome | Hard | [LC 1312](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/) |

---

## 📊 Statistics Round

This round catches a lot of people off guard. Most AI/ML folks skip statistics prep assuming it won't come up. It does. Prepare karo.

- What is a t-test?
- What is p-value?
- How do you carry out hypothesis testing? (null hypothesis → test → conclusion)
- What is Central Limit Theorem?
- What are the 5 assumptions of Linear Regression?
- What happens when each assumption breaks?
- How do you derive the loss function of Linear Regression?
- What is R² score?
  - What does it mean if R² < 0?
  - What does it mean if R² > 1?

---

## 🤖 ML Depth Round

This round had two parts — core ML/DL theory and a deep dive into projects. My project at Blinkit involved extracting attributes from product images uploaded on the platform. The discussion went into every design decision I made.

### Transformers & Attention
- What is the attention matrix? Walk through the math
- What is BERT? What is GPT? How are they different?
- How do you handle image and text data together in a transformer?
- How do you tokenize images for a transformer? (Patch embeddings — ViT approach)
- Why do we need multiple attention heads?

### Project Discussion
- Walk through your problem statement
- Why did you use Gemini models? (Better at image reasoning tasks)
- Which Gemini model did you use and why?
- How do you decide which LLM to use?
  - Step 1: Define the type of task
  - Step 2: Evaluate cost
  - Step 3: Evaluate latency (offline vs real time)

### General Discussion
- Where is the ML field heading?
- How do you define tools for AI agents?

---

## 👔 Hiring Manager Round (Director Level)

This was honestly the best round. Very senior, very humble. It felt more like a genuine conversation than an interview — about the team, the culture, role expectations, and where Dynamics 365 is headed with agents. Be yourself here. Ask real questions.

### SQL / Database
- Basic database filtering and matching questions
- Be comfortable with joins, aggregations, and simple filtering logic

### Behavioural
- How do you handle disagreements with your manager?
- What feedback did your previous manager give you and how did you implement it?

### Role & Culture Discussion
- What are the day to day responsibilities of the role?
- How are agents being introduced at Dynamics 365?
- What are your expectations from this role?

💡 *Tip: This round is as much about you evaluating them as them evaluating you. Ask genuine questions. Show curiosity about the team and the product.*

---

## 🎯 Overall Takeaway

Microsoft focuses on **intuition over exact knowledge**. They understand the field moves fast and nobody knows everything. What they want to see is whether you can think clearly, reason through problems, and build things.

And honestly — the interviewers were kind. Every round felt like a conversation, not a viva. They encouraged rather than grilled. That genuinely made a difference.

---

*🔙 [Back to main repo](./README.md)*
