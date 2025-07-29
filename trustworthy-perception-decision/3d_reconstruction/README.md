![Laboratory Logo](image/logo.png)

# trustworthy_3d_Reconstruction

### Environment

Before you execute any of the modules in this project, please install the conda environment:

```shell script
conda env create -f environment.yml
``` 

This will create the `SingleViewReconstruction` environment, you can use it by:

```shell script
conda activate SingleViewReconstruction
```

This uses `Tensorflow 1.15` with `python 3.7`. This also includes some OpenGL packages for the visualizer.

### Quick and easy complete run of the pipeline

There is a script, which provides a full run of the BlenderProc pipeline, you will need the `"SingleViewReconstruction"` environment.

But, be aware before you executed this script. That it will execute a lot of code and download a lot of stuff to your PC.

This program will download `BlenderProc` and then afterwards `blender`. It will also download the `SceneNet` dataset and the corresponding texture lib used by `SceneNet`.
It will render some color & normal images for the pipeline and will also generate a true output voxelgrid to compare the results to best possible.

Before running, this make sure that you adapt the `SDFGen/CMakeLists.txt` file. See this [README.md](SDFGen/README.md).

```shell script
python run_on_example_scenes_from_scenenet.py
```

This will take a while and afterwards you can look at the generated scene with: 

```shell script
python TSDFRenderer/visualize_tsdf.py BlenderProc/output_dir/output_0.hdf5
```

### Data generation

This is a quick overview over the data generation process, it is all based on the SUNCG house files.

1. The SUNCG house.json file is converted with the SUNCGToolBox in a house.obj and camerapositions file, for more information: [SUNCG](SUNCG)
2. Then, these two files are used to generate the TSDF voxelgrids, for more information: [SDFGen](SDFGen)
3. The voxelgrid is used to calculate the loss weights via the [LossCalculatorTSDF](LossCalculatorTSDF)
4. They are used to first the train an autoencoder and then compress the 512³ voxelgrids down to a size of 32³x64, which we call encoded. See [CompressionAutoEncoder](CompressionAutoEncoder).
5. Now only the color & normal images are missing, for that we use [BlenderProc](https://github.com/DLR-RM/BlenderProc) with the config file defined in [here](BlenderProc).

These are then combined with this [script](SingleViewReconstruction/generate_tf_records.py) to several tf records, which are then used to [train](SingleViewReconstruction/train.py) our SingleViewReconstruction network.

### Download of the trained models

We provide a [script](download_models.py) to easily download all models trained in this approach:

1. The [SingleViewReconstruction](SingleViewReconstruction) model
2. The Autoencoder Compression Model [CompressionAutoEncoder](CompressionAutoEncoder)
3. The Normal Generation Model [UNetNormalGen](UNetNormalGen)

```shell script
python download_models.py
```

