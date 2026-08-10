# Navi — AI Scientist 🏢

## Overview

Navi is building an AI-first fintech company. Sachin Bansal is bullish on AI and the vision is to add an AI layer across all their products — automating processes that currently involve humans.

They want people who can **move fast and get things done** over people who go very deep into theory. That philosophy reflects directly in how they interview.

One honest heads up — Navi has a reputation for being thorough to the point of being unpredictable. Even clearing all rounds doesn't guarantee an offer. Go in knowing that and focus on what you can control.

**Structure:** Screening Round → 5 onsite rounds at their Bangalore office

| Round | Focus |
|---|---|
| Screening | DSA |
| Round 1 | Prompt Engineering & RAG Design |
| Round 2 | Culture Fit |
| Round 3 | Director of AI — Resume Deep Dive |
| Round 4 | Mix of LLM Technical + Leadership |

---

## 💻 Screening Round — DSA

Two coding questions. The hard part in both was **identifying the right approach**, not just coding it.

| Question | Concept | Link |
|---|---|---|
| Allocate Minimum Pages | Binary Search | [GFG](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) |
| Coin Toss Probability | DP / Recursion with Memoization | Custom problem |

### Coin Toss Problem (detailed)

**Problem:** Given array P of size n where P[i] is probability of heads on ith toss, find probability of getting at least n/2 heads after n turns.

**Approach:**
```
get_prob(i, rem):
    if i == len(P): return 0
    total_prob = P[i] * get_prob(i+1, rem-1) + (1-P[i]) * get_prob(i+1, rem)
    return total_prob

Call: get_prob(0, n//2)
```
Memoize on (i, rem) → O(N²) solution.

💡 *Tip: For binary search problems, the hard part is identifying that binary search applies. Practice recognizing the pattern — monotonic search space, minimise the maximum or maximise the minimum.*

---

## 🤖 Round 1 — Prompt Engineering & RAG Design

I was given a problem statement: **Design a loan eligibility chatbot for Navi.**

This is not a standard ML system design — it is specifically about how you design prompts and RAG pipelines for a financial use case.

### RAG Design Questions
- How will you chunk documents for a financial RAG system?
- Which embedding model will you use and why?
- How will you store conversation history?
- How will you handle context window limits?

### Prompt Structure
The prompt for a loan eligibility system needs:

```
Role: You are a financial expert at Navi working in the loan business
Context: {company background, loan eligibility criteria via RAG}
Task: Determine if the given person is eligible for the loan they are requesting
Step by step process:
  1. Check credit history
  2. If no credit history, evaluate income status
  3. Reference RAG output for eligibility criteria
Input: {user_data}, {rag_data}
Output: {reasoning}, {verdict}, {confidence}
```

### Guardrails — Critical for Financial AI
This is what makes fintech prompting different from a restaurant chatbot:

**Before LLM:**
- Input validation — is the data complete?
- PII detection and masking
- Prompt injection detection

**After LLM:**
- Check for hallucinated figures or made up data
- Regulatory compliance check — no discriminatory reasoning
- Confidence threshold — if below threshold, route to human
- Explainability — decision must be explainable to the user

**Key risks specific to financial AI:**
- Bias in lending decisions (illegal in most jurisdictions)
- Hallucination of financial figures
- Regulatory compliance — RBI guidelines in India
- Transparency — user has right to know why they were rejected

---

## 🤝 Round 2 — Culture Fit

With someone from the founder's office. More conversational than technical.

- Walk me through your ML background — what have you built?
- What was your previous manager's feedback about you?
- How do you handle conflict at work? (Give a real example)
- How do you prioritize when multiple tasks come up?
- Why Navi?

💡 *Tip: Be honest here. They are not looking for perfect answers — they are looking for self awareness and maturity. The manager feedback question is a trap if you say "no feedback" — everyone gets feedback.*

---

## 👔 Round 3 — Director of AI

Full resume deep dive. Every project in STAR format.

- Problem statement — what were you solving?
- Approach — how did you think about it?
- Method — what did you actually build?
- Results — what was the impact?

Then LLM design decisions:
- Which LLM did you use and why?
- How did you decide between open source vs closed source?
- What guardrails did you put in place?
- How did you evaluate performance?

Know every design decision you made. They will ask why you didn't do it differently.

---

## 🔀 Round 4 — Mix Round

LLM technical questions mixed with leadership scenarios in the same round.

**Technical:**
- LLM fundamentals — fine tuning, RAG, when to use which
- Open source vs closed source tradeoffs
- How to put guardrails before and after LLM requests
- How do you evaluate an LLM in production?

**Leadership:**
- How do you handle conflicts with teammates?
- How do you handle a situation where you disagree with the approach being taken?
- How do you prioritize when everything is urgent?

---

## 🎯 Overall Takeaway

Navi covers a lot of breadth — DSA, prompt engineering, RAG, culture fit, system design, leadership. It is genuinely intense.

What helps you stand out:
- Show enthusiasm and ownership — they want people who will figure things out without hand holding
- Know your projects inside out — every decision, every tradeoff
- For the financial AI questions — show you understand the unique risks (bias, compliance, hallucination) that come with AI in fintech
- Be honest in culture fit rounds — self awareness matters more than perfect answers

---

*🔙 [Back to main repo](./README.md)*
