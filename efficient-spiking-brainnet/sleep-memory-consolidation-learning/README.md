# **S**leep-based **M**emory **C**onsolidation **L**earning

**Title:** **S**leep-based **M**emory **C**onsolidation **L**earning



SMCL proposes a novel continual learning framework for (online) continual learning where a slow network gradually accumulates knowledge to improves its general representation over time and a fast network utilizes the slow representation to quickly learn new information.

![Zhuoxi](logo.png)

# Requirements
- python 3.7.3
- pytorch >= 1.8
- torchvision >= 0.9
- Kornia >= 0.5.0

# Benchmarks
### 1. Prepare data
The `data/` folders contains the train and test splits for the miniImageNet and CORE50 benchmarks. Download the raw data and modify the path in the `csv` files to point to the raw data folder.

### 2. Run experiments
To replicate our results on the task aware and task free settings, run
```
chmod +x scripts/*
./scripts/task_aware.sh
./scripts/task_free.sh
```

The results will be put in the `resuts/` folders.

### Semi-supervised learning setting
For the semi-supervised continual learning experiments, run
```
./scripts/semi.sh --rho 0.1
./scripts/semi.sh --rho 0.25
```
The parameter `rho` indicates the percentage of data that are labeled (e.g. 10% or 25%).

