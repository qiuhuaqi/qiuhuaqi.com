---
layout: post
title: Setup Google Cloud Compute instance + Jupyter Notebook
date: 2017-08-07
---

This note walks through the cs231n [Goolge Cloud tutorial][cs231n-tutorial], sets up a Google Cloud Engine (GCE) Virtual Machine instance and sets up Jupyter Notebook for developing.  

[cs231n-tutorial]:http://cs231n.github.io/gce-tutorial

In addition to the original tutorial, this note adds details on:

- issues with working behind proxy
- SSH connection with with $gcloud commmand line tool


## List of content:
1. [Set up GCE VM instance](#1-set-up-gce-vm-instance)
2. [Connect to VM instance](#2-connect-to-vm-instance)  
    1. [Install gcloud command line tool](#1-install-`$gcloud`-command-line-tool)
    2. [Proxy settings](#2-proxy-settings)
    3. [Connect to VM instance via SSH](#3-connect-to-vm-instance-via-ssh)
3. [Start IPython Notebook and work in browser](#3-start-ipython-notebook-and-work-in-browser)  

[Summary](#summary)


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
>Skip this if you are not working behind a proxy.  
   
If you are working behind a proxy, you need to set your environment variables related to proxy. Enable HTTP and HTTPS proxy of your proxy tool before you continue.  
     
For Mac OS X, add the following lines in `~/.bash_profile` and `~/.bashrc`:  
```
export http_proxy=http://[proxy_address]:[port];
export https_proxy=https://[proxy_address]:[port];
```
Replace the `[proxy_address]:[port]` with your HTTP and HTTPS proxy **address** and **port**.  
   
For Linux (Ubuntu) users, put this is in `~/.env` (**warning**: this could be wrong as I'm not a Ubuntu user).  

Now resume your `$gcloud init` step [above](#1-install-gcloud-command-line-tool) and you should be OK.  
   
   
### 3. Connect to VM instance via SSH  
Once you get your VM instance running, you can now connect to the instance via SSH tunnel. You need to **START** your instance before you try to connect. 

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

## 3. Start Jupyter Notebook on instance and work in local browser
Now we have a running VM instance on GCE. The next thing to do is to write codes and run computations on the VM. Of course, you can use your favoriate Linux based light-weight text editors (vim, nano etc.) to edit code/script and run them by kernel using command line. But, it would be nice if we can have a IDE to do that. IPython notebook is such a great tool that we can use. 

**Step 1: Check Jupyter Notebook and IPython installation**  
Check package list in your working environment or more commonly, virtual environment. If you are planning to use a virtual environment, activate your virtualenv first and then check packages using `pip list` or `conda list` (if you are using conda to manage your virutalenv as me). Look for `ipython` and `jupyter` related packages. Update the packages by
```
pip install [package-name] --update
```
In my case, I found some very useful features (e.g. the Markdown and some key mappings) were not included in my initial `apt-get` installation of Jupyter Notebook. So I updated to the newer version in `pip`.

**Step 2: Set external IP address, expose TCP port**  
In order to access Jupyter Notebook run on the Cloud VM from a local browser, we need to assign an external IP address for the VM. Google allows us to attach one static IP address to our VM instances ***free of charge***. We also need to add a firewall rule to expose a TCP port to which we will direct our connection from the browser. Detailed instructions can be found in the cs231n [Google Cloud tutorial][cs231n-tutorial]. Once you are done, take not of your VM's external IP address. 

**Step 3: Create jupyter configuration**  
We now need to do a bit configurations for the notebook. On your running VM instance, find the Jupyter Notebook configuration file (this file is typically under the directory: /home/your_user_name/.jupyter)
```ls ~/.jupyter/jupyter_notebook_config.py```  

If the config file doesn't exit, create one by:  
```jupyter notebook --generate-config```
(you need to activate your virtual environment to use `jupyter notebook`)

Add the following configurations to the config file:

```
c = get_config()

c.NotebookApp.ip = '*'

c.NotebookApp.port = <PORT-NUMBER>

c.NotebookApp.open_browser = False
```

The \<PORT-NUMBER\> should match the one you set in the VM firewall rule. I assigned port 7000 for my notebook. The configurations we added mean that the notebook will be listening to all IP addresses on port \<PORT-NUMBER\> and will not open a browser upon starting up.  

**Step 4: Launching the notebook and connecting to it**
Start the Jupyter Notebook by running the following in the VM under your desired working directory:
```
juypter notebook
```
(you can ignored the `--no-browser` flag that is suggested by cs231n tutorial. It's already set in the configuration)  

You should see a few messages from NotebookApp telling you that your notebook server is now up and running. In particular, you should look for the line that gives you the URL for accessing the notebook. Mine looks like:
```
[I 03:46:12.932 NotebookApp] The IPython Notebook is running at: http://[all ip addresses on your system]:7000/
```

Next, open up your favorite browser and access the URL with the \[all ip addresses on your system\] part replaced by the static external IP address that you set earlier. If it all goes well, you should then see the Jupyter Notebook interface. We're all set!

### Summary  
In summary, the topics that we covered in this blog are:
- setting up a Google Cloud Compute VM and running VM instances
- connecting to the running VM instance via SSH
- setting up Jupyter Notebook for developing and accessing the notebook server from a local browser  

I hope this helps.  

And of course, don't forget to ***STOP YOUR INSTANCE***.  
