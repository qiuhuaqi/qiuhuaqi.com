---
layout: post
title: Install Python and start programming for beginners
date: 2017-07-13
---

### A simple tutorial: install and get started with Python programming for beginners
(FYI: This is for Python beginners who have very little or no programming experience. For this reason, terminal commands for Linux/Unix users are not provided.)  

You can use this tutorial to **quick-start** Python programming and figure out the detailed stuff later as you learn. I hope that this can save you from spending too much time installing and configuring software for coding, which could be very painful for beginners. Interest is a fine thing that needs nurturing.  

The three steps to start coding in Python:
1. [Install Python](#1-install-python)
2. [Install Anaconda](#2-install-anaconda)
3. [Start coding with IDE](#3-start-coding-with-ide)

### 1. Install Python
- Download Python from [here](https://www.python.org/downloads/). 

- Versions?  
Python currently supports two versions: Python 2 and Python 3. Unfortunately, Python 3 does not support some [syntax](https://en.wikipedia.org/wiki/Syntax_(programming_languages)) and the mechanism used in Python 2.
 
- Which version to use?  
Your decision should be based on **your learning material**. Find out which version that your material is using and download that one.  
Once you mastered one version, using the other version isn't much of a big challenge.

### 2. Install Anaconda

- Download Anaconda from [here](https://www.continuum.io/downloads).  
Choose the correct platform that you are on (Windows/macOS/Linux).  
Don't worry about the Python version. Anaconda works with both versions.  

When you are done, open Anaconda-Navigator (the Anaconda [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)) to have a look.

- Why Anaconda?  
Imagine the Python you just installed is an engine. You can use an engine to build a motorcycle, a boat or a car. But you need all the other parts to do that. In Python world, these parts are the **packages**. Collections of these packages are sometimes referred to as **libraries**. You might want to use different combinations of packages/libraries for different projects. So you can put together an **environment** (commonly: [virtual environment][virtual-env]) of packages/libraries for each of your project. Managing these environments manually is possible but rather time-consuming and troublesome. So for now, let's keep it simple and let the professionals do that for us.  
**Anaconda** is a package & environment management tool that does just that.  

[virtual-env]:https://realpython.com/blog/python/python-virtual-environments-a-primer/


### 3. Start coding with IDE

- What's IDE?  
IDE stands for **Integrated Development Environment**. This is where you can write and run your Python code.  
[More about IDE](https://en.wikipedia.org/wiki/Integrated_development_environment)

- Do I have to use IDE?
NO. Although coding with an IDE makes your life much easier, you do not have to.  
Technically, you can create and edit a Python script file (.py file) with a text editor that you like. You can use Atom, Vim or Nano if you are on Linux or macOS platform. If you are on Windows, you can use Notepad++. Once you are done coding, you can run the code script in a Python kernel that you can start in a shell. I do not recommend this for beginners. But it's a good thing to know about.  
(*Notice: please don't use Microsoft Word for Python coding, nor for coding in any programming language*).  

- Which IDE to use?  
The Python you installed in [Step 1](#1-install-python) comes with a default IDE called **IDEL**. Anaconda offers more powerful IDEs for us such as Jupyter Notebook and Spyder. I recommend **Spyder** for beginners. You can simply launch it in the Anaconda-Navigator Home page. Spyder comes with an interactive kernel for simple testing runs of your code and an editor for writing Python scripts. Don't worry, you should learn about these concepts from your Python learning material.  
  
  
*Once you are comfortable with coding in Python, check out the amazing IDE - [Pycharm](https://www.jetbrains.com/pycharm) powered by Google-favored company JetBrains (the community edition is free and adequate for most purposes).*

I believe now you have all you need to start on Python. Remember this is a quick passage to kick-start coding in Python and is by no means the exclusive way. I hope you can later figure out what role each step plays in this process and generalise.  

But for now, have fun coding!
