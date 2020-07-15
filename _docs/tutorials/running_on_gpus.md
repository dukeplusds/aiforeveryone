---
title: Running On The GPU
category: Tutorials
order: 4
---

### Interactive Session

Interactive sessions on the Duke Research Computing Cluster allows us to train a network interactively. That is, we can run the script in the console without submitting it to the scheduler. This allows us to view the output of the network including the loss and any print statements in real time. This method is great for tests and fast training networks. It is suggested that you don't use interactive sessions for training over days/weeks.

#### 1) SSH into your Account

```
ssh <your-id>@dcc-slogin-01.oit.duke.edu
```

#### 2) Reserve a GPU + Memory
```
srun -p dsplus-gpu --account=plusds --gres=gpu:1 -c 10 --mem=10G --pty bash -i
```

#### 3) Load the Python module

```
module load Python-GPU/3.6.5
```

#### 4) Run your Code and exit

```
python  my_new_gan.py
```


### Batch Session

Batch sessions allow us to write a bash script for training on the scheduler. This allows us to submit the script and have it run when resources become available. It allows us to train multiple nets simultaneously with different hyperparameters. We should use batch scripts for long-running training, multiple GPU training, or for training multiple network  simultaneously.

#### 1) Define Batch Script

```
#!/bin/bash
#SBATCH -e slurm.err
#SBATCH -o nbody.out
#SBATCH -p dsplus-gpu --gres=gpu:1 
#SBATCH --account=plusds
#SBATCH --mem=10G 
##SBATCH -c 6 
module load Python-GPU/3.6.5
python mygan/gans_trial/run_gan.py
```

#### 2) Run Batch Script 

```
sbatch test_gan.sh
```

### Running Jupyter Notebook

Jupyter Notebooks are a key part of every data scientists toolset. Jupyter Notebooks allow users to develop code in a browser based IDE and execute code interactively. Setting up Jupyter Notebooks on the Duke Compute Cluster takes a few extra steps. Please find the steps below for the +DS Advanced Project working group, adapted from my colleague (Mark Olson)'s [tutorial](https://mjvo.github.io/tutorials/machine-learning/pytorch-dcgan/)

#### 1) SSH into your Account

```
ssh <your-id>@dcc-slogin-01.oit.duke.edu
```

#### 2) Reserve a GPU + Memory
```
srun -p dsplus-gpu --account=plusds --gres=gpu:1 -c 10 --mem=10G --pty bash -i
```

#### 3) Load the Python module

```
module load Python-GPU/3.6.5
```

#### 4) Set the runtime environment for Jupyter

```
export XDG_RUNTIME_DIR=""
```

#### 5) Set a port number

```
export myport=48477
```

#### 6) Print out the SSH tunnel information

```
echo "ssh -NL $myport:$(hostname):$myport $USER@dcc-slogin.oit.duke.edu"
```

This should return `ssh -NL 48477:dcc-dsplus-gpu-01:48477 <your_id>@dcc-slogin.oit.duke.edu`

#### 7) Establish an SSH tunnel in a new Terminal session
*In a new terminal session*, paste the command from step #7 (eg. `ssh -NL 48477:dcc-dsplus-gpu-01:48477 <your_id>@dcc-slogin.oit.duke.edu`)

Upon password authentication, it will seem like nothing is happening

#### 8) In the first tab, launch Jupyter notebook
*In the first session*, run:
```
jupyter-notebook --no-browser --port=$myport --ip='0.0.0.0'
```
Note the token that is printed as Jupyter starts running

#### 9) Navigate to Jupyter in you browser
*In your browser* navigate to:
```
http://localhost:45678
```
You will be prompted for a token password. The token password is printed after launching jupyter notebook 
eg.:
```
http://dcc-dsplus-gpu-01:48477/?token=283abf4005804f864f654a49911130de6567e9283704baba&token=283abf4005804f864f654a49911130de6567e9283704baba
```

### Running Array Jobs

```
#!/bin/bash
#SBATCH –e slurm.err
#SBATCH --array=1-5
python myCode.py
```

```py
import os
rank=int(os.environ['SLURM_ARRAY_TASK_ID']) 
print(rank)
```

```
sbatch my_array.sh
```

### External Cloud Computing

There are many other option for accessing GPU computing outside of the Duke resources. Many of them do cost money, but generally range from free to ~$1.40/hr per GPU to rent. Please find an exhaustive list of GPU resources, how to access each of them and general price points at the link below.

Please refer to the [FastAI Course website](https://course.fast.ai/#using-a-gpu) for a complete list and directions 



