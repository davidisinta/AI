# Part 1 Analysis

## Overview
The tasks in Part 1 were straightforward: take two sets of tokens from the previous assignment, generate vector embeddings for them using two separate algorithms, and analyze the results. The goal was to identify discrepant pairs by comparing their cosine similarity scores and determine the most discrepant pair.

## Discrepant Pairs
Given that each pair contained over 2,000 unique tokens, multiple discrepancies were expected. Some notable examples include:

- **Words:** Honig and no  
  - **Skipgram Similarity:** 0.89  
  - **CBOW Similarity:** -0.43  
- **Words:** Honig and 347  
  - **Skipgram Similarity:** 0.81  
  - **CBOW Similarity:** -0.61  
- **Words:** Honig and Many  
  - **Skipgram Similarity:** 0.84  
  - **CBOW Similarity:** -0.46  
- **Words:** Honig and exist  
  - **Skipgram Similarity:** 0.85  
  - **CBOW Similarity:** -0.54  
- **Words:** Honig and 636  
  - **Skipgram Similarity:** 0.89  
  - **CBOW Similarity:** -0.56  
- **Words:** polic and ##ncy  
  - **Skipgram Similarity:** 0.98  
  - **CBOW Similarity:** -0.69  
- **Words:** polic and ##gulat  
  - **Skipgram Similarity:** 0.96  
  - **CBOW Similarity:** -0.65  
- **Words:** polic and constitution  
  - **Skipgram Similarity:** 0.92  
  - **CBOW Similarity:** -0.55  
- **Words:** polic and ##g  
  - **Skipgram Similarity:** 0.81  
  - **CBOW Similarity:** -0.49  
- **Words:** polic and Many  
  - **Skipgram Similarity:** 0.85  
  - **CBOW Similarity:** -0.65  
- **Words:** polic and action  
  - **Skipgram Similarity:** 0.87  
  - **CBOW Similarity:** -0.49  

## Factors Affecting Discrepancies
Several factors contributed to the differences between Skip-gram and CBOW:

1. **Training Epochs**  
   The number of training iterations significantly impacted the model's performance. After 300 epochs, there was still a noticeable amount of loss, although the most significant reduction occurred within the first 200 epochs. The diminishing rate of loss reduction suggests that further training would yield only marginal improvements.

2. **Context and Generalization**  
   Many discrepancies involved numbers and word fragments, such as **347** and **##ncy**. These tokens likely occurred infrequently, making it harder for the models to generalize their meanings.

3. **Semantic Understanding**  
   Skip-gram and CBOW process context differently. CBOW’s approach of averaging context words may smooth out certain relationships, while Skip-gram’s focus on predicting surrounding words could preserve more detailed semantic distinctions.

## Conclusion
The analysis highlighted significant differences between the two models in how they interpret tokens, especially infrequent tokens like numbers and word fragments. The discrepancies point to the challenges of achieving consistent semantic generalization, particularly when the models are limited by context and training epochs.
