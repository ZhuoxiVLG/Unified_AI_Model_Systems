![Laboratory Logo](image/logo.png)

# AD-PDILM: Integrated Sensing and Decision-Making Large Model

AD-PDILM is an integrated sensing and decision-making large model that achieves full integration of perception and decision-making through innovative object-level scene representation and a Transformer-based large language model architecture. The model extracts high-quality object features from a vision large model and, through imitation learning, uses large-scale expert driving data to directly map scene representations to future trajectories. In simulation experiments, AD-PDILM demonstrates outstanding performance, achieving a target perception accuracy of 99.74%, lateral motion control error of 0.11m, heading control error of 0.14°, path planning error of 0.06m, average model response time of 27ms, lane change and overtaking success rate of 99.92%, ramp passage success rate of 99.95%, and continuous autonomous driving for 2 hours at an average speed of 80km/h.

# Contents
* [Training](#training)
* [Evaluation](#evaluation)
* [Sensing AD-PDILM](#sensing-ad-pdilm)

## Training
To run AD-PDILM training on a dataset, execute:
```bash
python Model/lit_train.py model=AD-PDILM
```
To modify any hyperparameters, refer to `Model/AD-PDILM.yaml`. For general training settings (e.g., number of GPUs), refer to `Model/config.yaml`.

## Evaluation
This will evaluate the AD-PDILM model on the specified benchmark (default: longest6). Configurations are specified in the `carla_agent_files/config` folder.

Start the Carla server (see [Data Generation](#data-generation)).  
When the server is running, start the evaluation:
```bash
python leaderboard/scripts/run_evaluation.py experiments=AD-PDILMmedium3x eval=longest6
```
Evaluation results can be found in the newly created evaluation folder within the model folder. For a (very minimal) visualization, you can set the `viz` flag (e.g., `python leaderboard/scripts/run_evaluation.py user=$USER experiments=AD-PDILMmedium3x eval=longest6 viz=1`).

## Sensing AD-PDILM
We have released two AD-PDILM agents for the CARLA Leaderboard. For the SENSORS track, we use a perception module to predict routes. In the MAP track model, we obtain route information from the map. The code is adapted from the [TransFuser (PAMI 2022) repo](https://github.com/autonomousvision/transfuser) for our use case. Configurations are specified in the `carla_agent_files/config` folder. The perception model's configuration is in `model/config.py`.

### SENSORS
Start the Carla server.  

When the server is running, start the evaluation:
```bash
python leaderboard/scripts/run_evaluation.py experiments=AD-PDILMSubmission track=SENSORS eval=longest6 save_path=SENSORSagent
```
Visualization can be activated using the `viz` flag, and unlocking from the TransFuser repo can be activated using the `experiments.unblock` flag.

### MAP
Start the Carla server.  

When the server is running, start the evaluation:
```bash
python leaderboard/scripts/run_evaluation.py experiments=AD-PDILMSubmissionMap track=MAP eval=longest6 save_path=MAPagent
```
Visualization can be activated using the `viz` flag, and unlocking from the TransFuser repo can be activated using the `experiments.unblock` flag.