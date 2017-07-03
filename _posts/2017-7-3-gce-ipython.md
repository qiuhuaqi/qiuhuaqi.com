---
layout: post
title: Setup Google Cloud Compute instance + iPython notebook
---

This note walks through the cs231n [Goolge Cloud tutorial][cs231n-tutorial] and sets up a Google Cloud Engine (GCE) Virtual Machine instance with iPython notebook (IDE). 

[cs231n-tutorial]:http://cs231n.github.io/gce-tutorial

In addition to the original tutorial, this note adds details on:

- issues with working behind proxy
- SSH connection with with $gcloud commmand line tool
- using Docker on GCE VM


## List of content:
1. [Set up GCE VM instance](#1-set-up-gce-vm-instance)
2. [Connect to VM instance](#2-connect-to-vm-instance)  
    1. [Install gcloud command line tool](#1-install-gcloud-command-line-tool)
    2. [Proxy settings](#2-proxy-settings)
    3. [Connect to VM instance via SSH](#3-connect-to-vm-instance-via-ssh)
3. [Start IPython Notebook and work in browser](#3-start-ipython-notebook-and-work-in-browser)
4. [Work with Docker](#4-work-with-docker)


## 1. Set up GCE VM instance  
GCE are part of the Google Cloud Platform (GCP). It provides Cloud computing power using Google's cloud servers for users at a fair price. It's a great choice for individual developers who have limited local computing resources. Google provides $300 of credit to new users of GCP, which is a great gesture.

**Step 1: Set up GCE VM instance**  
Firstly, you need to set up a GCP account and create a VM instance on GCE. Follow the cs231n [Google Cloud tutorial][cs231n-tutorial] for this part. Note that number of CPU, size of Disk storage and number of GPU etc affect the cost of running the instance. GCE gives a price estimate (*assuming 24hrs/day running*) for your reference when you first create your instance.  

 **Step 2: Start or Stop instance**  
Once your instance is ready to go, run your instance by selecting the instance you want to run and click the **START** button on the top menu in **VM instances** section of the **Compute Engines** dashboard. Stop your instance by clicking the **STOP** button next to the START button.

![instance-start](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/gce-start.png)

**Remember to stop your VM instance when you are done! Running instances cost credits or dollar bills!**
![out-of-credit-dog](http://cs231n.github.io/assets/sadpuppy_nocredits.png)

## 2. Connect to VM instance  
### 1. Install `$gcloud` command line tool  
To connect to your running VM instance on GCE, you can use the `$gcloud` command line in Google Cloud SDK. Download and install the SDK from [here](https://cloud.google.com/sdk/docs) following **step 1 to step 4** on the page.  
   
Then run the following in your shell:  
```
$gcloud init --console-only --skip-diagnostics
```
   
The `--console-only` flag stops the shell from opening a browser (this avoids some shell-browser related issues) and the `--skip-diagnostics` flag skips network diagnostics to save some time. This step creates a configuration of gcloud. It requires you to log in your Google account and authorises your local SDK tool to access and operate your GCE. It also needs you to pick compute region and the **cloud project** by selecting the **project ID** (you can find your project ID on your Cloud console dashboard - **project info**). You can view, change or delete your configurations later ([more details](https://cloud.google.com/sdk/docs/managing-configurations)).  
   
If you are working behind a proxy, you could run into some network-related Errors in this step. Check out the [proxy settings](#2-proxy-settings) and try again.  
   
>If you do have network problems other than proxy issues, run the following command to run a diagnostic:  
>```
>$gcloud info --run-diagnostics
>```
   
Now your SDK is good to go!  
   
### 2. Proxy settings  
>Skip this if you are not working behind a proxy.**  
   
If you are working behind a proxy, you need to set your environment variables realted to proxy. Enable HTTP and HTTPS proxy of your proxy tool before continue.  
     
For Mac OS X, add the following lines in `~/.bash_profile` and `~/.bashrc`:  
```
export http_proxy=http://[proxy_address]:[port];
export https_proxy=https://[proxy_address]:[port];
```
Replace the `[proxy_address]:[port]` with your HTTP and HTTPS proxy **address** and **port**.  
   
For Linux (Ubuntu) users, put this is in `~/.env` (**warning**: this could be wrong as I'm not a Ubuntu user).  

Now resume your `$gcloud init` step [above](#1-install-gcloud-command-line-tool) and you should be OK.  
   
   
### 3. Connect to VM instance via SSH  
Once you get your VM instance running, you can now connect to the instance via SSH tunnel.  

**1. From GCE dashboard**  
In GCE dashboard, you can SSH to your running instance by clicking the **SSH** button in the **VM instances** section.
![web-gce-ssh](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/web-gce-ssh.png)  

Wait for the connection to be established and you can run commands on your VM now in the shell that popped up.  


**2. From local shell**  
As long as your VM instance is running, you can connect to it from your local terminal and store your SSH keypairs on your local machine.  

In your terminal:  
```
$gcloud compute ssh --zone=[YOUR-ZONE] [USERNAME]@[YOUR-INSTANCE-NAME]
```

If you don't have SSH keypair for GCE previously, this command prompts you to generate a new SSH keypair (*you can leave                the keygen passphrase empty*), stores them in `~/.ssh` and transfers them to your GCE **Metadata** . Authentication of your later connections will be automatically done by matching the private key stored locally and the public key on Google Cloud. 

>If you have previous knowledge on SSH and prefer not to use `gcloud` tool to handle the connection, check out [this page](https://cloud.google.com/compute/docs/instances/connecting-to-instance) for more details.

## 3. Start IPython Notebook on instance and work in local browser

## 4. Work with Docker
