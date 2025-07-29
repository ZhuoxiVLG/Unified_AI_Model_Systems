![Laboratory Logo](image/logo.png)

# Efficient Attention Transformers


## Installation

Install the dependency packages using the environment file `smat_pyenv.yml`.

Generate the relevant files:
```
python tracking/create_default_local_file.py --workspace_dir . --data_dir ./data --save_dir ./output
```
After running this command, modify the datasets paths by editing these files
```
lib/train/admin/local.py  # paths about training
lib/test/evaluation/local.py  # paths about testing
```

## Training

* Set the path of training datasets in `lib/train/admin/local.py`
* Place the pretrained backbone model under the `pretrained_models/` folder
* For data preparation, please refer to [this](https://github.com/botaoye/OSTrack/tree/main)
* Uncomment lines `63, 67, and 71` in the [base_backbone.py](https://github.com/goutamyg/SMAT/blob/main/lib/models/mobilevit_track/base_backbone.py) file. 
Long story short: The code is opitmized for high inference speed, hence some intermediate feature-maps are pre-computed during testing. However, these pre-computations are not feasible during training. 
* Run
```
python tracking/train.py --script mobilevitv2_track --config mobilevitv2_256_128x1_ep300 --save_dir ./output --mode single
```
* The training logs will be saved under `output/logs/` folder

## Pretrained tracker model
The pretrained tracker model can be found [here](https://drive.google.com/drive/folders/1TindIEwu82IvtozwL4XQFrSnFE2Z6W4y)

