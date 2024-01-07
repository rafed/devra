---
title: Run JupyterLab on OpenGPU Cluster with SLURM at UCI
date: 2024-01-02
tags: [cloud, ml, uci]
image: "slurm.png"
---

As a graduate student in UCI's IN4MATIX program, exploring the resources available on the Donald Bren School Computing Support page ([wiki.ics.uci.edu](https://wiki.ics.uci.edu/doku.php)) is truly fascinating. While most of the documentation is quite clear, I noticed that there is a lack of detailed guidance on utilizing the OpenGPU cluster. In this guide, I will provide you with a comprehensive walkthrough to help you effectively harness the power of the GPUs.

#### 1. Prerequisites
* You will need an ICS account
* You need ssh installed on your system
* Familiarity with JupyterLab is a plus

#### 2. SSH to ICS Openlab

SSH to the ICS OpenLab Linux host. Use your ICSusername password to log in (N.B. This is different from UCINetId)

```bash
$ ssh <ICSusername>@openlab.ics.uci.edu
```

After logging in you should see your ICS home directory.

#### 3. Create sbatch FIle

Create a sh file (technically sbatch file). You your favorite text editor to do it.

```bash
$ vi jupyterLab.sh
```

Paste the following text into your sbatch script, and save the file.

```bash
#!/bin/bash
#SBATCH --job-name=jupyter
#SBATCH --partition=gpu
#SBATCH --gres=gpu:1
#SBATCH --time=1-00:00:00
#SBATCH --mem=20GB
#SBATCH --output=/home/<ICSusername>/jupyter.log

cat /etc/hosts
jupyter lab --ip=0.0.0.0 --port=8888
```

Make sure to replace the <ICSusername> part of your ```#SBATCH --output=home/<ICSusername>/jupyter.log``` with your ICSusername.

This file will allow us to tell Slurm to launch a Jupyter Lab server on the node with your requested resources over port 8888.

#### 4. Load Slurm

Now we will need to interact with Slurm. The slurm-client is already installed on the machine. You can activate it by

```bash
$ module load slurm
```

Now we can interact with the slurm queue.

#### 5. Submit the sbatch to Slurm

Let's send the script we prepared as a job to Slurm.

```bash
$ sbatch jupyterLab.sh
```

Now, you can check that your job is running:

```bash
$ squeue -l
$ squeue -u $USER ## or
```

You should see something like this

```bash
$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           2977100 opengpu.p   xxxxxx dddddddd  R   10:01:13      1 poison
           2910105 openlab.p yyyyyyyy eeeeeeee  R 22-05:23:37     1 circinus-32
           2961968 openlab.p zzzzzzzz    fffff  R 12-04:19:50     1 circinus-81
           2976070 openlab.p      aaa gggggggg  R 6-07:19:49      1 circinus-21
           2962837 openlab.p bbbbbbbb    hhhhh  R 11-12:14:34     1 circinus-17
           2961916 openlab.p cccccccc    hhhhh  R 12-11:47:43     1 circinus-48
```

Once the job is in running state you can continue to the next steps. However, whether it is running depends on how many other people are using it. I got my first job after 5 or 6 days.

#### 6. Create an SSH tunnel for access

Once the job is up and running on the GPUs check the log output to find out the address we need to create an SSH tunnel:

```bash
$ cat ~/jupyter.log | grep http

    http://poison.ics.uci.edu:8888/lab?token=64ddb49f56acc8569f2d237cce504e7edd1ef559e76a23e7
    http://127.0.0.1:8888/lab?token=64ddb49f56acc8569f2d237cce504e7edd1ef559e76a23e7
```


Note the address in the first part (poison.ics.uci.edu), you’ll need that info (your address will be different) to setup a port-forwarding connection.

Now, on your laptop, open a new Terminal Window and create an SSH tunnel.

```bash
ssh -L8888:10.1.80.10:8888 <ICSusername>@openlab.ics.uci.edu
```

#### 7. Open JupyterLab

Now, on your laptop open a browser window and you can then browse to:

http://127.0.0.1:8888/lab?token=64ddb49f56acc8569f2d237cce504e7edd1ef559e76a23e7

Voila! Now you have a jupyterlab instance running on GPU nodes which you can access from your local machine!

For the remainder of your job run, the IP and port will stay the same. If you close your laptop you will need to recreate an SSH Tunnel - you can reuse the “ssh -L8888” command above. If your job ends, you need to resubmit your slurm job, and then modify your SSH Tunnel command with the new IP address. Jobs last for a maximum of 7 days.

If at any time port 8888 seems to already be in use, you can change the port (any above 1024) in your sbatch file, and in the corresponding commands for your SSH tunnel.

#### 8. Managing slurm jobs

Please don't occupy the GPUs once you are done with your work. This will allow other researchers to share the valuable resources. To cancel your job

```bash
$ scancel <JOBID> # Find job id using squeue command
```

More on how to manage slurm: [stanford-rc.github.io/docs-earth/docs/slurm-basics](https://stanford-rc.github.io/docs-earth/docs/slurm-basics)

#### 9. What you can to with the OpenGPU cluster?

As of 2023 the specs of the OpenGPU cluster is:
* GPU: 4 x NVIDIA Corporation GP102 [TITAN Xp], 12GB RAM
* RAM: 128 GB
* Processor: Intel(R) Xeon(R) Silver 4114 CPU @ 2.20GHz

With these specifications, training small to medium-sized deep neural networks is quite manageable. However, I believe that Google Colab offers greater convenience and more powerful processors, enabling you to accomplish even more.

My initial goal was to utilize the cluster for running large language models. Unfortunately, even the smallest of these models prove challenging to accommodate on this relatively modest cluster.

#### Conclusion

If you found this write-up helpful, please consider leaving a thumbs up or a positive comment below. I trust you've discovered valuable insights in this blog.