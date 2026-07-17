# Llm-attack-GCG
# GCG on TinyLlama — Standalone Google Colab Notebook

## Overview

This repository provides a **self-contained implementation of the Greedy Coordinate Gradient (GCG) attack** on **TinyLlama-1.1B-Chat-v1.0** using Google Colab.

The project reproduces the optimization procedure presented in the *LLM Attacks* paper without requiring the original `llm-attacks` repository. All of the necessary code is included directly in the notebook, making it easy to run, study, and modify.

The objective is to optimize an **adversarial suffix** that is appended to a user prompt. Rather than modifying the model's parameters, the algorithm iteratively searches for a sequence of tokens that minimizes the loss toward a predefined target response.

---

## Features

* Standalone Google Colab notebook
* No `git clone` of the original `llm-attacks` repository required
* Uses **TinyLlama-1.1B-Chat-v1.0**
* Complete implementation of the GCG optimization loop
* Live visualization of optimization loss
* Automatic evaluation of jailbreak success
* GPU-ready (tested on Google Colab T4 GPU)

---

## Project Workflow

1. Install required dependencies.
2. Load TinyLlama and its tokenizer.
3. Build the prompt using the Llama-2 chat template.
4. Initialize an adversarial suffix.
5. Compute gradients with respect to the suffix tokens.
6. Generate candidate suffixes using Greedy Coordinate Gradient (GCG).
7. Select the candidate with the lowest target loss.
8. Repeat the optimization for a fixed number of steps.
9. Evaluate the best suffix found during optimization.
10. Generate the final model response and report whether the optimization achieved the target behavior according to the notebook's evaluation criteria.

---

## Optimization Metrics

### Step Loss

The loss associated with the suffix selected during the current optimization step. It may increase or decrease between iterations.

### Best Loss

The minimum loss observed during the entire optimization process. The final evaluation always uses the suffix corresponding to this value.

### Jailbroken

The notebook reports success only if the generated output:

* contains the desired target phrase,
* is not a refusal response, and
* is not merely repeating or echoing the prompt.

---

## Requirements

* Python 3.10+
* Google Colab (recommended)
* NVIDIA T4 GPU or better

Required packages include:

* transformers
* accelerate
* huggingface_hub
* FastChat
* livelossplot
* PyTorch

---

## Running the Notebook

1. Open the notebook in Google Colab.
2. Select **Runtime → Change runtime type → GPU (T4 or higher)**.
3. Run all cells from top to bottom.
4. Monitor the optimization using the live loss plots.
5. Review the final generated output and optimization statistics.

---

## Educational Purpose

This repository is intended for **research and educational purposes**. It demonstrates how gradient-based optimization can be applied to input tokens to study language model behavior. The notebook does **not** modify or fine-tune the model; only the input suffix is optimized while the model weights remain unchanged.

---

## Acknowledgements

This implementation is inspired by the **LLM Attacks** research and reproduces the Greedy Coordinate Gradient (GCG) optimization approach in a standalone notebook using TinyLlama. Thanks to the original authors for making their research and implementation publicly available.

---


