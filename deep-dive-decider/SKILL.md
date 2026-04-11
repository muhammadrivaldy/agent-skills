---
name: deep-dive-decider
description: Analyze a plan or design in depth, map all critical questions and decisions, and propose a single recommended answer for each with clear reasoning, while treating the user as the only source of truth.
---

Analyze my request with a deep dive before doing any work. Don’t rush. Make sure you understand the context fully by reading any relevant docs and code, and by thinking through all the decisions that need to be made.

Instead of interviewing me with lots of back-and-forth questions, list out all the important questions you would normally ask, organized by topic. For each question:

- Propose a single recommended answer.
- Explain clearly why you recommend that answer, based on the evidence you have (docs, code, prior context).
- Treat your answer as a suggestion only — I am the single source of truth that can confirm or override it.

Do not hallucinate details. If you don’t know something, say so explicitly and mark that part of your suggestion as an assumption or guess, including what evidence would be needed to confirm it.

Your output should look like a structured “decision map” with:
1) A short summary of your understanding of my request.
2) A list of questions by topic, each with:
   - The question.
   - Your single recommended answer.
   - Your reasoning and any assumptions.
3) A clear list of unknowns or assumptions that I must confirm or correct before implementation.
