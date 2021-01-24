---
layout: post
title: Manage Python project using PIP and virtual environments
date: '2021-01-21T08:40:00.000-08:00'
author: MaX
tags: 
- Python
- VirtualEnv
- Project
- Development
modified_time: '2021-01-24T18:00:42.898-08:00'
---


# Setup minimal Python3 Project with virtual environments
The virtual environment is a simple yet effective way to configure and maintain the set of libraries you need for your project.
It is very minimal, but the file requirements.txt, it can be compared to a minimalist version of package managers configurations like pom.xml for Java or package.jason for NodeJS. 
In this short post I will pull together few steps to create an environment form scratch, save the libs configurion and reload them.


## Create and activate the virtual env inside your project folder.
### Linux:
``` bash
sudo apt-get install python3-venv
python3 -m venv .venv
source .venv/bin/activate
```
### Windows:
``` cmd
py -m venv .venv
.venv\Scripts\activate.bat
```
## Install the libraries (for Windows use py instead of python3):
Let's now install two widely used libraries: mathplotlib and numpy 
``` bash
apt-get install python3-tk
python3 -m pip install matplotlib
python3 -m pip install numpy
```

## Automate the installation:
Save the libraries into **requirements.txt**
``` bash
pip list 
pip freeze > requirements.txt
```
Use the requirements list when you are reinstalling the project from scratch (i.e. after the checkout from a repository).

``` bash
python3 -m pip install -r requirements.txt
Jupyter Notebooks requires ipykernel
```

## References:
If you want to learn more you can llok at this interesting articles:
- [Setup Local Python3 Dev Environment in Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server)
- [Pyton3 Venv DOC](https://docs.python.org/3/library/venv.html)
- [Python Virtual Environments](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/26/python-virtual-env/)