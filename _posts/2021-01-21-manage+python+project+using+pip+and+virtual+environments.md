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
modified_time: '2021-01-21T08:40:42.898-08:00'
---


# Setup minimal Python3 project with virtual environments

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
``` bash
apt-get install python3-tk
python3 -m pip install matplotlib
python3 -m pip install numpy
```

## Automate the installation:
``` bash
pip list 
pip freeze > requirements.txt
```
Use the requirements list.
``` bash
python3 -m pip install -r requirements.txt
Jupyter Notebooks requires ipykernel
```