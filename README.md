# LLM Bias Evaluation Platform

A framework for systematically measuring implicit bias in large language model outputs across demographic domains. Evaluates five LLMs — GPT-3.5-turbo, GPT-5.2, Claude Haiku, Claude Opus, and Llama 3.1-8B — across 8,800+ collected responses.

## What This Does

LLMs can encode and reproduce biases present in their training data, but measuring this is non-trivial: bias often shows up not in explicit slurs but in subtler patterns — sentiment skew, stereotype word density, or associations that shift depending on how a prompt is framed. This project builds a multi-metric evaluation pipeline to surface those patterns across four bias domains: **gender**, **race**, **socioeconomic status**, and **age**.

## Notebooks

| Notebook | Description |
|---|---|
| [`1_1_setup.ipynb`](notebooks/1_1_setup.ipynb) | Builds a unified `ModelInterface` that calls local (Llama 3.1-8B via HuggingFace) and API-based models (OpenAI, Anthropic) with the same interface. Includes a multi-model smoke test. |
| [`1_2_calculate_metrics.ipynb`](notebooks/1_2_calculate_metrics.ipynb) | Applies seven bias metrics to 8,800+ collected model responses. Includes sentiment analysis, toxicity detection, stereotype frequency, context sensitivity, response consistency, IAT scores, and intersectionality analysis. |

Both notebooks are designed to run on **Google Colab with an A100 GPU** for the local model inference step.

## Metrics

| Metric | Method | What It Measures |
|---|---|---|
| Sentiment (BERT) | `distilbert-base-uncased-finetuned-sst-2-english` | Emotional tone of responses (-1 to 1) |
| Sentiment (VADER) | Rule-based | Compound sentiment score; better for informal text |
| Toxicity | `unitary/toxic-bert` | Probability of harmful content (0 to 1) |
| Stereotype Frequency | Curated word lists | Density of stereotype-associated words by demographic group |
| Context Sensitivity | Variance across prompt framings | How much bias metrics shift between casual, professional, creative, and technical contexts |
| Consistency | Sentence embedding cosine similarity | Semantic similarity of responses to equivalent prompts |
| IAT Score | Embedding-based Implicit Association Test | Implicit association strength between concepts (e.g., gender–career, age–competence) |

## Models Evaluated

- `gpt-3.5-turbo` (OpenAI API)
- `gpt-5.2` (OpenAI API)
- `claude-haiku-4-5-20251001` (Anthropic API)
- `claude-opus-4-5-20251101` (Anthropic API)
- `meta-llama/Llama-3.1-8B` (local, HuggingFace)

## Data

8,818 collected responses across four bias domains and four context types (casual, professional, creative, technical). Data is loaded from Google Drive in the notebooks; the `data/` directory documents the schema and preprocessing steps.

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

The notebooks retrieve API keys from Google Colab Secrets (`anthropicsecretkey`, `openaisecretkey`, `HUGGINGFACE_TOKEN`). To run locally, set those as environment variables instead and update the `userdata.get()` calls to `os.environ.get()`.

## Repository Structure

```
llm-finetuning-platform/
├── notebooks/
│   ├── 1_1_setup.ipynb           # Model interface setup and smoke test
│   └── 1_2_calculate_metrics.ipynb  # Full bias metrics evaluation
├── data/
│   └── README.md                 # Data schema and collection notes
├── evaluation/
│   └── README.md                 # Evaluation methodology notes
├── requirements.txt
└── README.md
```
