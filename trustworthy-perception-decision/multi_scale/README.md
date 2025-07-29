![Laboratory Logo](image/logo.png)

# Multi Scale Swin-Transformer

### Prerequisites

- This project is implemented in Pytorch (>1.8). Thus please install Pytorch first.

- ctcdecode==0.4 [[parlance/ctcdecode]](https://github.com/parlance/ctcdecode)，for beam search decode.

- sclite [[kaldi-asr/kaldi]](https://github.com/kaldi-asr/kaldi), install kaldi tool to get sclite for evaluation. After installation, create a soft link toward the sclite:    
  `ln -s PATH_TO_KALDI/tools/sctk-2.4.10/bin/sclite ./software/sclite`

### Data Preparation

1. Download the RWTH-PHOENIX-Weather 2014 Dataset [[download link]](https://www-i6.informatik.rwth-aachen.de/~koller/RWTH-PHOENIX/). Our experiments based on phoenix-2014.v3.tar.gz.

2. Modify the dataset_preprocess.py file to reflect the location of the dataset.

3. The original image sequence is 210x260, we resize it to 256x256 for augmentation. Run the following command to generate gloss dict and resize image sequence.     

   ```bash
   cd ./preprocess
   python data_preprocess.py --process-image --multiprocessing
   ```

### Training
To train the Multi Scale Swin-Transformer model on phoenix14, run the command below:

`python main.py`

The Swin-Small architeture is used by default. If you would like to train your model using the Swin-Tiny strcuture, in the baseline.yaml file, change the c2d_type to 'swin_t'.  

### Inference
To evaluate the trained model, run the command below：

`python main.py --load-weights {name}.pt --phase test`