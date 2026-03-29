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

Our team had two major RAG competition results in 2025.

First, we won the [SIGIR 2025 LiveRAG Challenge](https://sigir2025.dei.unipd.it/live-rag-challenge.html). Later, at NeurIPS 2025 MMU-RAG, our system won the **Best Dynamic Evaluation** award in the **Open Source** category for the **text-to-text** track, as described in our [MMU-RAG system paper](https://arxiv.org/abs/2602.20735).

These results came from two related systems developed in the same year: **GRAG** for LiveRAG, and **R2RAG** for MMU-RAG.

## The two results

### 1) SIGIR 2025 LiveRAG Challenge

On the [official LiveRAG challenge page](https://sigir2025.dei.unipd.it/live-rag-challenge.html), the winners are listed as:

> **First place:** RMIT-ADMS — Kun Ran, Shuoqi Sun, Khoi Nguyen Dinh Anh, Damiano Spina, Oleg Zendel

The same page states that on the live challenge day, teams had to answer a stream of unseen questions under a **two-hour** time limit, and **25 teams returned valid answers**.

The [ADM+S announcement](https://www.admscentre.org.au/arc-centre-of-excellence-team-wins-global-liverag-challenge-at-sigir-2025/) reports that the competition drew **70 teams from 27 countries**, and that during the live event teams had to answer **500 never-before-seen questions** using the same AI model and dataset.

### 2) NeurIPS 2025 MMU-RAG

A later system, **R2RAG (Routing-to-RAG)**, is described in our paper [*RMIT-ADM+S at the MMU-RAG NeurIPS 2025 Competition*](https://arxiv.org/abs/2602.20735). In that paper, the system is described as an award-winning approach for the **Text-to-Text** track, and the paper states that it won the **Best Dynamic Evaluation** award in the **Open Source** category.

The [ADM+S announcement on MMU-RAG](https://www.admscentre.org.au/mmu-rag-challenge-win/) describes this as the team’s second major RAG competition result that year. It also reports that **81 teams registered**, but only **8** submitted a fully working system.

## What we built

The second system built on ideas developed in the first.

### LiveRAG: G-RAG / GRAG

In our [LiveRAG paper](https://arxiv.org/abs/2506.14516), we described **Generation-Retrieval-Augmented Generation (GRAG)**.

The method works in three main steps:

- generate a **hypothetical answer** first,
- use that generated answer **alongside the original question** during retrieval,
- then apply **LLM-based pointwise re-ranking** before final answer generation.

As [Damiano's publication page](https://www.damianospina.com/publication/ran-2025-grag/) summarizes, the submitted system achieved the **highest Borda score**, based on aggregated manual evaluation of **Coverage, Relatedness, and Quality**, and ranked **first** in the SIGIR 2025 LiveRAG Challenge.

### MMU-RAG: R2RAG

In MMU-RAG, we extended these ideas with **Routing-to-RAG (R2RAG)**.

In the [MMU-RAG paper](https://arxiv.org/abs/2602.20735), R2RAG is described as a **research-focused RAG architecture composed of lightweight components** that dynamically adapt retrieval strategy based on:

- inferred **query complexity**, and
- **evidence sufficiency**.

The paper also states that the system uses **smaller LLMs** and can operate on **a single consumer-grade GPU**, while still supporting complex research tasks.

## Why these results matter technically

Taken together, the two systems highlight several recurring design themes:

- **retrieval quality** matters;
- **evidence use** matters;
- **evaluation design** matters;
- **latency and robustness** matter;
- and careful system design can beat brute force.

They also show a progression from a competition-winning LiveRAG pipeline to a more adaptive RAG architecture designed for dynamic evaluation settings.

## Team

These results were team efforts.

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
