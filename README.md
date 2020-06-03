# Interferobot: aligning an optical interferometer by a reinforcement learning agent 

This repository is the official implementation of [Interferobot: aligning an optical interferometer by a reinforcement learning agent ](https://arxiv.org/abs/TODO). 

<p float="center">
    <img src="gif/0.gif" width="400"/>
    <img src="gif/2.gif" width="400"/>
</p>


## Structure
This repo contains the following four submodules 

|---|---|
| interf_game  |  interactive user interface  for both simulator and hardware interferometer| 
| gym_interf    |  gym environment for interferometer simulator  | 
|  iron_interf    |  gym environment for hardware interferometer |
|  interf_dqn    |  code to train double dueling dqn agent |
|---|---|


## Installation

### Clone the repo including submodules 
```
git clone --recurse-submodules git@github.com:dmitrySorokin/interferobotProject.git
```

### * interferometer simulator
```
cd gym_interf
pip3 install -r requirements.txt
pip3 install -e ./
```

### * hardware interferometer

apt-get install libusb-1.0-0 (to install drivers) 
pip3 install pyusb (1.0.2) (python bindings) 
pip3 install pyueye (python bindings)
http://www.sanxo.eu/content/techtips/TechTip_Embedded_Vision_Kit_EN.pdf
https://en.ids-imaging.com/download-ueye-emb-hardfloat.html
/usr/bin/ueyeusbd

```
cd iron_interf
pip3 install -e ./
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

### interferometer simulator 
to run it in iteractive mode do:
```
cd interf_game
python3 main_sim.py
```
it will start pygame interface. You can try to align the interferometer manually by using keyboard:
* w, a, s, d - controlls mirror 1
* i, j, k, l  - controlls beam splitter 2
* press r to reset the simulator to a random position
* press q to move to alligned state
* press space to run the trained agent


to evaluate the trained agent for 100 episodes run:
```
cd interf_game
python3 eval_sim.py
```

### hardware interferometer
the same functionality is available for hardware interferometer in 
```
main.py and eval.py
```

## Training

To train the model(s) in the paper, run this command:

```
cd interf_dqn
./run.sh
```

## Evaluation

To evaluate my model on ImageNet, run:

```eval
python eval.py --model-file mymodel.pth --benchmark imagenet
```

> 📋Describe how to evaluate the trained models on benchmarks reported in the paper, give commands that produce the results (section below).


## Experimental data

### 
[google drive](https://drive.google.com/drive/folders/1hJ7qZNdD0RXapVm97u8iSA2aWGZymRJf?usp=sharing)

### Videos

[google drive](https://drive.google.com/drive/folders/1aCN76hxIwY7zNbrZd84NIdNhdQE5yzfP?usp=sharing)

## Results

Our model achieves the following performance on :

### [Image Classification on ImageNet](https://paperswithcode.com/sota/image-classification-on-imagenet)

| Model name         | Top 1 Accuracy  | Top 5 Accuracy |
| ------------------ |---------------- | -------------- |
| My awesome model   |     85%         |      95%       |

> 📋Include a table of results from your paper, and link back to the leaderboard for clarity and context. If your main result is a figure, include that figure and link to the command or notebook to reproduce it. 


## Contributing

> 📋Pick a licence and describe how to contribute to your code repository. 
