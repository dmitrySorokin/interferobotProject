# Interferobot: aligning an optical interferometer by a reinforcement learning agent 

This repository is the official implementation of [Interferobot: aligning an optical interferometer by a reinforcement learning agent ](http://arxiv.org/abs/2006.02252).

<p float="center">
  <img src="gif/0.gif" width="400"/>
  <img src="gif/2.gif" width="400"/>
</p>


## Structure
This repo contains the following four submodules:

* interf_game - the interactive user interface for both simulator and hardware interferometer
* gym_interf  - gym environment for interferometer simulator  
* iron_interf  - gym environment for hardware interferometer
* interf_dqn  - code to train double dueling dqn agent


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

| model | description | 
|---|---|
| interf_game/ablation_models/all_random | model trained with all doman randomizations | 
| interf_game/ablation_models/no_brightness_random |  model trained without brightness randomization | 
| interf_game/ablation_models/no_channel_shift | model trained without duty cycle randomization |
| interf_game/ablation_models/no_noise | model trained without noise white nose |
| interf_game/ablation_models/no_radius_random | model trained without radius randomization |

## Running

### Interferometer simulator 
Run simulator in iteractive mode:
```
cd interf_game
python3 main_sim.py --model=path/to/model
```

You can try to align the interferometer manually by keyboard:
* w, a, s, d - controls mirror 1
* i, j, k, l - controls beam splitter 2
* r - reset the simulator to a random position
* q - move to an aligned state
* x - to change the step size

Or let the agent do this:
* press space to run/stop the agent

### Hardware interferometer
The same functionality is available for hardware interferometer in interf_game/main.py

## Training

To train Interferobot with all domain randomizations run:
```
cd interf_dqn
./run.sh
```

## Evaluation
Evaluate the trained agent for 100 episodes:
```
cd interf_game
python3 eval_sim.py --model=ablation_models/all_random --ngames=100 --log_dir=all_random
```
This will create directory all_random with files:
* log.txt - semicolon separated values igame, istep, visib_camera, visib_device
* game_{igame}\_step_{istep}.npz - numpy arxieves with fields state, action, next_state, done, visib_device, visib_camera


To visualize episoge 0 run: 
```
./show.py --game_id=0 --folder=all_random
```

## Experimental data

### Evaluation data 
Evaluation episodes collected the physical interferometer for all trained models in the format described above are available at [google drive](https://drive.google.com/drive/folders/1hJ7qZNdD0RXapVm97u8iSA2aWGZymRJf?usp=sharing). 

### Videos
Alignment videos generated for all_random model evaluated at physical interferometer are available at [google drive](https://drive.google.com/drive/folders/1aCN76hxIwY7zNbrZd84NIdNhdQE5yzfP?usp=sharing).

## Results

Our models trained entirely in simulation achieves the following performance in zero-shot Sim2Real transfer:

| Model name     | visibility | return |
| ------------------ |---------------- | -------------- |
| all_random          |  **0.96 ± 0.02** | **221 ± 54** |
| no_radius_random    | 0.74 ± 0.20     | 85 ± 69     |
| no_brightness_random | 0.91 ± 0.04     | 178 ± 39    |
| no_noise            | 0.82 ± 0.07     | 129 ± 43    |
| no_channel_shift     | 0.89 ± 0.07     | 200 ± 42    | 
