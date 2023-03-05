# [atet](https://github.com/atet) / [**_llm_**](https://github.com/atet/llm/blob/main/README.md#atet--llm)

[![.img/logo_llm.png](.img/logo_llm.png)](#nolink)

# Introduction to Large Language Models

This introduction covers what is absolutely necessary to get you up and running to host [_large language models_](https://en.wikipedia.org/wiki/Wikipedia:Large_language_models) like OpenAI GPT, Google T5, and other models on your own computer.

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Examples](#1-examples)
* [2. Installation](#2-installation)
* [3. Next Steps](#3-next-steps)

### Supplemental

* [Other Resources](#other-resources)
* [Troubleshooting](#troubleshooting)
* [Sources](#sources)

--------------------------------------------------------------------------------------------------

## 0. Requirements

The general rules of thumb as of 2023Q1 so that you spend less time troubleshooting and more time using these models:
* Have more RAM and VRAM than you think you need
* Load entire language model on the GPU VRAM
* Use an Nvidia GPU

The following tutorials will require:

* **Software**: This tutorial was developed on Microsoft Windows 10 with Windows Subsystem for Linux
* **Hardware**: The size of the large language model you can run is dependent on the amount of GPU VRAM **and** system RAM you have:

Model | Size Variant | Required System RAM | Required VRAM | Example Desktop GPU
--- | --- | --- | --- | ---
EleutherAI GPT-Neo | 125 Million Parameter (125M) | 4 GB | 2 GB | Nvidia GeForce GTX 1650
EleutherAI GPT-Neo | 1.3 Billion Parameter (1.3B) | 12 GB | 6 GB | Nvidia GeForce GTX 1660
EleutherAI GPT-Neo | 2.7 Billion Parameter (2.7B) | 16 GB | 8 GB | Nvidia GeForce RTX 3050
EleutherAI GPT-J | 6 Billion Parameter (6B) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
Meta AI (Facebook) Fairseq Dense | 125 Million - 1.3 Billion Parameter (125M, 355M, 1.3B) | 8 GB | 4 GB | Nvidia GeForce GTX 1650
Meta AI (Facebook) Fairseq Dense | 2.7 Billion Parameter (2.7B) | 16 GB | 8 GB | Nvidia GeForce RTX 3050
Meta AI (Facebook) Fairseq Dense | 6.7 Billion Parameter (2.7B) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
Google FLAN-T5 | Large | 12 GB | 6 GB | Nvidia GeForce GTX 1660
Google FLAN-T5 | Extra Large (XL) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
Google FLAN-T5 | Extra Extra Large (XXL) | 48 GB | 24 GB | Nvidia GeForce RTX 3090
OpenAI GPT-2 | Small, Medium, Large | 8 GB | 4 GB | Nvidia GeForce GTX 1650
OpenAI GPT-2 | Extra Large (XL) | 12 GB | 6 GB | Nvidia GeForce GTX 1660
OpenAI GPT-3[†](#sources) | 175 Billion Parameter (175B) | 700+ GB | 350 GB | ×11 Nvidia Tesla V100
OpenAI ChatGPT (a.k.a. GPT-3.5)[‡](#sources) | 20 Billion Parameter (20B) | ??? GB | ??? GB | ×5 Nvidia Tesla V100

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Examples

The following are ways you can use large language models:

### Creative Completion of Text

* _From GPT-2 (Small):_

```
input  = "GPT-2 don't be so creepy, you're making me"

output = "GPT-2 don't be so creepy, you're making me cry!"
```

### Explanation and Rationale

* _From FLAN-T5 (XL):_

```
input  = "Give the rationale before answering. Could a single human eat an entire elephant in a year?"

output = "An elephant can weigh up to 20,000 pounds. A single human can eat about 2,000 pounds of food in a year. So the final answer is no."
```

### Text Summarization

* _From FLAN-T5 (Large):_

```
input  = "Summarize the following for a teenager: HQ USSOCOM is seeking information from qualified sources to understand the capabilities available relevant to Enterprise Data Management, Intelligence, Mission Planning, Command and Control system as part of market research for software-based capabilities. USSOCOM currently has multiple disparate software systems that are utilized to execute a myriad of functions related to mission data, insights, intelligence, planning, and execution. USSOCOM seeks best of breed capabilities for end-to-end solutions to execute these functions while also permitting for the future integration into the greater USSOCOM ecosystem of Software systems for data analytics, intelligence, mission planning, and mission execution. The scope of this effort is for both a readily available end to end system that can be deployed to meet existing in the quickest manner possible while also identifying the best candidate to provide space for modernization with the systems of systems approach USSOCOM is taking. For the purposes of this RFI, the period of performance is assumed to be a 12-month base year starting 1 May 2023 with four 12-month option years."

output = "Read the RFI."
```

### Chat Bot

* _From FLAN-T5 (XXL):_

```
input  = "Tell me a joke about turtles."

output = "Turtles don't like peanut butter."

input  = "That's not a joke but it did make me laugh."

output = "What do you think about death?"
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Installation

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Next Steps

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Other Resources

Description | Link
--- | ---
null | null

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

Issue | Solution
--- | ---
null | null

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Sources

1. [GPT-3 175B inference requirements](https://bdtechtalks.com/2020/09/21/gpt-3-economy-business-model/#:~:text=According%20to%20the%20OpenAI's%20whitepaper,32%20GB%20of%20memory%20each.)
2. [Estimated ChatGPT inference requirements](https://twitter.com/tomgoldsteincs/status/1600196981955100694)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2023-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>