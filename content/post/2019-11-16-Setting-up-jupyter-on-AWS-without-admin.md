---
title: Setting up Jupyter Notebook on an AWS machine without admin access
author: Hao Zhu
date: '2019-11-16'
slug: jupyter-on-non-admin-aws
categories:
  - python
tags:
  - python
  - jupyter
  - aws
---

When you have admin access to an AWS EC2 machine/Google Cloud or you can access the control console through either the web interface or cli, you basically just need to follow the following guides.

For AWS: https://docs.aws.amazon.com/dlami/latest/devguide/setup-jupyter.html

For Google Cloud: https://course.fast.ai/start_gcp.html 

However, I recently came across the case that someone has already very kindly setup the computing environment for me on EC2. However, since it's for a class project and the server is managed by the department, as you can imagine, I have neither the root access nor the access to the cloud console. 

Here is how I get around and setup Jupyter notebook there. 

# Generate ssh keypair between your computer and the server
Running Jupyter remotely needs you to set up an ssh key. Since we can't access the AWS console, you should generate on your computer using `ssh-keygen`.

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"
```

Follow the promote and generate a pair of public and private key under `~/.ssh/`. In this case, let's say we name this pair as 'aws_class', you will get 2 files `aws_class` and `aws_class.pub`. Note that AWS only supports RSA key so you need `-t rsa` there. When you are asked to enter a passphrase, you can hit Enter to skip. 

Then, you should copy content of the pub key `aws_class.pub` and paste it in `~/.ssh/authorized_keys` on the AWS server. Note that this file may not exist so you might need to create that. If it exists, just paste your pub key to this file. The `authorized_keys` file can hold multiple pub keys.

You also need to make sure both of your `~/.ssh/authorized_keys` and `~/.ssh/` folder has proper aceess permision.

```
$ chmod 0600 ~/.ssh/authorized_keys
$ chmod 0700 ~/.ssh
```

Then, let's try to log in from your computer. In most other cases, I usually just login using `ssh` directly. However, for this AWS server, for some reason, for the first time login, you will have to login using `ssh-copy-id` and enter password to login for the last time 

```
$ ssh-copy-id -i your_name@your_aws_server
```

In the future, you can just login with regular `ssh` and you shouldn't need to enter password any more. 

# Setting up conda environment and install jupyter
For this part, it's pretty typical. Just follow the normal way of installing conda. Since I don't have sudo access, I installed anaconda in my home directory. 

For this server specifically, note that since the cuda driver is 8.0, which is not compatible with the latest stable pytorch. I install pytorch 1.0, which is the last version that support cuda 8.0.

Another thing to be noted is that, after I finish the installation, I found that somehow the bash on this server is not refreshed after I log out. It means that when you call `conda`, you may see errors like "conda: command not found" because all the settings conda inserted into your .bashrc file won't be reloaded. One way to fix this is to manually start a bash instance

```
$ exec bash
```

Then you can just create an environment and install the packages you need. 

My final note here is that a jupyter has already been installed on this server but it's for python 2. You need to install jupyter notebook/lab in your environment again. 

# Setup password and SSL certificate for your jupyter
You won't want to type in the token for jupyter session when you connect remotely. Therefore, you are recommended to setup a password for your jupyter. As the same time, it's also a good practice to setup SSL for the server.

You can just follow the official AWS guide on this: https://docs.aws.amazon.com/dlami/latest/devguide/setup-jupyter-config.html

Since this is a self-signed certificate, you can download that to your laptop.

Here are the key commands:

```
$ jupyter notebook password
```

```
$ cd ~
$ mkdir ssl
$ cd ssl
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem
```

# Start the jupyter server

```
jupyter notebook --certfile=~/ssl/mycert.pem --keyfile ~/ssl/mykey.key
```

It's up to you whether to use `nohup` to run it

# Start the connection between your computer and the jupyter server
Again following the [AWS toturial](https://docs.aws.amazon.com/dlami/latest/devguide/setup-jupyter-configure-client-linux.html), we can use the ssh private key we generate in Step 1 to connct to the jupyter server. 

```
$ ssh -i ~/.ssh/aws_class -N -f -L 8888:localhost:8888 your_name@your_aws_server_address
```

You should be able to access jupyter at `localhost:8888`. You will be asked to type in the password you created earlier and you should be all set. 
