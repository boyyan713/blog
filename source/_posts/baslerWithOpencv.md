---
title: Getting started with Basler Camera With Opencv on Python
date: 2020-09-23 14:26:06
tags:
 - Basler
 - Opencv
 - python
categories: Basler
---
# Introduction
This post document is about using Basler Camera with Opencv on Python. At the beginning of this guide I will introduct how to set-up development environment with Pylon and opencv within Conda virual environment. Seconly, I will talk about how to check and set some of basic Basler feature base on pypylon. At the end, I will give a example about using Opencv read Basler Camera data stream.

# Hardware and Software Testing Environment
## Hardware Environment
+ Camera: Basler (a2A1920 - 51gcPRO)
+ Network Adapter: Intel I350 Gigabit Network adapter (POE)
+ CPU: Intel(R) Core(TM) i7-9700F CPU @ 3.00GHz
+ RAM: 16GiB system memory
## Software Environment
+ Ubuntu 18.04 (Linux version 5.4.0-48-generic)
+ Need set-up Network exchange environment, the document link: {% post_link ubuntuRouter %}

# Development Environment Set-up

## Creating conda environment
You can follow the below steps to create the conda environment. If you want to know more details about Conda, please have a look link: {% post_link conda %}

```bash
conda create -n baslerOpencv python=3.7.7
conda activate baslerOpencv
conda install notebook ipykernel
ipython kernel install --user --name baslerOpencv --display-name "Python (Basler with Opencv)"
```
## Installing Pylon
1. Go to [Pylon Official Website](https://www.baslerweb.com/en/products/software/basler-pylon-camera-software-suite/).
2. Go to Downloads Section
3. Click link: pylon 6.1.1 Camera Software Suite Linux x86 (64 Bit) - Debian Installer Package
4. Filling in your personal INFOs and click "Start the Download!"
5. Goto you download directory(Using cd command)
6. You can use the apt command for install deb file
```bash
sudo apt install xxxx.deb
```
When you done, you can see there are three applications be installed, which are Pylon IP Configurator, pylon viewer and Basler Product Documention.

## Installing pypylon binary wheel file to conda environment
[pypylon](https://github.com/basler/pypylon)
## For the Impatient
+ Download a binary wheel from the [releases](https://github.com/Basler/pypylon/releases) page.
https://github.com/basler/pypylon/releases/download/1.6.0/pypylon-1.6.0-cp37-cp37m-linux_x86_64.whl
+ Install the wheel using pip3 install <your downloaded wheel>.whl
+ Look at samples/grab.py in this repository

**TIPS:**
```bash
Traceback (most recent call last):
  File "opencv.py", line 6, in <module>
    from pypylon import pylon
  File "/home/yanboyang713/miniconda3/envs/baslerOpencv/lib/python3.7/site-packages/pypylon/pylon.py", line 40, in <module>
    from . import _pylon
ImportError: libpython3.7m.so.1.0: cannot open shared object file: No such file or directory
```

```bash
export LD_LIBRARY_PATH=/home/yanboyang713/miniconda3/envs/front/lib
echo $LD_LIBRARY_PATH
```

## Set-up pypylon-opencv-viewer(Option)
pip install pypylon-opencv-viewer

## Installing Opencv to conda environment
pip install opencv-python==3.4.2.17
pip install opencv-contrib-python==3.4.2.17 


