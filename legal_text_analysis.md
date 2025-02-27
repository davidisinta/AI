# Part 1 Analysis

## Overview
The tasks in Part 1 were straightforward: take two sets of tokens from the previous assignment, generate vector embeddings for them using two separate algorithms, and analyze the results. The goal was to identify discrepant pairs by comparing their cosine similarity scores and determine the most discrepant pair.

## Discrepant Pairs
Given that each pair contained over 2,000 unique tokens, multiple discrepancies were expected. Notable examples include:

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

1. **Training Epochs** – More training iterations typically improve model accuracy. After 300 epochs, there was still some loss, though most of the reduction occurred within the first 200 epochs, with diminishing returns thereafter.

2. **Context and Generalization** – Tokens like numbers and word fragments were more prone to discrepancies. For example, **347** and **Honig** were often mismatched, likely because their infrequent occurrences made it harder for models to generalize them.

3. **Semantic Understanding** – Skip-gram and CBOW process words differently. CBOW’s context-smoothing nature likely contributed to the stronger negative similarities in certain cases.

## Conclusion
The analysis highlighted the inherent differences in how Skip-gram and CBOW models interpret tokens, particularly numbers and word fragments. Training epochs and context availability played a significant role in these discrepancies, emphasizing the challenge of achieving consistent semantic understanding across embedding models.

---

# Part 2 Analysis

## Challenges and Approach
The second part of the assignment was quite challenging, particularly when it came to extracting court case citations from a plain text file. The unstructured format made evaluation difficult, and even with recognizable patterns, significant regex expertise was required—yet this still did not work for all cases. **SpaCy** helped automate parts of the extraction process.

Initially, my approach was to compare embeddings of **real cases** directly against **cited cases**. However, this presented two key challenges:

1. **Detecting Non-Existent Cases**  
   - Full case descriptions were unnecessary for identifying fictitious cases—only the case titles (or headers) mattered.  
   - To optimize this, I **split** each case into two parts: **header** and **description**.  
   - This significantly improved accuracy in detecting non-existent cases.  
   - The results improved even further when I **trimmed headers** to retain only the **"Who vs. Who"** format, making the embeddings highly effective at identifying hallucinated case names.

2. **Evaluating Misinterpreted Texts**  
   - Using **cosine similarity directly** on full case descriptions led to poor results.  
   - This was because original case descriptions could be **thousands of words long**, making a single vector embedding inaccurate.  
   - **Chunking** the original descriptions into smaller segments **improved cosine similarity accuracy**, leading to better comparisons with cited case descriptions.

## Findings

### **Real Cited Cases (Strong Matches)**
These cases were correctly cited with strong embedding similarities:

```
Messenger v. Gruner  
Hurwitz v. United  
Gautier v. Pro  
Delan v. CBS, Inc.  
Finger v. Omni  
Arrington v. New  
```

### **Possible Matches**
These cases had close but imperfect matches, suggesting some level of misinterpretation:

```
Cited: Hurwitz v. United | Real: Powers v. United | Similarity: 0.5806  
Cited: Hurwitz v. United | Real: Smith v. United | Similarity: 0.6261  
Cited: Delan v. CBS, Inc. | Real: J.H. Desnick, M.D., Eye Services, Ltd. v. American Broadcasting Companies, Inc., Jon Entine, and Sam Donaldson, 233 F.3d 514 (7th Cir. 2000) | Similarity: 0.5520  
```

### **Non-Existent Case Citations**
These cases were **hallucinated**—they did not exist in real legal records:

```
Andrea v. Fakename, 972 F.Supp.  
Piskac v. Shapiro, 230 Conn. 345 (2025).  
Candelaria v. Spurlock, the plaintiff appeared briefly in the documentary *Super Size Me.*  
Spurlock v. Candelaria, 08 Civ. 1830 (BMC) (RER)  
```

## Conclusion
By refining how case headers were extracted and processed, I achieved **remarkable accuracy** in detecting non-existent cases. Additionally, chunking full case descriptions significantly improved **cosine similarity comparisons**, making it easier to identify misinterpretations. While regex alone was insufficient, combining **SpaCy-based extraction** with **embedding-based comparisons** proved to be an effective strategy for legal text analysis.
