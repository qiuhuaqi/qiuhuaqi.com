---
layout: post
title: PyCharm remote interpreter and deployment
date: 2017-07-13
---

### Idea: Use PyCharm when working on remote server
PyCharm is a sweet and powerful IDE that I use for Python developing on my MacBook. However, when it comes to working on code that is on a remote server, my choices are limited to text editors (VIM, Sublime Text etc.) and Jupyter Notebook. I'm not really interested in configuring text editors into powerful IDE-ish tools and the later is really just good for organising scientific experiments and results, not coding. Plus, there's the project file management system and debugger that are just tempting. So, I emparked on finding a way to use PyCharm on servers.

In this blog, I crunched some of the ideas that I found into a workflow.

---
### What we want to do:
- Use PyCharm to develope code on remote server
- Use PyCharm to run and debug those code

(A foresight: keep in mind that the idea we have is not exactly in line with PyCharm's intent. But everything work out fine in the end)

### What we need:
- **A laptop**
- **A running remote server and its IP address**: I'm using a Google Cloud Engine server VM instance for this blog.
- **Python**: Python on both local and remote machine
- **PyCharm Professional**: This workflow is not possible for PyCharm CE, for now. If you work in academic, you can apply the Pro version for free using just your academic email address [here](https://www.jetbrains.com/student/).


### How we do it:
**1. Setup SSH**  
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


**2. PyCharm remote deployment**  
The key to this is the PyCharm **remote deployment**. PyCharm designed this for the "local development - remote deployment" situation, which is exactly right for us. 

We start with a new empty PyCharm project so we don't mess up an existing project. Fire up the PyCharm Pro and create a new testing project. 


Two very important QUOTES:

"PyCharm assumes that all development, debugging, and testing is done on your computer and then the code is deployed to a production environment."

"To provide efficient coding assistance, PyCharm needs to re-index code fast, which requires fast access to project files. The latter can be ensured only for local files, that is, files that are stored on you hard disk and are accessible through the file system. Therefore PyCharm does not support the mode when you access your files over a network folder (very often it becomes slow and unresponsive, performs random look-ups for no obvious reason, etc)."

Therefore we have to say this syncronisation system is not good for distributed development.


**3. PyCharm remote interpreter**  

**4. Debug**  


### Summary  
In summary, we 

### Future thoughts: Docker
Virtual Machines still rely partially on OS level. You and I both know that messing with OS configurations is not fun. Solution: **Docker**. Docker daemon takes care of the talking to OS part, leaving us comfortablely messing with the **Containers**. It is possible to run interpreters in Docker containers and more excitingly, connect it to PyCharm. Next time on developing environment topic, I want to figure out the connection to Docker and take this to the next level.


Main references:
- Blog by Erik Hallström [link here](https://medium.com/@erikhallstrm/work-remotely-with-pycharm-tensorflow-and-ssh-c60564be862d)
- Official documentations from JetBrain [link here](https://www.jetbrains.com/help/pycharm/deploying-your-code.html)
