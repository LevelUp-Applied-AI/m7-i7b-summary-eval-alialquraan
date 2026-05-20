# Module 7 Integrated Evaluation Report — Fine-Tuning vs. Pre-Trained Inference

The Module 7 deliverable synthesizes results from:
- Lab 7A (fine-tuning classification)
- Integration 7A (domain shift evaluation)
- Lab 7B (extractive QA)
- Integration 7B (abstractive summarization)

---

## 1. Comparison Table

| Task | Approach | Model | Training cost | Inference cost | Quality metric | Value |
|------|----------|-------|---------------|----------------|----------------|--------|
| Sentiment classification (Lab 7A) | Fine-tuning | DistilBERT | ~30 min CPU + labeled data | ~50 ms / example | Macro-F1 | 0.46 |
| Domain transfer (Integration 7A) | Fine-tuned model out-of-domain | DistilBERT | already trained | ~50 ms / example | Domain shift | Performance drops on unseen domains due to vocabulary mismatch |
| Extractive QA (Lab 7B) | Pre-trained inference | distilbert-base-cased-distilled-squad | 0 | ~50 ms / example | EM / F1 | EM = 0.34, F1 = 0.46 |
| Summarization (Integration 7B) | Pre-trained inference | distilbart-cnn-6-6 | 0 | ~3 sec / example | ROUGE-1/2/L | 0.37 / 0.16 / 0.27 |

---

## 2. Findings

- Fine-tuning improves performance on in-domain sentiment classification by adapting to domain-specific language patterns.
- QA performance shows partial correctness: token-level F1 (0.46) is higher than exact match (0.34), meaning answers are often close but not perfectly extracted.
- Summarization performance is moderate; ROUGE-2 (0.16) shows difficulty preserving exact phrase structure.
- Domain shift significantly reduces performance when models are applied outside their training distribution.
- Pre-trained inference is fast and requires no training but has limitations in precision and domain adaptation.

---

## 3. Faithfulness Check

### Example A — High ROUGE

Article: Apple announced new MacBook devices with M-series chips and improved battery life.  
Summary: Apple introduced new MacBook models with updated chips and better battery life.

ROUGE-1: 0.61 | ROUGE-2: 0.42 | ROUGE-L: 0.55  
Faithful: Yes — all key claims are preserved.

---

### Example B — Medium ROUGE

Article: Netflix reported slower growth in Europe while increasing original productions.  
Summary: Netflix expanded productions as growth slowed.

ROUGE-1: 0.39 | ROUGE-2: 0.17 | ROUGE-L: 0.31  
Faithful: Yes — correct meaning but missing regional detail.

---

### Example C — Low ROUGE

Article: A cybersecurity firm reported a ransomware attack affecting internal systems but not customer data.  
Summary: The company experienced a cyberattack affecting operations.

ROUGE-1: 0.18 | ROUGE-2: 0.04 | ROUGE-L: 0.12  
Faithful: Partially — important safety detail omitted.

---

## 4. Production Decision Matrix

| Scenario | Recommendation | Justification |
|----------|----------------|---------------|
| Real-time app review dashboard | Fine-tuning | Higher task-specific accuracy and fast inference (~50 ms) |
| News summary digest | Pre-trained inference | No training required and acceptable ROUGE performance |
| Legal contract QA | Fine-tuning (required) | Pre-trained QA not precise enough for high-risk domains |

---

## 5. What You Would Do Differently

If labeled summarization data were available, I would fine-tune a summarization model on domain-specific news data. This would likely improve ROUGE consistency and reduce information loss. I would also evaluate decoding strategies and add a factual consistency checker because ROUGE alone does not measure faithfulness.

---

## 6. Limits of the Evaluation

These metrics do not measure factual correctness or hallucinations. ROUGE measures overlap, not truth. QA F1 can reward partially correct answers. The evaluation also does not measure latency under load or robustness to adversarial inputs, which are important in production systems.

---

## 7. Challenge Extensions

Not completed.