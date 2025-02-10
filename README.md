# Word Piece Tokenizer Analysis

Word Piece Tokenizer is a powerful approach to tokenizing text. It was fascinating to explore how we can start with a simple vocabulary consisting of individual letters—distinguishing those that occur at the beginning of words from those that do not—and then progressively build a more statistical algorithm by evaluating token pair patterns. This process prioritizes merging token pairs where the individual elements occur the least frequently.

## Tokenization Experiment

When tokenizing two different text datasets, I initially experimented with a smaller vocabulary size of about 100 tokens. This resulted in poor token generation. Upon investigation, I discovered a bug: my model was not properly training on my corpus. Before even entering the first loop, the vocabulary size had already reached 136. After fixing this issue and increasing the vocabulary size, the model's performance improved significantly. It even started generating tokens that closely resembled proper English words. For example, the word *"this"* was identified as its own token, which makes sense given its high frequency in the English language.

A larger vocabulary size requires more training time but allows the model to capture more complex patterns in the data. 

## Results

The tokenized datasets produced the following results:

- **Wizard of Oz document**: 2,351 tokens
- **Court of Appeal document**: 2,309 tokens
- **Shared tokens between both sets**: 621

Some common tokens, such as *"family"*, appeared in both datasets. This indicates that the tokenizer effectively identifies meaningful patterns in the English language. The presence of shared tokens between two separately trained models demonstrates the efficiency of the algorithm.

However, a majority of tokens in each dataset were unique:

- **Unique to Wizard of Oz**: 1,730 tokens
- **Unique to Court of Appeal**: 1,688 tokens

For instance, the word *"synonymous"* appeared only in *Wizard of Oz*. Although it is a common word, it likely did not appear frequently enough in the *Court of Appeal* document to be included in its final vocabulary. This is also attributed to the model being trained on data of one particular topic therefore its ability to generalize is a little skewed and biased.
