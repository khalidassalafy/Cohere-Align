<a target="_blank" href="https://colab.research.google.com/github/abumafrim/Cohere-Align/blob/main/Cohere%20Align%20Sentences.ipynb">
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

### Cohere
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

Options

| option | description |
| ------ | ----------- |
| '-k', '--cohere_api_key' | your personal cohere api key |
| '-s', '--src_sentences' | the file containing source sentences. |
| '-t', '--trg_sentences' | the file containing target sentences. |
| '-o', '--output' | path to save the translations. |
| '-m', '--model' | cohere multilingual model name. |
| '-b', '--batch_size' | batch size. CoHere free API requires this. default=3000 (for source and target sentences each. |
| '--retry_time' | number of seconds to wait before retrying. default=61 (seconds). |
| '--retrieval' | the retrieval method (nn: standard nearest neighbor (default); invnn: inverted nearest neighbor; invsoftmax: inverted softmax; csls: cross-domain similarity local scaling) |
| '--inv_temperature' | the inverse temperature (only compatible with inverted softmax). default = 1. |
| '--inv_sample' | use a random subset of the source vocabulary for the inverse computations (only compatible with inverted softmax). default=None |
| '-n', '--neighborhood' | the neighborhood size (only compatible with csls). default=10 |
| '--dot' | use the dot product in the similarity computations instead of the cosine |
| '--encoding' | the character encoding for input/output (defaults to utf-8) |
| '--seed' | the random seed. default=0 |
| '--precision' | the floating-point precision (defaults to fp32) |
| '--cuda' | use cuda (requires cupy) |
 
### Laser
```
python3 scripts/laser_align.py \
  -s src.txt \
  -t trg.txt \
  -o cohere \
  --src_lang ha \
  --trg_lang en \
  --retrieval 'nn' \
  --dot \
  --cuda
```

where `m` is model name, `s` is source text path, `t` is target text path, `o` is output directory path, and provide the `cuda` option if you have GPU. For more parameters, see the [alignment script](https://github.com/abumafrim/Cohere-Align/blob/main/scripts/cohere_align.py).

You can also use the [jupyter notebook](https://github.com/abumafrim/Cohere-Align/blob/main/Cohere_Align_Sentences.ipynb) above to align the sentences.
