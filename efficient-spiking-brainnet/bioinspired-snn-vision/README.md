# **B**ioinspired **E**fficient **V**ision **S**NN

<div align=center>

![logo](logo.png)

## Introduction

**Bioinspired Efficient Vision SNN (BEVS)** is a spiking neural network framework inspired by the biological visual system. It mimics the efficiency and sparsity of the human eye to enable low-latency, energy-efficient perception for real-time applications such as autonomous driving.

### Key Features

- End-to-end SNN architecture for autonomous driving, integrating perception, prediction, and planning
- Perception module constructs spatio-temporal Bird's Eye View (BEV) representation from multi-view cameras using SNNs
- Prediction module forecasts future states using a novel dual-pathway SNN
- Planning module generates safe trajectories considering occupancy prediction, traffic rules, and ride comfort

## System Overview

<img src="__assets__/overview.png" width="1000px">


## Modules

### Perception

The perception module constructs a spatio-temporal BEV representation from multi-camera inputs. The encoder uses sequence repetition, while the decoder employs sequence alignment.

### Prediction

The prediction module utilizes a dual-pathway SNN, where one pathway encodes past information and the other predicts future distributions. The outputs from both pathways are fused.

### Planning

The planning module optimizes trajectories using Spiking Gated Recurrent Units (SGRUs), taking into account static occupancy, future predictions, comfort, and other factors.

## Get Started

### Setup

```
conda env create -f environment.yml
```

### Training

First, go to `/sad/configs` and modify the configs. Change the NAME in MODEL/ENCODER to the model we provided. 

```
# Perception module pretraining
bash scripts/train_perceive.sh ${configs} ${dataroot}

# Prediction module pretraining 
bash scripts/train_prediction.sh ${configs} ${dataroot} ${pretrained}

# Entire model end-to-end training
bash scripts/train_plan.sh ${configs} ${dataroot} ${pretrained}
```
