---
title: Install Tensorflow 2.1 on Ubuntu 18.04 LTS with GPU support
subtitle: Nvidia Drivers, CUDA 10 and cuDNN
date: 2020-09-15 11:08:05
tags:
 - Tensorflow
 - Machine Learning
 - Nvidia GPU
categories: GPU
---
# Introduction
This post document is about how to build GPU support environment for Tensorflow 2.1. This document will include install Nvidia driver, CUDA Toolkit, cuDNN on Ubuntu 18.04.

# Hardware Environment

# Secure UEFI Boot

An issue that often arises when attempting to install Nvidia drivers on Linux involves a motherboard setting known as Secure UEFI Boot. In order for the driver installation to be successful it is necessary to disable this setting on most motherboards.

The procedure for carrying this out is highly specific to each particular motherboard. Hence it is difficult to provide detailed instructions that apply to a range of system configurations.

In broad terms it will be necessary to enter the BIOS as the machine boots up. This can usually be achieved by pressing the Del or F10 key. Once in the BIOS it is necessary to navigate to the section that determines boot settings. To disable Secure UEFI Boot it sometimes involves backing up and removing certain keys while in other instances it is simply a boolean setting that is easily modified.

If this feature is not disabled then in all likelihood trouble will arise subsequent to the Nvidia driver installation. Issues may occur when attempting to login in to Ubuntu after bootup. The problem is particularly difficult to resolve as it often involves an inability to load the Ubuntu GUI!

![Installing TensorFlow 2.2 on Ubuntu 18.04 with an Nvidia GPU](https://www.quantstart.com/articles/installing-tensorflow-22-on-ubuntu-1804-with-an-nvidia-gpu/)

![Deep Learning GPU Installation on Ubuntu 18.4](https://towardsdatascience.com/deep-learning-gpu-installation-on-ubuntu-18-4-9b12230a1d31)
