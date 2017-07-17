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
Python currently supports two versions: Python 2 and Python 3. Unfortunately, Python 3 does not support some [syntax](https://en.wikipedia.org/wiki/Syntax_(programming_languages)) and the mechanism used in Python 2. So you do have to choose.  
 
- Which version to use?  
Your decision should be based on **your learning material**. Find out which version that your material is using and download that one.  
Once you mastered one version, using the other version isn't much of a big challenge.

### 2. Install Anaconda
- Why Anaconda?  
Imagine the Python you just installed is an engine. You can use an engine to build a motorcycle, a boat or a car. To do thatm you need to combine the engine with all the other parts. In Python world, these parts are the **packages**. Collections of these packages are sometimes referred to as **libraries**. You might want to use different combinations of packages/libraries for different projects. So you can put together an **environment** of packages/libraries (e.g. [virtual environment][virtual-env]) for each of your project. Managing these environments manually is possible but rather time-consuming and troublesome. So for now, let's keep it simple and let the professionals do that for us.  
**Anaconda** is a package & environment management tool that does just that.  

- How to install?  
Download Anaconda from [here](https://www.continuum.io/downloads).
Choose the correct platform that you are on (Windows/macOS/Linux). Don't worry about the Python version. Anaconda works with both versions. Once you are done, open Anaconda-Navigator (the Anaconda [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)) to have a look.  

Note: Anaconda is **not** really a light-weight solution to package management. There are loads of other management tools, among which many of them can create virtual environments. For example, I'm currently using the light-weight `virutalenv` instead of mini-conda for package and virtual environment management on my sotrage-limited Raspberry Pi.  

[virtual-env]:https://realpython.com/blog/python/python-virtual-environments-a-primer/


### 3. Start coding with IDE

- What's IDE?  
IDE stands for **Integrated Development Environment**. This is where you can write and run your Python code.  
[More about IDE](https://en.wikipedia.org/wiki/Integrated_development_environment)

- Which IDE to use?  
The Python you installed in [Step 1](#1-install-python) comes with a default IDE called **IDEL**. Anaconda offers more powerful IDEs for us such as Jupyter Notebook and Spyder. I recommend **Spyder** for beginners. You can simply launch it in the Anaconda-Navigator Home page. Spyder comes with an interactive kernel for simple testing runs of your code and an editor for writing Python scripts. Don't worry, you should learn about these concepts from your Python learning material.  

- Do I have to use IDE?  
**NO.** Although coding with an IDE makes your life much easier, you do not have to use it.   
You can create and edit a Python script file (.py file) with your choice of text editor and run your script with a Python kernel. You can use Sublime Text, Atom, Vim or Nano if you are on Linux or macOS platform. You can even add plug-in(s) on some of these text editors so you can have cool color-scheme, split-window, pep8 style-checking, interactive kernel and auto-complete. If you are on Windows, you can use Notepad++. I do not recommend this for Python beginners unless you have good experience in system configuration.

*Once you are more comfortable with coding in Python and environment configurations, check out the amazing IDE - [Pycharm](https://www.jetbrains.com/pycharm) powered by Google-favored company JetBrains (the CE - community edition is free and adequate for learning purposes).*

I believe now you have all you need to start on Python. Remember this article is a quick passage to kick-start coding in Python and is by no means the exclusive way. I hope you can later figure out what role each step plays in the process of coding-running of Python. Also, I encourage you to create your own developing configuration workflow and share it with others!  

For now, have fun coding!
