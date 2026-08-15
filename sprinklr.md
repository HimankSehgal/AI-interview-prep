# Sprinklr — Product Engineer (ML) 🏢

## Overview

Sprinklr works with some of the world's biggest brands on customer experience at scale — Microsoft, P&G, Samsung, 50%+ of Fortune 100. The interview reflects that — they want people who can think, research, build, and ship.

I made it to Round 3 but didn't clear it. In hindsight I could have structured my system design answer better — but that's what these experiences teach you.

**Structure:** 4 rounds

| Round | Focus |
|---|---|
| Round 1 | Project Discussion |
| Round 2 | System Design + Python Internals |
| Round 3 | Applied GenAI System Design |
| Round 4 | Product and Leadership |

---

## 🔬 Round 1 — Project Discussion

They picked two projects from my resume and went very deep. Full STAR format expected — problem, approach, experiments, outcomes, improvements.

**Project discussed: OCR using Gemini for attribute extraction (Blinkit)**

Questions asked:
- What was the problem you were solving?
- Which LLM did you use and why?
  - Answer framework: task type → cost → latency → accuracy
- What experiments did you run?
- What were the outcomes? How much cost or time did you save?
- What challenges did you face and how did you improve?

💡 *Tip: Don't just describe what you built. They want numbers — how much did it improve, how much did it save. Prepare those before the interview.*

---

## 💻 Round 2 — System Design + Python Internals

Two parts in this round.

### Python Internals
- Why is Python slow? What runs underneath it?
- Why is Python written in C?
- Why are all ML libraries (NumPy, TensorFlow, PyTorch) written in Python but execute in C/C++?
- What are Python kernels?

**The answer in brief:**
Python is an interpreted language with a GIL (Global Interpreter Lock) that makes it slow for computation. ML libraries expose a Python API but the heavy computation runs in optimised C/C++ underneath. This gives you Python's ease of use with C's speed.

### System Design
A game design question involving priority queues as a data structure. Classic problem — search "game leaderboard design priority queue" for similar problems.

---

## 🤖 Round 3 — Applied GenAI System Design

This was the most interesting round. Open ended, real world problem.

**Problem Statement:**
You are onboarding new customer care agents at Zomato. You have 10,000 unlabeled conversation transcripts. How do you use this data to:
1. Define training categories/scenarios
2. Train agents on how to respond
3. Evaluate whether their responses are correct

**The challenge:** You have no labels. Just raw conversation text.

### Full Solution Approach

**Step 1 — Topic Discovery (unsupervised)**

Since data is unlabeled, use topic modelling to discover categories automatically.

Options:
- **TF-IDF + Clustering** — simple, fast, good baseline
- **LDA (Latent Dirichlet Allocation)** — probabilistic topic model, gives word distributions per topic
- **BERTopic** — modern approach using embeddings + clustering, better semantic understanding

```
Pipeline:
Raw conversations → Preprocessing → TF-IDF / Embeddings → 
Clustering (K-means / HDBSCAN) → Topic Labels
```

Example topics that might emerge:
- Payment failure
- Food quality issues
- Late delivery
- Wrong order delivered
- Refund requests

**Step 2 — Filter quality conversations**

Not all conversations are good training data. Filter for successfully resolved ones:
- Keyword signals: "thank you", "resolved", "received"
- No escalation signals: "manager", "complaint", "still waiting"
- Conversation length: 4-15 turns (too short = unresolved, too long = escalated)
- Sentiment of last customer message: positive = resolved

**Step 3 — Build training interface**

For each topic cluster:
- Show agent a customer message from that category
- Agent types their response
- Evaluate response quality

**Step 4 — Evaluation (the hard part)**

How do you know if the agent's response was correct with no labels?

Options:
- **Semantic similarity** — compare agent response to top golden responses from the cluster using cosine similarity on embeddings
- **Keyword matching** — does the response contain the right resolution keywords for that category?
- **LLM as judge** — use an LLM to evaluate whether the response appropriately addresses the customer issue

**Post processing:**
Handle text normalisation — "Payment" vs "payment" vs "PAYMENT" should all map to the same category. Simple lowercasing + stemming handles this.

💡 *What I should have answered more clearly: The key insight is that this is an unsupervised problem first — discover categories, then build evaluation around those categories. The interviewer was testing whether you reach for topic modelling when you have unlabeled text data.*

---

## 👔 Round 4 — Product and Leadership

- Translating research into shipped features
- Roadmap prioritisation and stakeholder management
- Defining success metrics and measuring impact
- Cross functional leadership examples

---

## 🎯 Overall Takeaway

Sprinklr goes deep on both research thinking and product thinking. They want someone who can take an idea from paper to production and measure the impact.

What to focus on:
- Know your projects with exact numbers — cost savings, accuracy improvements, throughput
- Python internals are fair game — understand what runs under the hood
- For system design — always clarify if data is labeled or unlabeled. It completely changes your approach.
- When you don't know something, reason through it out loud — they value thought process over memorised answers

---

*🔙 [Back to main repo](./README.md)*
