---
layout: post
title: "Two RAG wins in one year: LiveRAG and MMU-RAG"
date: 2026-03-25 19:25
comments: true
categories:
- research
tags:
- rag
- liverag
- mmu-rag
- neurips
- sigir
- rmit
- adms
---

It still feels a bit unreal to write this: our team won **two international RAG competitions in one year**.

First, we won the **SIGIR 2025 LiveRAG Challenge**. Then we followed it up at **NeurIPS 2025 MMU-RAG**, where our system won **the Best Dynamic Evaluation award in the Open Source category** for the text-to-text track.

For anyone working in retrieval, ranking, and LLM systems, this kind of result is deeply satisfying. These competitions are not toy demos. They test whether your system can survive contact with messy, time-constrained, real evaluation settings.

## The two wins

### 1) SIGIR 2025 LiveRAG Challenge

According to the official challenge page, the winners of the LiveRAG Challenge were:

> **First place:** RMIT-ADMS — Kun Ran, Shuoqi Sun, Khoi Nguyen Dinh Anh, Damiano Spina, Oleg Zendel

The official SIGIR 2025 LiveRAG page also notes that during the live challenge day, teams had to answer a stream of unseen questions under a **two-hour** time limit, and **25 teams returned valid answers**.

The ADM+S announcement adds more context: the competition drew **70 teams from 27 countries**, and during the live event teams had to answer **500 never-before-seen questions** using the same AI model and dataset.

That combination is exactly why this result means so much to me: it was not just about getting a model to look good offline. It was about building a system that could perform under pressure.

### 2) NeurIPS 2025 MMU-RAG

After LiveRAG, we kept pushing.

Our later system, **R2RAG (Routing-to-RAG)**, was described in the paper *RMIT-ADM+S at the MMU-RAG NeurIPS 2025 Competition*. The paper describes it as an **award-winning** system for the **Text-to-Text track** and states that it won the **Best Dynamic Evaluation award in the Open Source category**.

The ADM+S announcement summarised the outcome even more plainly: our RMIT team won **first prize** at the international MMU-RAG challenge. It also notes how tough the competition was: **81 teams registered, but only 8 submitted a fully working system**.

That stat says a lot. In these evaluations, ideas matter, but engineering discipline matters just as much.

## What we built

One of the most fun parts of this journey is that the second system clearly grew out of the first.

### LiveRAG: G-RAG / GRAG

In our LiveRAG paper, we described **Generation-Retrieval-Augmented Generation (GRAG)**. The key idea was simple but effective:

- generate a **hypothetical answer** first,
- use that generated answer **alongside the original question** during retrieval,
- then apply **LLM-based pointwise re-ranking** before final answer generation.

The paper reports that this system achieved the **highest Borda score**, based on aggregated manual evaluation of **Coverage, Relatedness, and Quality**, and ranked **first** in the SIGIR 2025 LiveRAG Challenge.

### MMU-RAG: R2RAG

In MMU-RAG, we extended the ideas further with **Routing-to-RAG (R2RAG)**.

The paper describes R2RAG as a **research-focused RAG architecture composed of lightweight components** that dynamically adapt retrieval strategy based on:

- inferred **query complexity**, and
- **evidence sufficiency**.

What I especially like about this design is that it is not just about throwing a larger model at the problem. The paper explicitly highlights that the system uses **smaller LLMs** and can operate on **a single consumer-grade GPU**, while still supporting complex research tasks.

That matters. Efficient systems are not just cheaper; they are easier to reason about, easier to iterate on, and often more reproducible.

## Why this matters to me

A lot of RAG discussion online gets trapped in shallow comparisons: which model, which embedding, which vector database, which benchmark number.

But these competition experiences reminded me what actually matters:

- **retrieval quality** matters;
- **evidence use** matters;
- **evaluation design** matters;
- **latency and robustness** matter;
- and careful system design can beat brute force.

I am especially proud that these systems were built in a research environment where we care about evidence-backed answers, reproducibility, and understanding *why* something works.

## Huge thanks

These results were team efforts.

For LiveRAG, the winning team listed on the official SIGIR page was:

- Kun Ran
- Shuoqi Sun
- Khoi Nguyen Dinh Anh
- Damiano Spina
- Oleg Zendel

For the MMU-RAG competition paper, the authors are:

- Kun Ran
- Marwah Alaofi
- Danula Hettiachchi
- Chenglong Ma
- Khoi Nguyen Dinh Anh
- Khoi Vo Nguyen
- Sachin Pathiyan Cherumanal
- Lida Rashidi
- Falk Scholer
- Damiano Spina
- Shuoqi Sun
- Oleg Zendel

I feel lucky to have worked with such a strong team.

## What’s next

Winning is fun, but the more interesting part is what comes after.

The real goal is not to collect trophies. It is to build RAG systems that are genuinely useful for research and real-world information seeking:

- better at deciding **when** to retrieve,
- better at deciding **what** evidence is enough,
- better at being **faithful** to sources,
- and better at operating under realistic constraints.

That is the direction I want to keep pushing.

## Sources

- SIGIR 2025 LiveRAG Challenge official page: https://sigir2025.dei.unipd.it/live-rag-challenge.html
- ADM+S announcement on LiveRAG win: https://www.admscentre.org.au/arc-centre-of-excellence-team-wins-global-liverag-challenge-at-sigir-2025/
- LiveRAG system paper / summary page: https://www.damianospina.com/publication/ran-2025-grag/
- MMU-RAG system paper / summary page: https://www.damianospina.com/publication/ran-2026-r2rag/
- ADM+S announcement on MMU-RAG win: https://www.admscentre.org.au/mmu-rag-challenge-win/
- arXiv: RMIT-ADM+S at the SIGIR 2025 LiveRAG Challenge: https://arxiv.org/abs/2506.14516
- arXiv: RMIT-ADM+S at the MMU-RAG NeurIPS 2025 Competition: https://arxiv.org/abs/2602.20735
