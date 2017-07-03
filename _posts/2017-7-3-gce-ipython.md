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
2. [Connect to the VM instance](#2-connect-to-the-vm-instance)  
    1. [Install gcloud command line tool](#1-install-gcloud-command-line-tool)
    2. [Proxy settings](#2-proxy-settings)
    3. [Initialise gcloud](#3-initialise-gcloud)
    4. [Connect to instance via SSH](#4-connect-to-instance-via-ssh)
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

## 2. Connect to the VM instance  
   ### 1. Install gcloud command line tool
   ### 2. Proxy settings
   ### 3. Initialise gcloud
   ### 4. Connect to instance via SSH

## 3. Start IPython Notebook and work in browser

## 4. Work with Docker
