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

I still find this a bit surreal to write: our team had **two big RAG competition results in one year**.

First, we won the [SIGIR 2025 LiveRAG Challenge](https://sigir2025.dei.unipd.it/live-rag-challenge.html). Later, at NeurIPS 2025 MMU-RAG, our system won the **Best Dynamic Evaluation award in the Open Source category** for the text-to-text track, as described in our [MMU-RAG system paper](https://arxiv.org/abs/2602.20735).

As someone who spends a lot of time thinking about retrieval, evidence, and how LLM systems actually behave in realistic settings, this meant a lot to me. These competitions are not toy demos. They are messy, time-constrained, high-pressure evaluations where a system has to actually work.

## The two results

### 1) SIGIR 2025 LiveRAG Challenge

On the [official LiveRAG challenge page](https://sigir2025.dei.unipd.it/live-rag-challenge.html), the winners are listed as:

> **First place:** RMIT-ADMS — Kun Ran, Shuoqi Sun, Khoi Nguyen Dinh Anh, Damiano Spina, Oleg Zendel

The same page says that on the live challenge day, teams had to answer a stream of unseen questions under a **two-hour** time limit, and **25 teams returned valid answers**.

Like the [ADM+S announcement](https://www.admscentre.org.au/arc-centre-of-excellence-team-wins-global-liverag-challenge-at-sigir-2025/) said, the competition drew **70 teams from 27 countries**, and during the live event teams had to answer **500 never-before-seen questions** using the same AI model and dataset.

That combination is exactly why this win feels special to me. It was not just about looking good on an offline benchmark. It was about building a system that could hold up under pressure.

### 2) NeurIPS 2025 MMU-RAG

After LiveRAG, we kept going.

Our later system, **R2RAG (Routing-to-RAG)**, is described in our paper [*RMIT-ADM+S at the MMU-RAG NeurIPS 2025 Competition*](https://arxiv.org/abs/2602.20735). In that paper, we describe it as an **award-winning** system for the **Text-to-Text track**, and note that it won the **Best Dynamic Evaluation award in the Open Source category**.

Like the [ADM+S announcement on MMU-RAG](https://www.admscentre.org.au/mmu-rag-challenge-win/) said, this was the team's second big RAG competition result that year. It also mentioned something I think is very telling: **81 teams registered, but only 8 submitted a fully working system**.

That statistic says a lot. In competitions like this, ideas matter, but engineering discipline matters just as much.

## What we built

One thing I really like about this story is that the second system clearly grew out of the first.

### LiveRAG: G-RAG / GRAG

In our [LiveRAG paper](https://arxiv.org/abs/2506.14516), we described **Generation-Retrieval-Augmented Generation (GRAG)**.

The core idea was simple, but effective:

- generate a **hypothetical answer** first,
- use that generated answer **alongside the original question** during retrieval,
- then apply **LLM-based pointwise re-ranking** before final answer generation.

As [Damiano's publication page](https://www.damianospina.com/publication/ran-2025-grag/) put it, the submitted system achieved the **highest Borda score**, based on aggregated manual evaluation of **Coverage, Relatedness, and Quality**, and ranked **first** in the SIGIR 2025 LiveRAG Challenge.

### MMU-RAG: R2RAG

In MMU-RAG, we pushed the ideas further with **Routing-to-RAG (R2RAG)**.

In the [MMU-RAG paper](https://arxiv.org/abs/2602.20735), we describe R2RAG as a **research-focused RAG architecture composed of lightweight components** that dynamically adapt retrieval strategy based on:

- inferred **query complexity**, and
- **evidence sufficiency**.

What I especially like about this design is that it is not just about throwing a larger model at the problem. The paper explicitly says that the system uses **smaller LLMs** and can operate on **a single consumer-grade GPU**, while still supporting complex research tasks.

That matters to me. Efficient systems are not just cheaper. They are usually easier to reason about, easier to iterate on, and easier to reproduce.

## Why this matters to me

A lot of RAG discussion online gets trapped in shallow comparisons: which model, which embedding, which vector database, which benchmark number.

But these competition experiences kept bringing me back to the same things:

- **retrieval quality** matters;
- **evidence use** matters;
- **evaluation design** matters;
- **latency and robustness** matter;
- and careful system design can beat brute force.

I am especially proud that these systems came out of a research environment where we care about evidence-backed answers, reproducibility, and understanding *why* something works.

## Huge thanks

These results were absolutely team efforts.

For LiveRAG, the [official challenge page](https://sigir2025.dei.unipd.it/live-rag-challenge.html) lists the winning team as:

- Kun Ran
- Shuoqi Sun
- Khoi Nguyen Dinh Anh
- Damiano Spina
- Oleg Zendel

For MMU-RAG, the [paper](https://arxiv.org/abs/2602.20735) lists the authors as:

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

I feel very lucky to have worked with such a strong team.

## What’s next

Winning is fun, but to me the more interesting part is what comes after.

The real goal is not to collect trophies. It is to build RAG systems that are genuinely useful for research and real-world information seeking:

- better at deciding **when** to retrieve,
- better at deciding **what** evidence is enough,
- better at being **faithful** to sources,
- and better at operating under realistic constraints.

That is the direction I want to keep pushing.

## References

- [SIGIR 2025 LiveRAG Challenge official page](https://sigir2025.dei.unipd.it/live-rag-challenge.html)
- [ADM+S announcement on the LiveRAG win](https://www.admscentre.org.au/arc-centre-of-excellence-team-wins-global-liverag-challenge-at-sigir-2025/)
- [LiveRAG system paper / summary page](https://www.damianospina.com/publication/ran-2025-grag/)
- [MMU-RAG system paper / summary page](https://www.damianospina.com/publication/ran-2026-r2rag/)
- [ADM+S announcement on the MMU-RAG result](https://www.admscentre.org.au/mmu-rag-challenge-win/)
- [arXiv: RMIT-ADM+S at the SIGIR 2025 LiveRAG Challenge](https://arxiv.org/abs/2506.14516)
- [arXiv: RMIT-ADM+S at the MMU-RAG NeurIPS 2025 Competition](https://arxiv.org/abs/2602.20735)
