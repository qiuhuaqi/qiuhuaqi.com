---
layout: post
title: PyCharm remote interpreter and deployment
date: 2017-08-10
---

### List of contents:  
[Intro](#intro)  
[1. Setup SSH](#1-setup-ssh)  
[2. Remote deployment](#2-remote-deployment)  
[3. Remote interpreter](#3-remote-interpreter)  
[4. Debug](#4-debug)  
[Summary](#summary)  
[Future thoughts: Docker](#future-thoughts-docker)  

---

## Intro
**Idea: Use PyCharm when working on remote server**  
PyCharm is a sweet and powerful IDE that I use for Python developing on my MacBook. However, when it comes to working on code that is on a remote server, my choices are limited to text editors (VIM, Sublime Text etc.) and Jupyter Notebook. I'm not really interested in configuring text editors into powerful IDE-ish tools and the later is really just good for organising scientific experiments and results, not coding. Plus, there's the project file management system and debugger that are just tempting. So, I emparked on finding a way to use PyCharm on servers.

In this blog, I crunched some of the ideas that I found into a workflow.

**What we want to do:**  
- Use PyCharm to develope code on remote server
- Use PyCharm to run and debug those code

(A foresight: keep in mind that the idea we have is not exactly in line with PyCharm's intent. But everything work out fine in the end)

**What we need:**  
- **A laptop**
- **A running remote server and its IP address**: I'm using a Google Cloud Engine server VM instance for this blog.
- **Python**: Python on both local and remote machine
- **PyCharm Professional**: This workflow is not possible for PyCharm CE, for now. If you work in academic, you can apply the Pro version for free using just your academic email address [here](https://www.jetbrains.com/student/).

Ideas in mind, tools in hand, let's get to work.

---

## 1. Setup SSH
Communicating with the remote server typically includes authentication as a sercurity measure. Make sure that both your laptop and the remote server have SSH installed. The remote server, in my case, has a standard Ubuntu 16.04.2 system. Run the following code in remote terminal to install SSH:
```
sudo apt-get install ssh
```
Your remote server is now ready for SSH connection. Do the same on your laptop if you are on Linux. For MacBook users, the SSH tool is most possibly already installed. If not, use package managment tools [Homebrew](https://brew.sh) and [Cask](https://caskroom.github.io) and install SSH and ssh-copy-id:

```
brew install ssh-copy-id
```  
Now, let's deploy SSH keypair so we don't have to authenticate by typing in password everytime. First, check your `~/.ssh` directory on your laptop for existing SSH keypairs. If you can't find any, create new keypairs by:

```
ssh-keygen -t rsa
```

Follow the instructions (you can leave the passphrase empty) and you should have a `id_rsa` (private key) and `id_rsa.pub` (public key) file in your `.ssh` folder. You can display and copy the key in your terminal by:
```
cat id_rsa
cat id_rsa.pub
```
Keep your private key to yourself, and copy the public key to your remote server:
```
ssh-key-copy [remote username]@[remote IP]
```
`[remote IP]` is the IP address of your  You will most likely required to login using password for your first connection. If your server rejects your `ssh-key-copy`, you can always mannualy create a authrosied key file in the `.ssh` directory of your remote server and copy-paste your local public key to it.
  
Now we are "SSH ready".


## 2. Remote deployment
### Instructions
We start with a new empty PyCharm project so we don't mess up an existing project. Fire up the PyCharm Pro and create a new testing project. Head to PyCharm configurations at: **PyCharm > Preferences** (File > Settings for Linux & Windows). Then go to **Build, Execution, Deployment > Deployment**. Click on the `+` to create a new deployment setting. 

![add server](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/pycharm-remote/start-deploy.png)

Name your remote server and choose **SFTP** for **Type**, as shown in the snapshot. This means we will be using the SFTP protocol for file transfer. Do make sure your server supports this protocol. Click `OK`. Next, we need to configure the connection to the server.   

In the **Connection** tab:
- \[Type\]: SFTP
- \[SFTP host\]: the IP address of your remote server
- \[Port\]: 22 (default)
- \[Root path\]: the root path for configuration, typically your user home directory. All path set later will be relative to this path. (you can use `Autodetect` once you have the authentication settings below)

- \[User name\]: your username on the remote server
- \[Auth type\]: Key pair (OpenSSH or PuTTY)
- \[Private key file\]: path to your **private** key

![connection setting](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/pycharm-remote/connect-settings.png)

Click `Test SFTP connection` to make sure your connection is successful. If so, go to **Mappings** tab. 
- \[Local Path\]: path of your local project
- \[Deployment path on server\]: path to which you deploy your project. Your local project will be uploading file to this path on the server and downloading files from this path to your local path.  

![mappings setting](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/pycharm-remote/mappings.png)

We are all done here. Click `OK`.  

You can check files on your remote host(server). Go to the menu bar **Tool > Deployment > Browse Remote Host** to open the remote host file window. You should have something looking like the snapshot below:  

![remote host](https://raw.githubusercontent.com/HarveyQ/HarveyQ.github.io/master/images/pycharm-remote/deployed.png)


### Some explainations
The key to this is the PyCharm **Remote Deployment**. PyCharm designed this for the "local development - remote deployment" situation. For our purpose, we can build the development workflow as: **"download - local development - upload"** which is effectively coding on the remote server. To understand why we have to go throught the "download - upload" maneuver, check out the following two quotes from PyCharm documentation:

> "PyCharm assumes that all development, debugging, and testing is done on your computer and then the code is deployed to a production environment."

> "To provide efficient coding assistance, PyCharm needs to re-index code fast, which requires fast access to project files. The latter can be ensured only for local files, that is, files that are stored on you hard disk and are accessible through the file system. Therefore PyCharm does not support the mode when you access your files over a network folder (very often it becomes slow and unresponsive, performs random look-ups for no obvious reason, etc)."

In a word, the PyCharm "charm" requires working on local Python code. Direct coding on remote host is possible (you can try to edit .py file in remote host browsing) but it doens't make much sense.  


## 3. Remote interpreter



## 4. Debug


## Summary
In summary, we 

## Future thoughts: Docker
Virtual Machines still rely partially on OS level. You and I both know that messing with OS configurations is not fun. Solution: **Docker**. Docker daemon takes care of the talking to OS part, leaving us comfortablely messing with the **Containers**. It is possible to run interpreters in Docker containers and more excitingly, connect it to PyCharm. Next time on developing environment topic, I want to figure out the connection to Docker and take this to the next level.


Main references:
- Blog by Erik Hallström [link here](https://medium.com/@erikhallstrm/work-remotely-with-pycharm-tensorflow-and-ssh-c60564be862d)
- Official documentations from JetBrain [link here](https://www.jetbrains.com/help/pycharm/deploying-your-code.html)
