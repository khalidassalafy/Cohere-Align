<a target="_blank" href="https://colab.research.google.com/github/abumafrim/Cohere-Align/blob/main/Cohere%20Align%20Sentences.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Table of Contents
<!-- vscode-markdown-toc -->
- [Table of Contents](#table-of-contents)
- [Cohere-Align](#cohere-align)
    - [Create account on CoHere](#create-account-on-cohere)
    - [Install CoHere module](#install-cohere-module)
    - [CoHere Align Sentences](#cohere-align-sentences)
- [Evaluation](#evaluation)
    - [Install laserembeddings module](#install-laserembeddings-module)
    - [Download pre-trained LASER models](#download-pre-trained-laser-models)
    - [LASER Align Sentences](#laser-align-sentences)
- [Options](#options)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

# <a name='Cohere'></a>Cohere-Align 
This repo takes two text files in the source and target languages, and returns sentences that are most likely translations of each other.

### <a name='Acct'></a>Create account on CoHere
Before running the aligner, create an account on [cohere](https://cohere.com) to get your api key.

### <a name='Install-C'></a>Install CoHere module
```
pip install cohere
```

### <a name='Align-C'></a>CoHere Align Sentences
To align sentences, create two text files, with each line containing a distinct text, for the source and target languages. Afterwards , run the following command.

```
python3 scripts/cohere_align.py \
   --cohere_api_key `'<api_key>'` \
   -m 'embed-multilingual-v2.0' \
   -s example/src.txt \
   -t example/trg.txt \
   -o cohere \
   --retrieval 'nn' \
   --dot \
   --cuda
 ```

# <a name='Eval'></a>Evaluation
We implemented a code for aligning the sentences using [LASER](https://github.com/facebookresearch/LASER) for evaluation. Afterwards, we compute F1 on the two aligned sentences to determine the better aligner.

### <a name='Install-L'></a>Install laserembeddings module

```
pip install laserembeddings
```
### <a name='Download-Laser'></a>Download pre-trained LASER models
```
python -m laserembeddings download-models
```
### <a name='Align-L'></a>LASER Align Sentences
```
python3 scripts/laser_align.py \
  -s example/src.txt \
  -t example/trg.txt \
  -o laser \
  --src_lang ha \
  --trg_lang en \
  --retrieval 'nn' \
  --dot \
  --cuda
```

You can also use the [jupyter notebook](https://github.com/abumafrim/Cohere-Align/blob/main/Cohere_Align_Sentences.ipynb) above to align the sentences.

# <a name='Options'></a>Options
| option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | description |
| ----------------- | ----------- |
| `'-k'` `'--cohere_api_key'` | your personal cohere api key (cohere-align only) |
| `'-s'` `'--src_sentences'` | the file containing source sentences |
| `'-t'` `'--trg_sentences'` | the file containing target sentences |
| `'-o'` `'--output'` | path to save the translations |
| `'-m'` `'--model'` | cohere multilingual model name (cohere-align only) |
| `'-b'` `'--batch_size'` | batch size. CoHere free API requires this. default=3000 (for source and target sentences each) (cohere-align only) |
| `'--retry_time'` | number of seconds to wait before retrying. default=61 (seconds) (cohere-align only) |
| `'--retrieval'` | the retrieval method (nn: standard nearest neighbor (default); invnn: inverted nearest neighbor; invsoftmax: inverted softmax; csls: cross-domain similarity local scaling) |
| `'--src_lang'` | source language (laser-align only, required) |
| `'--trg_lang'` | target language (laser-align only, required) |
| `'--inv_temperature'` | the inverse temperature (only compatible with inverted softmax). default = 1. |
| `'--inv_sample'` | use a random subset of the source vocabulary for the inverse computations (only compatible with inverted softmax). default=None |
| `'-n'` `'--neighborhood'` | the neighborhood size (only compatible with csls). default=10 |
| `'--dot'` | use the dot product in the similarity computations instead of the cosine |
| `'--encoding'` | the character encoding for input/output (defaults to utf-8) |
| `'--seed'` | the random seed. default=0 |
| `'--precision'` | the floating-point precision (defaults to fp32) |
| `'--cuda'` | use cuda (requires cupy) |