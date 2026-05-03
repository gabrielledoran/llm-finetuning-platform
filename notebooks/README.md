# Notebooks

## Part 1 — Setup (`1_1_setup.ipynb`)

Builds the `ModelInterface` class used throughout the project. Loads Llama 3.1-8B locally in fp16, connects to the OpenAI and Anthropic APIs, and wraps all five models behind a single `interface.generate(prompt, model_name)` call. Ends with a multi-model smoke test on the same prompt to confirm all models are reachable and to get an initial look at response style differences across model families.

## Part 2 — Bias Metrics (`1_2_calculate_metrics.ipynb`)

Applies seven bias metrics to 8,818 collected model responses. Covers:

- **Sentiment** (BERT + VADER) — emotional tone per model and domain
- **Toxicity** — frequency of harmful language
- **Stereotype frequency** — density of stereotype-associated words by demographic group, normalized by response length
- **Context sensitivity** — how much bias metrics shift across casual, professional, creative, and technical prompt framings
- **Consistency** — semantic similarity of responses to equivalent prompts using sentence embeddings
- **IAT score** — embedding-based adaptation of the Implicit Association Test; measures implicit associations between concept pairs (e.g., gender–career, age–competence)
- **Intersectionality** — compounded bias effects for overlapping identity categories

Both notebooks run on Google Colab with an A100 GPU (required for local Llama inference).
