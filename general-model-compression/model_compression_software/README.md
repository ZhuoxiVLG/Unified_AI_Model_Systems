![Laboratory Logo](image/logo.png)

# Low Code Operator Adaptation Model Compression

## Installation
To run the code, please install the dependencies using 

``` bash
pip install -r requirements.txt 
```

## Training and Evaluation

### Layerwise Unified Compressed and Adaptive Layer Tuning
To launch the training of the whole Edge-LLM algorithm, please use the following command: 

``` bash
bash ./scripts/edge_llm_train.sh
```

We also provide the script to run each enablers of our proposed framework below 

### Quantize Model
In our implementation, we build our quantization mmethod on top of [LLM-QAT](https://github.com/facebookresearch/LLM-QAT). To try our proposed layer-wise pruning technique to prune the model, please use the following command to quantize and tune the model: 

``` bash
bash ./scripts/layer_wise_quantization.sh
```

### Prune Model
In our implementation, we build our pruning method on top of  [SparseGPT](https://github.com/IST-DASLab/sparsegpt). To only use our proposed layer-wise pruning technique to prune the model, please use the following command to prune and tune the model: 

``` bash
bash ./scripts/layer_wise_pruning.sh
```

### Layerwise Unified Compressed Model
To test the model performance with only the layer-wise unified compression, please use the following command to compress and tune the model: 

``` bash
bash ./scripts/layer_wise_pruning_quantization.sh
```


