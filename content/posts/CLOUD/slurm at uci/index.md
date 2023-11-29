---
title: Run opengpu cluster with slurm at UCI
date: 2023-11-21
tags: [cloud, ml, uci]
image: "aas-vs.jpg"
draft: true
---


https://stanford-rc.github.io/docs-earth/docs/slurm-basics

Running Jupyter on Slurm GPU Nodes
Running Jupyter on Slurm
Several scenarios come up where you might want to run your Jupyter server via Slurm. This enables you to run your Jupyter server on a Slurm node with GPUs. This documentation specifically covers this process.

With Nero On-Prem, you’ll need to submit this as a Slurm job. That way, your jupyter lab server gets placed on a Slurm node with enough resources to host it. To summarize: We are creating a slurm job that runs jupyterlab on a Slurm node, for up to 2 days (max is 7). Once running, we are going to connect to the jupyterlab instance with SSH port forwarding from our local laptop. A tunnel must be created as you cannot directly SSH to Slurm nodes on Nero.

First create a Slurm sbatch file:

Use Terminal On Your Laptop:

1) SSH to Nero On-Prem

ssh <sunetID>@nero.compute.stanford.edu

2) Create your sbatch file. You can use your text editor of choice.

vi jupyterLab.sh

Paste the following text into your sbatch script, and save the file.

#!/bin/bash
#SBATCH --job-name=jupyter
#SBATCH --partition=gpu
#SBATCH --gres=gpu:1
#SBATCH --time=2-00:00:00
#SBATCH --mem=50GB
#SBATCH --output=/home/<sunetID>/jupyter.log

module load anaconda
source activate /share/sw/open/anaconda/3

cat /etc/hosts
jupyter lab --ip=0.0.0.0 --port=8888

Replace the <sunetID> part of your #SBATCH --output=home/<sunetID>/jupyter.log with your SUNetID. Or, provide an alternate path for your log output.

Note: You can activate a custom Jupyter conda environment if you want to use custom packages by changing the path for the “source activate /path/here” section of the above code.

This tells Slurm to launch a Jupyter Lab server on the node with your requested resources, over port 8888.

Now we need to send this as a job to Slurm.


3) Submit this sbatch to Slurm:

sbatch jupyterLab.sh


4) Now, you can check that your job is running:

squeue -u $USER


Once it is running you can continue…

5) Wait 10 minutes after your job starts for Jupyter to start. Check the log output to find out the IP we need to use to create an SSH tunnel:

Via Terminal ON Nero:

cat ~/jupyter.log


The log file will output something like this:

Kubernetes-managed hosts file.
127.0.0.1 localhost
::1 localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
fe00::0 ip6-mcastprefix
fe00::1 ip6-allnodes
fe00::2 ip6-allrouters

10.1.80.10 slurm-gpu-compute-dell-c7wfg

[I 04:09:17.556 NotebookApp] Writing notebook server cookie secret to /home/wlaw/.local/share/jupyter/runtime/notebook_cookie_secret
[I 04:09:20.221 NotebookApp] JupyterLab beta preview extension loaded from /share/sw/open/anaconda/3/lib/python3.6/site-packages/jupyterlab
[I 04:09:20.222 NotebookApp] JupyterLab application directory is /share/sw/open/anaconda/3/share/jupyter/lab
[I 04:09:20.408 NotebookApp] Serving notebooks from local directory: /
[I 04:09:20.408 NotebookApp] The Jupyter Notebook is running at:

[I 04:09:20.408 NotebookApp] http://(slurm-gpu-compute-dell-c7wfg or 127.0.0.1):8888/?token=adec35ec9b6d12776c28c67cbe87dda9ac90ad913b691f3a

Note the IP address in the first part (10.1.80.10 next to slurm-gpu-…), you’ll need that info (your IP will be different) to setup a port-forwarding connection.

6) Then on your laptop, open a new Terminal Window and create an SSH tunnel:

ssh -L8888:10.1.80.10:8888 <sunetID>@nero.compute.stanford.edu

Important: You must replace the IP address (10.1.80.10) in the command below with your IP address from step 5

Note that whatever your log output says for IP you will need to use in the command above. DO NOT just copy and paste the example, you have to replace the IP address (the 10.1.80.10 part) to be the one your log output specifies.


7) On your laptop open a browser window and you can then browse to:

http://127.0.0.1:8888/?token=adec35ec9b6d12776c28c67cbe87dda9ac90ad913b691f3a

Important: Replace the “?token=x” part of the URL with your token from step 5

Note that this is copied from the output log file where it defines your Jupyter address and TOKEN. You MUST copy the token from the log out put, and cannot just use the example above. It may take up to 10 minutes for the “jupyter.log” output to show you the text with your token.


For the remainder of your job run, the IP and port will stay the same. If you close your laptop you will need to recreate an SSH Tunnel - you can reuse the “ssh -L8888” command above. If your job ends on Nero On-Prem, you need to resubmit your slurm job, and then modify your SSH Tunnel command with the new IP address. Jobs last for a maximum of 7 days.

If at any time port 8888 seems to already be in use, you can change the port (any above 1024) in your sbatch file, and in the corresponding commands for your SSH tunnel.