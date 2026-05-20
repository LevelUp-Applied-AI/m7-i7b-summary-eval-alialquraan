# Module 7 Week B — Integration Task: Summarization & Integrated Evaluation Report

This repository implements the Module 7 Week B Integration Task for evaluating and comparing pre-trained NLP models across multiple tasks including classification, question answering, and abstractive summarization.

The main objective of this project is to study the trade-offs between:
- Fine-tuned models (Lab 7A)
- Pre-trained QA systems (Lab 7B)
- Pre-trained summarization systems (Integration 7B)

The final deliverable is the integrated evaluation report (integrated-evaluation-report.md), which provides a full comparison of all approaches using real evaluation metrics.

---

## Quick start

Install dependencies and run full evaluation:

pip install -r requirements.txt  
make summarize  

The first execution downloads the Hugging Face model (~250MB).  
Subsequent runs reuse cached weights.

The full evaluation on 120 articles takes approximately 6–8 minutes on CPU.

---

## Summarization Model

We use the Hugging Face model:

sshleifer/distilbart-cnn-6-6

This is a distilled version of BART fine-tuned on the CNN/DailyMail dataset for abstractive summarization tasks.

Key characteristics:
- Transformer-based encoder-decoder architecture
- Optimized for news summarization
- Produces fluent abstractive summaries rather than extractive copying
- Lightweight compared to full BART models

---

## Dataset Description

The evaluation dataset consists of:

- 120 curated tech, entertainment, and digital culture news articles
- Human-written reference summaries aligned with each article
- Source dataset: glnmario/news-qa-summarization (Hugging Face)

Additionally, the full corpus contains 1,033 articles, but evaluation is restricted to the labeled 120-sample subset.

---

## Output Artifacts

Running the pipeline generates the following files:

- summary_predictions.csv  
  Contains article_id, reference summary, predicted summary, and per-sample ROUGE scores.

- summary_metrics.json  
  Contains aggregated ROUGE-1, ROUGE-2, and ROUGE-L F1 scores across the full dataset.

- integrated-evaluation-report.md  
  A structured analysis comparing:
  - Fine-tuned classification performance (Lab 7A)
  - Pre-trained QA performance (Lab 7B)
  - Pre-trained summarization performance (Integration 7B)

---

## Make Commands

make summarize   # Run full evaluation pipeline on 120 articles  
make smoke       # Run CI validation on 3-sample dataset  
make clean       # Remove generated outputs  

---

## Key Observations

This project demonstrates several important machine learning concepts:

1. Pre-trained models can perform competitive summarization without task-specific training.
2. Evaluation metrics like ROUGE provide approximate similarity but do not guarantee factual correctness.
3. Fine-tuning improves domain performance but reduces flexibility across tasks.
4. Pre-trained inference significantly reduces training cost and development time.

---

## Submission Guidelines

Submit your work via a Pull Request into the main branch.

The autograder validates:
- Correct execution of make smoke
- Proper output file generation
- Schema correctness of CSV and JSON outputs

---

## License

This repository is for educational purposes only.

You may use this code for learning and portfolio demonstration.

Redistribution outside this course is strictly prohibited.

This repository also includes full reproducibility guarantees and deterministic evaluation settings for consistent experimental results.