# Neural LP

This is the implementation of Neural Logic Programming, proposed in the following paper:

[Differentiable Learning of Logical Rules for Knowledge Base Reasoning](https://arxiv.org/abs/1702.08367).
Fan Yang, Zhilin Yang, William W. Cohen.
NIPS 2017.

## Requirements
- Python 2.7
- Numpy 
- Tensorflow 1.9.0
- Scikit-Learn 0.20.4

####You can use the following conda commands to setup suitable environments for the code:
```
conda create -n 'my_env_name' tensorflow=1.9 python=2.7
conda create -n 'my_env_name' tensorflow-gpu=1.9 python=2.7
```
Depending on whether GPU usage is desired (speeds up training and inference, but may not be available on all platforms).

## Quick start
The following command starts training a dataset about family relations, and stores the experiment results in the folder `exps/demo/`.

```
python src/main.py --datadir=datasets/family --exps_dir=exps/ --exp_name=demo
```

Wait for around 8 minutes, navigate to `exps/demo/`, there is `rules.txt` that contains learned logical rules. 

## Evaluation
To evaluate the prediction results, follow the steps below. The first two steps is preparation so that we can compute _filtered_ ranks (see [TransE](https://papers.nips.cc/paper/5071-translating-embeddings-for-modeling-multi-relational-data.pdf) for details).

We use the experiment from Quick Start as an example. Change the folder names (datasets/family, exps/dev) for other experiments.
```
. eval/collect_all_facts.sh datasets/family
python eval/get_truths.py datasets/family
python eval/evaluate.py --preds=exps/demo/test_predictions.txt --truths=datasets/family/truths.pckl
```
