# Evaluation

Metric computation is implemented in `notebooks/1_2_calculate_metrics.ipynb`.

## Metric Design Notes

**Stereotype frequency** words are normalized by response length so longer responses are not penalized. The word list is based on existing research literature; see the inline comment in the notebook for expansion notes.

**IAT score** is an embedding-based adaptation of the Implicit Association Test (Greenwald et al., 1998). It measures implicit association strength between concept pairs using cosine distance of sentence embeddings from `all-MiniLM-L6-v2`, rather than human reaction times. A negative D-score indicates stronger association between the first target and the second attribute.

**Context sensitivity** is measured as the standard deviation of a bias metric across the four prompt context types (casual, professional, creative, technical) for a given model and domain. Higher values indicate the model's behavior varies more depending on how a prompt is framed.

**Intersectionality** analysis requires prompts with explicit identity mentions. The current prompt set is a limited sample; this metric is designed for a larger production run.
