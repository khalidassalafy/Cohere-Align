<a target="_blank" href="https://colab.research.google.com/github/abumafrim/Cohere-Align/blob/main/Cohere_Align_Sentences.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Cohere-Align
 
This repo takes two text files in the source and target languages, and returns sentences that are most likely translations of each other.

Before running, create an account on [cohere](https://cohere.com) to get your api key.

Then install cohere, using the following command

```
pip install cohere
```

To align sentences, create two text files, with each line containing a distinct text, for the source and target languages. Afterwards , run the following command.

```
python3 scripts/cohere_align.py \
   --cohere_api_key '<api_key>' \
   -m 'embed-multilingual-v2.0' \
   -s src.txt \
   -t trg.txt \
   -o cohere \
   --retrieval 'nn' \
   --dot \
   --cuda
 ```

where `m` is model name, `s` is source text path, `t` is target text path, `o` is output directory path, and provide the `cuda` option if you have GPU. For more parameters, see the [alignment script](https://github.com/abumafrim/Cohere-Align/blob/main/scripts/cohere_align.py).

You can also use the [jupyter notebook](https://github.com/abumafrim/Cohere-Align/blob/main/Cohere_Align_Sentences.ipynb) above to align sentences.
