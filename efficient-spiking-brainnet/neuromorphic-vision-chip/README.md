# **N**euromorphic **V**ision **C**hip

This repository contains code for **NVC** - **N**euromorphic **V**ision **C**hip. NVC combines neuromorphic algoriths, sensors, and hardware to perform accurate, real-time robotic localization using visual place recognition (VPR). 

![logo](logo.png)

## Installation and setup
To run NVC, please download this repository and install the required dependencies.

### Install dependencies
All dependencies can be instlled from our [PyPi package](), local `requirements.txt`, or from [conda-forge]() (recommended to use [micromamba](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html)). Please ensure your Python version is <= 3.11.

## Quick start
Get started using our pretrained models and datasets to evaluate the system. 

### Run the inferencing model
To run a simulated event stream, you can try our pre-trained model and datasets. Using the `--sim_mat` and `--matching` flag will display a similarity matrix and perform Recall@N matching based on a ground truth matrix.

```console
python main.py --sim_mat --matching
```

### Train a new model
New models can be trained by parsing the `--train_model` flag. Try training a new model with our provided reference dataset.

```console
# Train a new model
python main.py --train_model
```

### Optimize network hyperparameters
For new models on custom datasets, you can optimize your network hyperparameters using [Weights & Biases](https://wandb.ai/site) through our convenient `optimizer.py` script.

```console
# Optimize network hyperparameters
python optimizer.py
```

For more details, please visit the [Wiki](https://github.com/AdamDHines/LENS/wiki/Setting-up-and-using-the-optimizer).

### Deployment on neuromoprhic hardware
If you have a SynSense Speck2fDevKit, you can try out LENS using our pre-trained model and datasets by deploying simulated event streams on-chip.

```console
# Generate a timebased simulation of event streams with pre-recorded data
python main.py --simulated_speck --sim_mat --matching
```

Additionally, models can be deployed onto the Speck2fDevKit for low-latency and energy efficient VPR with sequence matching in real-time.

First, install `samna`.

```console
# Install samna from pip
pip install samna
# Check that the package imports properly
python
> import samna
```

Then, use the `--event_driven` flag to start the online inferencing system.

```console
# Run the online inferencing model
python main.py --event_driven
```

