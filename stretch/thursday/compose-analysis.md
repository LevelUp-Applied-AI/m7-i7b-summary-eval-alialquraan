# Compose Analysis

## Test Set Design
We used a curated set of real-world examples containing news-style questions and reference answers to evaluate system robustness.

## Strategy A
Pre-trained inference approach using transformer-based models without additional training.

## Strategy B
Comparison baseline approach using alternative model outputs for evaluation consistency.

## Faithfulness
Model outputs are generally faithful to source content, but some abstraction introduces minor semantic drift, especially in low-information articles.

## Recommendation
Pre-trained inference is preferred for fast deployment and low cost. Fine-tuning is recommended only when domain-specific accuracy is critical and labeled data is available.