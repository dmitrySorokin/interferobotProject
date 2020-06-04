# Interferobot: aligning an optical interferometer by a reinforcement learning agent 

This repository is the official implementation of [Interferobot: aligning an optical interferometer by a reinforcement learning agent ](http://arxiv.org/abs/2006.02252).

<p float="center">
    <img src="gif/0.gif" width="400"/>
    <img src="gif/2.gif" width="400"/>
</p>


## Structure
This repo contains the following four submodules:

* interf_game  -  interactive user interface for both simulator and hardware interferometer
* gym_interf    -  gym environment for interferometer simulator  
* iron_interf    -  gym environment for hardware interferometer
* interf_dqn    -  code to train double dueling dqn agent


## Installation

### Clone including submodules 
```
git clone --recurse-submodules git@github.com:dmitrySorokin/interferobotProject.git
```

### Interferometer simulator
```
pip3 install -e gym_interf
```
### User interface 
```
pip3 install -r interf_game/requirements.txt
```

### Hardware interferometer
Install drivers for mirror mounts and python bindings
```
apt-get install libusb-1.0-0
pip3 install pyusb (1.0.2)
```

Install drivers for IDS camera from [here](https://en.ids-imaging.com/download-ueye-emb-hardfloat.html
) and python bindings
```
pip3 install pyueye
```

Run camera daemon
```
./usr/bin/ueyeusbd
```

Install gym environment
```
pip3 install -e iron_interf
```

## Pre-trained Models

Pretrained models located in interf_game submodule:

|  model |  description | 
|---|---|
| interf_game/ablation_models/all_random  |  model trained with all doman randomizations  | 
| interf_game/ablation_models/no_brightness_random  |   model trained without brightness randomization | 
|  interf_game/ablation_models/no_channel_shift  |  model trained without duty cycle randomization |
|  interf_game/ablation_models/no_noise  |  model trained without noise white nose |
|  interf_game/ablation_models/no_radius_random  |  model trained without radius randomization |

## Running

### Interferometer simulator 
Run simulator in iteractive mode:
```
cd interf_game
python3 main_sim.py #TODO add agent args
```

You can try to align the interferometer manually by keyboard:
* w, a, s, d - controlls mirror 1
* i, j, k, l  - controlls beam splitter 2
* r - reset the simulator to a random position
* q - move to alligned state
* x - to change the step size

Or let the agent do this:
* press space to run / stop the agent

### Hardware interferometer
The same functionality is available for hardware interferometer:
```
cd interf_game
python3 main.py
```

## Training

To train the model(s) in the paper, run this command:

```
cd interf_dqn
./run.sh #TODO add randomization args?
```

## Evaluation


Evaluate the trained agent for 100 episodes:
```
cd interf_game
python3 eval_sim.py #TODO add agent args
```

> 📋Describe how to evaluate the trained models on benchmarks reported in the paper, give commands that produce the results (section below).


## Experimental data

### Evaluation data
//TODO describe format, folders
[google drive](https://drive.google.com/drive/folders/1hJ7qZNdD0RXapVm97u8iSA2aWGZymRJf?usp=sharing)

### Videos

[google drive](https://drive.google.com/drive/folders/1aCN76hxIwY7zNbrZd84NIdNhdQE5yzfP?usp=sharing)

## Results

Our models trained entierly in simulation achieves the following performance in Sim2Real transter:

| Model name         | visibility | return |
| ------------------ |---------------- | -------------- |
| all_random                    |   **0.96 ± 0.02**  |  **221 ± 54**  |
| no_radius_random        | 0.74 ± 0.20         | 85 ± 69          |
| no_brightness_random | 0.91 ± 0.04         | 178 ± 39        |
| no_noise                       | 0.82 ± 0.07         | 129 ± 43        |
| no_channel_shift          | 0.89 ± 0.07         | 200 ± 42        | 


## Contributing

> 📋Pick a licence and describe how to contribute to your code repository. 
