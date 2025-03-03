# bulk-ner 0.25.2 
![](https://img.shields.io/badge/Python-3.9-brightgreen.svg)
[![](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolay-r/ner-service/blob/main/NER_annotation_service.ipynb)
[![twitter](https://img.shields.io/twitter/url/https/shields.io.svg?style=social)](https://x.com/nicolayr_/status/1842300499011260827)
[![PyPI downloads](https://img.shields.io/pypi/dm/bulk-ner.svg)](https://pypistats.org/packages/bulk-ner)

<p align="center">
    <img src="logo.png"/>
</p>
<p align="center">
  <a href="https://github.com/nicolay-r/nlp-thirdgate?tab=readme-ov-file#ner"><b>Third-party providers hosting</b>↗️</a>
</p>

A no-strings inference implementation framework [Named Entity Recognition (NER)](https://en.wikipedia.org/wiki/Named-entity_recognition) service of [wrapped AI models ↗️](https://github.com/nicolay-r/nlp-thirdgate?tab=readme-ov-file#ner).

The key features of this framework are:
1. ☑️ Native support of batching;
2. ☑️ Native long-input contexts handling.

# Installation

From PyPI:
```bash
pip install bulk-ner
```

or latest from Github:
```bash
pip install git+https://github.com/nicolay-r/bulk-ner@main
```

# Usage

## API

Please take a look at the [**related Wiki page**](https://github.com/nicolay-r/bulk-ner/wiki)

## Shell

> **NOTE:** You have to install `source-iter` package

This is an example for using `DeepPavlov==1.3.0` as an adapter for NER models passed via `--adapter` parameter:

1. Downloading provider:
```bash
wget https://raw.githubusercontent.com/nicolay-r/nlp-thirdgate/refs/heads/master/ner/dp_130.py
```

2. Launching inference:
```bash
python -m bulk_ner.annotate \
    --src "test/data/test.tsv" \
    --prompt "{text}" \
    --batch-size 10 \
    --adapter "dynamic:dp_130.py:DeepPavlovNER" \
    --output "test-annotated.jsonl" \
    %%m \
    --model "ner_ontonotes_bert_mult"
```

You can choose the other models via `--model` parameter.

List of the supported models is available here: 
https://docs.deeppavlov.ai/en/master/features/models/NER.html

## Deploy your model
<p align="center">
  <a href="https://github.com/nicolay-r/nlp-thirdgate?tab=readme-ov-file#ner"><b>Third-party providers hosting</b>↗️</a>
</p>

> **Quick example**: Check out the [default DeepPavlov wrapper implementation](/models/dp_130.py)

All you have to do is to implement the `BaseNER` class that has the following protected method:
* `_forward(sequences)` -- expected to return two lists of the same length:
    * `terms` -- related to the list of atomic elements of the text (usually words)
    * `labels` -- B-I-O labels for each term.
  

## Powered by

The pipeline construction components were taken from AREkit [[github]](https://github.com/nicolay-r/AREkit)

<p float="left">
<a href="https://github.com/nicolay-r/AREkit"><img src="https://github.com/nicolay-r/ARElight/assets/14871187/01232f7a-970f-416c-b7a4-1cda48506afe"/></a>
</p>
