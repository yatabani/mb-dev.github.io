---
tags: ['study-notes', 'text-retrieval']
title: 'Text Retrieval and Search Engines'
---
(https://www.coursera.org/course/textretrieval)[https://www.coursera.org/course/textretrieval]

## System Implementation

![TR Architecture](http://i.imgur.com/TYU3Gmw.png)
- The documents are processed by tokenizer to get words. Words are processed by indexer. Query would go to the Scorer it uses the index to score them.
- User looks at them and giving feedback.

So we can divide into 3 parts:

- Indexer - can be done offline manner
- Scorer - online
- Feedback - can be done online/offline

Tokenization:

- Does stemming - computer, computation, computing -> compute
- In most cases is efficient. But some times might skew the meaning of specialized words.

Indexing:

- Convert document to data structure to enable fast search.
- Most common used: inverted index.

![Inverted Index](http://i.imgur.com/0p73yFN.png)

- In the dictionary we store some statistics about each term
- For example news occurred in 3 documents - we use that for the IDF.
- For each term we have postings - reference to the document that match.
- We can also store the positions - the page where the term is - we can use this to tell how close the terms are to each other.
- Using with boolean query: Term A and B. We fetch documents that match term A and then B and then do intersection between them.
- Multi-term keyword query: Aggregate term weights.

Word distributions:

- A few words "the", "a", "we" - occur very frequently. Most words occur rarely.
- Most frequent words in one corpus may be rare in another.
- This is characterized by Zipf's Law:

[Imgur](http://i.imgur.com/2pkT4AM.png)

- Rank of word * frequency of word is equal to a constant
- alpha - adjust for learning.
- in the middle there's intermediate frequent words.
- The highest frequency words are usually stop words. They are usually removed.
- The tail is also very useful but they don't get used usually.

Data Structure:

- Dictionary: modest size
  - Need fast random access (preferred to be in memory)
  - Hash table, B-tree, trie
- Postings: huge
  - We will store them sequentially on disk
  - May contain docID, term freq, term pos
  - Compression is desirable and to speed up loading.

Constructing inverted index:

- Main difficult is to build a huge index with limited memory.
- Sorting based methods:
  - Step1: Correct local (termID, docId, freq) tuples.
  - Sort local tuples
  - Pair-wise merge runs - until you eventually merged all of them.
  - Output inverted file
- Example:

[Sort based inversion](http://i.imgur.com/8q9ke8v.png)

- We use integers for indices.
- initially sort by document id (1 document first, then 2 etc.)
- when we run out of memory  - we will sort by term id and write to a temp file.
- then we merge sort by term ids

Compression:

- TF Compression: we can leverage the skewed distribution. We will use fewer bits for small (high frequency) integers. And more bits for larger integers. We still save on average.
- Doc ID compression - we can store the gap between values instead of the actual values.
- Binary code encoding is used.

Encoding:

- Binary: equal length coding
- Unary: x>=1 is coded as x-1 one bits followed by 0. E.g. 3=>110; 5=> 11110 (very inefficient) - variable length encoding.
- gamma-code: unary code for 1+(floor(log(x))). the magnitude of log(x) is lower. followed by binary code. (x-2)^(floor(log x)) in log(floor(x)) bits - 3->101 (10 is 2 in unary code + 1 difference), 5->11001 (110 - 3 unary code). 0 is the end of the unary code.
- There is also delta code.
- gamma coding seems to work
