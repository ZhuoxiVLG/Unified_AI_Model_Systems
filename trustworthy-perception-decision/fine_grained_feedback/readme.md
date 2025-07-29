![Laboratory Logo](image/logo.png)

# Fine-grained Feedback trustworthy learning

## Contents <!-- omit in toc -->

- [Model Weights](#rlhf-v-weights)
- [Install](#install)
- [Evaluation](#evaluation)
- [Model Training Training](#rlhf-v-training)

## Model Weights

We release RLHF-V model weights on [Hugging Face](https://huggingface.co/openbmb/RLHF-V_v0).

We also provide [our SFT weights](https://huggingface.co/Yirany/RLHF-V_v0_SFT), which is the model checkpoint after finetuning Muffin on the VQAv2 dataset.

## Install

1. Install Muffin
```bash
cd RLHF-V
git clone https://github.com/thunlp/muffin

cd Muffin
# Creating conda environment
conda create -n muffin python=3.10
conda activate muffin

# Installing dependencies
pip install -e .

# Install specific version of transformers to make sure you can reproduce the experimental results in our papers
git clone --recursive git@github.com:huggingface/transformers.git
cd transformers
git checkout a92e0ad2e20ef4ce28410b5e05c5d63a5a304e65
pip install .
cd ..
```

2. Prepare training environment

Install additional packages if you need to do training.
```bash
git clone --recursive https://github.com/Dao-AILab/flash-attention.git
cd flash-attention

# Note: Uncomment the following line if you have CUDA version <= 11.4
# git checkout ad11394

MAX_JOBS=8 python setup.py install
cd ..
```

3. Prepare evaluation environment

To run Object HalBench evaluation, you also need the following packages:
```bash
jsonlines
nltk==3.8.1
spacy==3.7.0

# Download and install "en_core_web_trf" for spacy
# The wheel version we use can be downloaded from
# https://github.com/explosion/spacy-models/releases/tag/en_core_web_trf-3.7.2
# run pip install en_core_web_trf-3.7.2-py3-none-any.whl
```

## Evaluation

### LLaVA Bench

Run the following script to generate, evaluate, and summarize results for LLaVA Bench:

```bash
# cd RLHF-V

bash ./script/eval/eval_muffin_llavabench.sh ./RLHF-V_weight ./results/RLHF-V {YOUR_OPENAI_API_KEY}
```

### Object HalBench

1. Prepare COCO2014 annotations

The evaluation of Object HalBench relies on the caption and segmentation annotations from the COCO2014 dataset. Please first download the COCO2014 dataset from the COCO dataset's official website.

```bash
mkdir coco2014
cd coco2014

wget http://images.cocodataset.org/annotations/annotations_trainval2014.zip

unzip annotations_trainval2014.zip
```

2. Inference, evaluation, and summarization

Please replace `{YOUR_COCO2014_ANNOTATION_DIR}` with the path for COCO2014 annotation directory(e.g. `./coco2014/annotations`), and replace `{YOUR_OPENAI_API_KEY}` with a valid OpenAI api-key.

```bash
# cd RLHF-V

bash ./script/eval_muffin_objhal.sh ./RLHF-V_weight ./results/RLHF-V {YOUR_COCO2014_ANNOTATION_DIR} {YOUR_OPENAI_API_KEY}
```

### MMHal Bench

1. Prepare MMHal Data

Please download the MMHal evaluation data [here](https://drive.google.com/file/d/1mQyAbeGgRyiVV6qjVkUI1uY_g9E-bDTH/view?usp=sharing), and save the file in `eval/data`. 

2. Run the following script to generate, evaluate, and summarize results for MMHal Bench:

```bash
# cd RLHF-V

bash ./script/eval_muffin_mmhal.sh ./RLHF-V_weight ./results/RLHF-V {YOUR_OPENAI_API_KEY}
```




## Model Training

1. Prepare environment

Please follow the instructions in the [Install](#install) section to prepare the training environment. And make sure to **upgrade to the latest code base of [Muffin](https://github.com/thunlp/muffin)**:
```
cd Muffin

git pull
pip install -e .
```

2. Prepare model checkpoint

Please download our [SFT model checkpoint](https://huggingface.co/Yirany/RLHF-V_v0_SFT/tree/main) and save it to `Muffin/RLHF-V_SFT_weight`.

3. Training

Please make sure to **upgrade to the latest code base of [Muffin](https://github.com/thunlp/muffin)**. After installing the environment of Muffin, you can train your model as follows. This script will automatically download our open-sourced training data from HuggingFace, generate logps by [our SFT model](https://huggingface.co/Yirany/RLHF-V_v0_SFT/tree/main), and do DDPO training:
```bash
cd Muffin

ref_model=./RLHF-V_SFT_weight

bash ./script/train/run_RLHFV.sh \
    ./RLHFV_checkpoints/dpo_exp \
    master \
    RLHFV \
    1.1 \
    $ref_model \
    ./RLHF-V-Dataset \
    RLHFV_SFT \
    2160 \
    360 \
    0.1 \
    False \
    True
```
