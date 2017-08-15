---
layout: post
title: PyCharm remote interpreter and deployment
date: 2017-07-13
---

### Idea: Use PyCharm when working on remote server
PyCharm is a sweet and powerful IDE that I use for Python developing on my MacBook. However, when it comes to working on code that is on a remote server, my choices are limited to text editors (VIM, Sublime Text etc.) and Jupyter Notebook. I'm not really interested in configuring text editors into powerful IDE tools and the later is really just good for organising scientific experiments and results, not coding. Plus, there's the project file management system and debugger that are just tempting. So, I emparked on finding a way to use PyCharm on servers.

In this blog, I crunched some of the ideas that I found into a workflow for this idea.

---
### What we want to do:
- Use PyCharm for code that resides on a remote server
- Use PyCharm to run and debug those code


### What we need:
- **A laptop**
- **A running remote server**: I'm using a Google Cloud Engine server VM instance for this blog.
- **Python**: Python on both local and remote machine
- **PyCharm Professional**: This workflow is not possible for PyCharm CE, for now. If you work in academic, you can apply the Pro version for free using just your academic email address [here](https://www.jetbrains.com/student/).


### How we do it:
1. Setup SSH  
Communicating with the remote server typically includes authentication as a sercurity measure. Make sure that both your laptop and the remote server have SSH installed. The remote server, in my case, has a standard Ubuntu 16.04.2 system. Run the following code in remote terminal to install SSH:
```
sudo apt-get install ssh
```
Your remote server is now ready for SSH connection. Do the same on your laptop if you are on Linux. For MacBook users, the SSH tool is mostly 

2. 
