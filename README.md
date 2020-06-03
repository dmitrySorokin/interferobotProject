# Interferobot: aligning an optical interferometer by a reinforcement learning agent 

This repository is the official implementation of [Interferobot: aligning an optical interferometer by a reinforcement learning agent ](https://arxiv.org/abs/TODO). 

<img src="gif/0.gif" width="400"/>
<img src="gif/2.gif" width="400"/>
<img src="gif/20.gif" width="400"/>


> 📋Optional: include a graphic explaining your approach/main result, bibtex entry, link to demos, blog posts and tutorials

## Structure
This repo contains the following four submodules 
* interf_game --- interactive user interface
* gym_interf --- gym environment for interferometer simulator
* interf_dqn --- code to train double dueling dqn agent
* iron_interf --- gym environment for hardware interferometer

## Installation

### Clone the repo including submodules 
```
git clone --recurse-submodules git@github.com:dmitrySorokin/interferobotProject.git
```

### interferometer simulator
```
cd gym_interf
pip3 install -r requirements.txt
pip3 install -e ./
```

### hardware interferometer

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

## Running
```
cd interf_game
python3 main_sim.py
```
```
cd interf_game
python3 eval_sim.py
```

```
cd interf_game
python3 main.py
```
```
cd interf_game
python3 eval.py
```



### hardware interferometer

> 📋Describe how to set up the environment, e.g. pip/conda/docker commands, download datasets, etc...

## Training

To train the model(s) in the paper, run this command:

```train
python train.py --input-data <path_to_data> --alpha 10 --beta 20
```

> 📋Describe how to train the models, with example commands on how to train the models in your paper, including the full training procedure and appropriate hyperparameters.

## Evaluation

To evaluate my model on ImageNet, run:

```eval
python eval.py --model-file mymodel.pth --benchmark imagenet
```

> 📋Describe how to evaluate the trained models on benchmarks reported in the paper, give commands that produce the results (section below).

## Pre-trained Models

You can download pretrained models here:

- [My awesome model](https://drive.google.com/mymodel.pth) trained on ImageNet using parameters x,y,z. 

> 📋Give a link to where/how the pretrained models can be downloaded and how they were trained (if applicable).  Alternatively you can have an additional column in your results table with a link to the models.


## Datasets

[google drive](https://drive.google.com/drive/folders/1hJ7qZNdD0RXapVm97u8iSA2aWGZymRJf?usp=sharing)

## Videos

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
