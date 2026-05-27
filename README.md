# MixUP Upstage Korean Modernization

A Korean text modernization pipeline using **Upstage Solar Pro2** and **multi-turn prompt engineering**.

This project was developed for the **MixUP Upstage Promptathon**, where the goal was to convert text containing archaic Korean, Hanja, classical Chinese, and mixed-language expressions into modern Korean news-style sentences.

---

## Overview

Modernizing historical or mixed-style Korean text requires more than simple translation.
The system must preserve the original meaning while improving readability, fluency, and contemporary Korean expression.

This repository implements a prompt-based generation pipeline that converts input sentences into modern Korean using a structured three-turn prompting strategy.

The pipeline focuses on:

* Meaning preservation
* Natural modern Korean rewriting
* News-style sentence formatting
* Multi-turn self-verification
* Batch generation for CSV-based submissions

---

## Competition Result

| Metric                   |  Score |
| ------------------------ | -----: |
| Public Leaderboard Score | 0.8360 |
| Final Score              | 0.8140 |

---

## Key Features

* Solar Pro2-based Korean sentence modernization
* Multi-turn prompt engineering strategy
* CSV-based batch inference pipeline
* Parallel generation with configurable worker count
* Prompt configuration through `prompt.json`
* Temperature and token control for each generation turn
* Submission-ready CSV output generation

---

## Prompting Strategy

The system uses a three-turn prompting process.

### Turn 1: Meaning-preserving modernization

The model first rewrites the original sentence into modern Korean while preserving the original meaning.

### Turn 2: Fluency refinement

The model improves naturalness, readability, and news-style expression.

### Turn 3: Verification and correction

The model compares the rewritten sentence with the original input and revises the output if meaning loss or distortion is detected.

This structure was designed to reduce semantic drift while improving sentence quality.

---

## Repository Structure

```
.
├── generate.py          # Main batch generation script
├── prompt.json          # Prompt configuration file
├── prompts/             # Prompt templates or prompt-related modules
├── README.md
└── .gitignore
```

---

## Installation

Install dependencies:

```
pip install pandas tqdm python-dotenv openai
```

---

## Environment Variables

Create a `.env` file and add your Upstage API key:

```
UPSTAGE_API_KEY=your_api_key_here
```

Do not commit API keys or environment files to GitHub.

---

## Usage

Run batch generation:

```
python generate.py \
    --input data/test_dataset.csv \
    --output submission.csv \
    --model solar-pro2 \
    --prompt prompt.json \
    --max_workers 3 \
    --temp1 0.0 \
    --temp2 0.0 \
    --temp3 0.0
```

---

## Main Arguments

| Argument        | Description                    |
| --------------- | ------------------------------ |
| `--input`       | Input CSV file path            |
| `--output`      | Output CSV file path           |
| `--model`       | Model name, e.g. `solar-pro2`  |
| `--prompt`      | Prompt configuration JSON path |
| `--max_workers` | Number of parallel workers     |
| `--temp1`       | Temperature for turn 1         |
| `--temp2`       | Temperature for turn 2         |
| `--temp3`       | Temperature for turn 3         |
| `--max_tokens1` | Maximum tokens for turn 1      |
| `--max_tokens2` | Maximum tokens for turn 2      |
| `--max_tokens3` | Maximum tokens for turn 3      |

---

## Input Format

The input CSV file should contain the following columns:

| Column              | Description                      |
| ------------------- | -------------------------------- |
| `id`                | Unique sample ID                 |
| `original_sentence` | Source sentence to be modernized |

Example:

```
id,original_sentence
0,此는 옛 문헌에 기록된 문장이라...
```

---

## Output Format

The generated CSV file contains:

| Column              | Description                |
| ------------------- | -------------------------- |
| `id`                | Unique sample ID           |
| `original_sentence` | Original input sentence    |
| `answer_sentence`   | Modernized Korean sentence |

---

## Project Relevance

This project is related to:

* Prompt Engineering
* Large Language Models
* Korean NLP
* Text Modernization
* Batch Inference
* Multi-turn Generation
* LLM-based Text Transformation
* Upstage Solar Pro2

---

## Limitations

* This repository is a competition-oriented prompt engineering project.
* The system depends on the behavior and availability of the Solar Pro2 API.
* Outputs may vary depending on prompt design, temperature, token limits, and model updates.
* Additional human evaluation may be required for sensitive historical or legal text.
* This project does not train a language model; it focuses on prompt design and generation workflow.

---

## Future Work

* Add example input and output files
* Add automatic evaluation scripts
* Add prompt version comparison
* Add error analysis for semantic drift
* Add retry logic for API failures
* Add cost and latency tracking
* Refactor prompt templates into modular files
* Add a lightweight web interface for sentence modernization
