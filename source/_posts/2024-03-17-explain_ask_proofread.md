---
layout: post
title: "Apple Shortcuts to boost your reading performance"
date: 2024-03-17 10:16
comments: true
categories:
- productivity
tags:
- shortcuts
---

## Background

Lately, I have been delving into papers from a new field, and I often find the sentences challenging to comprehend. Instead of searching for clarification online, which disrupts my flow and hinders my ability to follow the author's thought process, I have been trying alternative strategies.

## Proposed Shortcuts

During the process, I developed several shortcuts utilizing LLMs, These methods assisted me in explaining concepts, answering my questions, and proof-reading my writings.

⚠️ Is my api key safe? Read the README of html-gpt: https://github.com/rankun203/html-gpt.

- **🪄 Explain GPT**: https://www.icloud.com/shortcuts/8606b26b404d4e7ea340acdc89c46717 (GPT-4, updated 06/04/2024).
  - Explain selected text in plain English
- **❓ Ask GPT**: https://www.icloud.com/shortcuts/5fb876f8c50c43a79fc7288428f8a7f5 (GPT-4, updated 09/04/2024).
  - Ask a question against selected text
- **🩺 Proofread GPT**: https://www.icloud.com/shortcuts/d14760568b6b401994f2d5bc0927504f (GPT-4, updated 06/04/2024).
  - Proofread selected text in british english standard
- **🚏 Format GPT**: https://www.icloud.com/shortcuts/b7d2cf9255b7453cac80793f3e073698 (GPT-3.5, updated 06/04/2024).
  - Format selected text in JSON
- **👩‍⚕️ Google Scholar**: https://www.icloud.com/shortcuts/442a9ad20e0b42a687306c05ae594ee3 (updated 18/03/2024).
  - Search selected text in Google Scholar

You will need to obtain an OpenAI API Key to use these shortcuts. If not, you can change the shortcut config to point to another free model.

## Example usage

![Example usage of shortcuts](/images/shortcuts/ask.png)

## Original Groq Shortcuts

- **🪄 Explain**: https://www.icloud.com/shortcuts/d85ee5b1959b4d25aa64ea93827dea91 (updated 18/03/2024).
- **❓ Ask**: https://www.icloud.com/shortcuts/1f9f7f36df88458bbc194d64074748f6 (updated 18/03/2024).
- **🩺 Proofread**: https://www.icloud.com/shortcuts/3f69b404303a4b64a87ee7a61701fae4 (updated 18/03/2024).
- **🚏 Format JSON**: https://www.icloud.com/shortcuts/48b07bf9955d4636b476ba9626219c7e (updated 23/03/2024).

## Change logs

- 06/04/2024: added more sophisticated GPT-4 for tasks, streaming output
- 18/03/2024: added logging, storing all requests and responses, system prompts, into an HTML file, stored in iCloud Shortcuts folder
- 17/03/2024: initial version with Groq
