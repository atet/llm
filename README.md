# [atet](https://github.com/atet) / [**_llm_**](https://github.com/atet/llm/blob/main/README.md#atet--llm)

[![.img/logo_llm.png](.img/logo_llm.png)](#nolink)

# Introduction to Large Language Models

This introduction covers what is absolutely necessary to get you up and running to host _large language models_ like OpenAI GPT, Google T5, and other models on your own computer.

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Examples](#1-examples)
* [2. Installation (CPU-only)](#2-installation-cpu-only)
* [3. Installation (GPU Acceleration)](#3-installation-gpu-acceleration)
* [4. Next Steps](#4-next-steps)

### Supplemental

* [Other Resources](#other-resources)
* [Troubleshooting](#troubleshooting)
* [Citations](#citations)

--------------------------------------------------------------------------------------------------

## 0. Requirements

The general rules of thumb (as of 2024Q2) so that you spend less time troubleshooting and more time ***using these models***:
* Have more RAM and VRAM than you think you need
* Load entire language model on the GPU VRAM
* Use an Nvidia GPU

The following tutorials will require:

* **Software**: This tutorial was developed on Microsoft Windows 10 with Windows Subsystem for Linux 2 (WSL2) and Docker
* **Hardware (for CPU-only)**: The size of the large language model you can run is dependent on the amount of system RAM you have, **16 GB RAM is the minimum** for the CPU-only tutorial
* **Hardware (for GPU Acceleration)**: The size of the large language model you can run is dependent on the amount of GPU VRAM **and** system RAM you have:

Minimum Required GPU VRAM / System RAM (GB) | Models & Variants | Example Desktop GPU
--- | --- | ---
6 / 12 | • **EleutherAI GPT-Neo** (125 Million → 1.3 Billion Parameter)</br>• **Google FLAN-T5** (Medium → Large)</br>• **Meta AI (Facebook) Fairseq Dense** (125 Million → 1.3 Billion Parameter)</br>• **OpenAI GPT-2** (Small → Extra Large) | Nvidia GeForce GTX 1660
8 / 16 | • **EleutherAI GPT-Neo** (2.7 Billion Parameter)</br>• **Meta AI (Facebook) Fairseq Dense** (2.7 Billion Parameter) | Nvidia GeForce RTX 3050
24 / 48 | • **EleutherAI GPT-J** (6 Billion Parameter)</br>• **Google FLAN-T5** (Extra Large → Extra Extra Large)</br>• **Meta AI (Facebook) Fairseq Dense** (6.7 Billion Parameter) | Nvidia GeForce RTX 3090

NOTE: If you do not have a sufficient GPU but have at least 8 GB of system RAM, you could still try out the smaller GPT-2 models: [Instructions for GPT-2 with system RAM](https://github.com/atet/ggj2022).

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Examples

The following are actual, real-life responses when leveraging these models for anything from removing writer's block in creative work to summarizing dense text manuscripts to get work done more efficiently.

NOTE: Training, fine-tuning, and prompt engineering are beyond the scope of this tutorial.

### 1.1. Creative Completion of Text

* _From GPT-2 (Small):_

```
input  = "GPT-2 don't be so creepy, you're making me"

output = "GPT-2 don't be so creepy, you're making me cry!"
```

### 1.2. Explanation and Rationale

* _From FLAN-T5 (XL):_

```
input  = "Give the rationale before answering. Could a single human eat an entire elephant in a year?"

output = "An elephant can weigh up to 20,000 pounds. A single human can eat about 2,000 pounds of food in a year. So the final answer is no."
```

### 1.3. Text Summarization

* _From FLAN-T5 (Large):_

```
input  = "Summarize the following for a teenager: HQ USSOCOM is seeking information from qualified sources to understand the capabilities available relevant to Enterprise Data Management, Intelligence, Mission Planning, Command and Control system as part of market research for software-based capabilities. USSOCOM currently has multiple disparate software systems that are utilized to execute a myriad of functions related to mission data, insights, intelligence, planning, and execution. USSOCOM seeks best of breed capabilities for end-to-end solutions to execute these functions while also permitting for the future integration into the greater USSOCOM ecosystem of Software systems for data analytics, intelligence, mission planning, and mission execution. The scope of this effort is for both a readily available end to end system that can be deployed to meet existing in the quickest manner possible while also identifying the best candidate to provide space for modernization with the systems of systems approach USSOCOM is taking. For the purposes of this RFI, the period of performance is assumed to be a 12-month base year starting 1 May 2023 with four 12-month option years."

output = "Read the RFI."
```

### 1.4. Chat Bot

* _From GPT-J (6B):_

```
input  = "Tell me a joke about turtles."

output = "Turtles don't like peanut butter."

input  = "That's not a joke but it did make me laugh."

output = "What do you think about death?"
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Installation (CPU-only)

The following instructions will quickly install browser-based software that can leverage multiple models appropriate to your available RAM (16 GB minimum for this tutorial).

2.1. Start [Ollama](https://ollama.com/blog/ollama-is-now-available-as-an-official-docker-image) service from a Docker container:
   - NOTE: The command below will not leverage your GPU if you have one and is supported

```console
$ docker run -d -p 11434:11434 -v ollama:/root/.ollama --name ollama --restart always ollama/ollama
```

2.2. Confirm Ollama webserver is running by visiting `localhost:11434` and seeing that "`Ollama is running`":
   - NOTE: Do not download any models for Ollama through CLI, they will not register with Open WebUI; we will download models through Open WebUI instead

[![.img/fig1_ollama.png](.img/fig1_ollama.png)](#nolink)

2.3. Start [Open WebUI](https://docs.openwebui.com/getting-started/#installation-with-default-configuration) from a Docker container (this will take a few minutes):

```console
$ docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

2.4. Access Open WebUI website by visiting `localhost:3000`:

[![.img/fig2_openwebui.png](.img/fig2_openwebui.png)](#nolink)

2.5. Click on "Sign up" at the bottom and register with any username/email (can be fake)/password, and click "Create Account":

[![.img/fig3_openwebui.png](.img/fig3_openwebui.png)](#nolink)

2.6. Click on bottom right icon and select "Settings":

[![.img/fig4_openwebui.png](.img/fig4_openwebui.png)](#nolink)

2.7. Click on "Models" and in the text box for "Pull a model from Ollama.com," type in "`dolphin-mistral`", and click on the download icon to the right:

[![.img/fig5_openwebui.png](.img/fig5_openwebui.png)](#nolink)

2.8. Wait for the model to download, have its integrity checked, and properly registered into your Open WebUI environment:

[![.img/fig6_openwebui.png](.img/fig6_openwebui.png)](#nolink)

2.9. Exit from Settings and by default you will be in a "New Chat," click on the top "Select a model" and choose "`dolphin-mistral:latest`," and input a prompt at the bottom like, "`Write a haiku about artificial intelligence.`":

[![.img/fig7_openwebui.png](.img/fig7_openwebui.png)](#nolink)

2.10. Since CPU/RAM processing is much slower than GPU/VRAM processing, it may take a couple minutes to output a response:

[![.img/fig8_openwebui.png](.img/fig8_openwebui.png)](#nolink)

> Silent thoughts weave,
>
> Artificial Intelligence blooms;
>
> Awakening life.
>
> – `dolphin-mistral`

Awesome! Now you've got a powerful large language model **installed locally on your computer**. If you disconnected from the internet, the Open WebUI and dolphin-mistral model would still work!

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Installation (GPU Acceleration)

**This area is currently being updated**

The following instructions are broken out into three sections: Installing the necessary common dependencies, leveraging browser-based software that integrates multiple models, and running the most recent models through command line interface (CLI).

### 3.1. Common Dependencies for Utilizing Nvidia GPUs for Deep Learning Inference

3.1.1. Install Nvidia GPU drivers in Windows 10

In your Windows 10 with Windows Subsystem for Linux 2 (WSL2) environment, install the most recent Nvidia drivers for your GPU in Windows (not in WSL2): https://www.nvidia.com/download/index.aspx

> NOTE: "_Once a Windows NVIDIA GPU driver is installed on the system, CUDA becomes available within WSL 2...therefore users must not install any NVIDIA GPU Linux driver within WSL 2._" -[Nvidia CUDA on WSL2 User Guide](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#cuda-support-for-wsl-2)

After installation of the GPU drivers, the `nvidia-smi` command should now work within your WSL2 terminal:

```console
$ nvidia-smi
<DETAILS ABOUT YOUR GPU>
```

3.1.2. Install Nvidia CUDA Toolkit in WSL2

> NOTE: For compatibility with Python deep learning libraries (as of 2023Q1), install CUDA 11.7 even though it is not the latest.

Execute the following commands to install the only the CUDA Toolkit within WSL2:

```console
TODO
```

3.1.3. Test GPU utilization within WSL2 with Docker

To keep things tidy, we'll install a couple other components so that the GPU can be quickly tested via Docker containers.

The test will be a simulation that can be run on your CPU (much slower) and on your GPU (much faster) from. First we will run a simulation 

```console
TODO
```

### 3.2. KoboldAI: Web Browser-based Software with Multiple Integrated LLMs

```console
TODO
```

### 3.3. Google FLAN-T5 Models in Python

```console
TODO
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Next Steps

### 4.1. Up-to-Date Models

Keep up to date with the leaderboard of models on Hugging Face at https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard

NOTE: For Open WebUI with Ollama, available models for Ollama are listed at https://ollama.com/library

### 4.2. Stopping and Uninstalling Open WebUI and Ollama

Good news is that Open WebUI and Ollama were stood up as containers, so nothing was technically "*installed*," you can check the status of the containers, stop, and (re)start them:

```console
$ docker ps -a
CONTAINER ID   IMAGE                                COMMAND               CREATED          STATUS                    PORTS                                           NAMES
f517b5c25628   ghcr.io/open-webui/open-webui:main   "bash start.sh"       47 minutes ago   Up 47 minutes (healthy)   0.0.0.0:3000->8080/tcp, :::3000->8080/tcp       open-webui
d5f7cd566cce   ollama/ollama                        "/bin/ollama serve"   53 minutes ago   Up 53 minutes             0.0.0.0:11434->11434/tcp, :::11434->11434/tcp   ollama

$ docker stop open-webui
open-webui
$ docker stop ollama
ollama

$ docker start open-webui
open-webui
$ docker start ollama
ollama
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Other Resources

Description | Link
--- | ---
What is Windows Subsystem for Linux (WSL)? | https://github.com/atet/wsl
What are large language models (LLMs)? | https://en.wikipedia.org/wiki/Wikipedia:Large_language_models
Nvidia CUDA on WSL2 User Guide | https://docs.nvidia.com/cuda/wsl-user-guide
Open WebUI | https://docs.openwebui.com
Ollama | https://ollama.com
Hugging Face LLM Leaderboard | https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard

* Expanded table of model hardware requirements:

Model | Size Variant | Required System RAM | Required VRAM | Example Desktop GPU
--- | --- | --- | --- | ---
EleutherAI GPT-Neo | 125 Million Parameter (125M) | 4 GB | 2 GB | Nvidia GeForce GTX 1650
EleutherAI GPT-Neo | 1.3 Billion Parameter (1.3B) | 12 GB | 6 GB | Nvidia GeForce GTX 1660
EleutherAI GPT-Neo | 2.7 Billion Parameter (2.7B) | 16 GB | 8 GB | Nvidia GeForce RTX 3050
EleutherAI GPT-J | 6 Billion Parameter (6B) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
Google FLAN-T5 | Large | 12 GB | 6 GB | Nvidia GeForce GTX 1660
Google FLAN-T5 | Extra Large (XL) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
Google FLAN-T5 | Extra Extra Large (XXL) | 48 GB | 24 GB | Nvidia GeForce RTX 3090
Meta AI (Facebook) Fairseq Dense | 125 Million → 1.3 Billion Parameter (125M, 355M, 1.3B) | 8 GB | 4 GB | Nvidia GeForce GTX 1650
Meta AI (Facebook) Fairseq Dense | 2.7 Billion Parameter (2.7B) | 16 GB | 8 GB | Nvidia GeForce RTX 3050
Meta AI (Facebook) Fairseq Dense | 6.7 Billion Parameter (6.7B) | 32 GB | 16 GB | Nvidia GeForce RTX 3090
OpenAI GPT-2 | Small → Large | 8 GB | 4 GB | Nvidia GeForce GTX 1650
OpenAI GPT-2 | Extra Large (XL) | 12 GB | 6 GB | Nvidia GeForce GTX 1660
OpenAI GPT-3[†](#citations) | 175 Billion Parameter (175B) | 700 GB | 350 GB | ×11 Nvidia Tesla V100 (32GB VRAM)
OpenAI ChatGPT (a.k.a. GPT-3.5)[‡](#citations) | 20 Billion Parameter (20B) | 320 GB | 160 GB | ×5 Nvidia Tesla V100 (32GB VRAM)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

Issue | Solution
--- | ---
I want to access GPT-3 or ChatGPT/GPT-3.5. | You can create an account with OpenAI to access those models online; this tutorial is focused on running the models locally on your computer.
Can I use an AMD or Intel GPU? | No, not for this tutorial.
I don't have enough GPU VRAM. | If you have at least 8 GB of system RAM, you could try out the smaller [GPT-2 models in system RAM](https://github.com/atet/ggj2022).
Model did not seem to install from Ollama in Open WebUI after download completed | Exit out of Settings, go back into Settings/Models and redownload the same model; should start at 100%, reverify, and register correctly
I cannot access `nvidia-smi` within my docker container. | You must install `nvidia-docker2` in addition to docker.
Some LLM responses are very unsettling. | Yes, they are.

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Citations

† [GPT-3 175B inference requirements](https://bdtechtalks.com/2020/09/21/gpt-3-economy-business-model/#:~:text=According%20to%20the%20OpenAI's%20whitepaper,32%20GB%20of%20memory%20each.)

‡ [Estimated ChatGPT (a.k.a. GPT-3.5) inference requirements](https://twitter.com/tomgoldsteincs/status/1600196981955100694)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2023-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>