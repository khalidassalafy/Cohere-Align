# Cohere-Align
 
This repo takes two text files in the source and target languages, and returns sentences that are most likely translations of each other.

Before running, create an account on [cohere](https://cohere.com) to get your api key.

To align sentences, create two text files, with each line containing a distinct text, for the source and target languages. Afterwards , run the following command.

```python3 cohere_align.py \
   --cohere_api_key 'Lbm3HFuQlXzKGcc9zw4vq4OKdsP5SM8PFeMK7cEb' \
   -m 'embed-multilingual-v2.0' \
   -s ../src.txt \
   -t ../trg.txt \
   -o ../cohere \
   --retrieval 'nn' \
   --dot \
   --cuda```
