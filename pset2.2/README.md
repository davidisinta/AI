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

---

## Findings

### **Real Cited Cases (Strong Matches)**
These cases were correctly cited with strong embedding similarities:

