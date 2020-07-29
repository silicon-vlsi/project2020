# Table of Contents 
- [Overview](#Overview)
- [Install/Setup](#Installation-Setup)
    - [Cloning the Repo](#Cloning-the-Repository)
    - [Setting the Environment Variables](#Setting-the-Environment-Variables)
    - [Suggested Directory Structure](#Suggested-Directory-Structure)
- [OpenRAM](#OpenRAM)

# Overview

This is the repository for the VLSI Project 2020. This repo contains the eda tools, Labs, assignments, docs, etc. related to the project.

# Installation Setup

## Cloning the Repository
```bash
git clone https://www.github.com/silicon-vlsi/project2020
```

## Setting the Environment Variables
Add the following in ```~/.bashrc```
```bash
export PATH=$PATH:<PATH-TO-REPO>/project2020/eda/ngspice-32/glnxa64/bin
```

## Suggested Directory Structure
```bash
<HOME_DIR> [eg. /home/vlsi]
   ├── project2020	[Git repo, DO NOT  work in this Dir]
   ├── Desktop
   |    ├── myLab	[Your work dir	]
   ├─ OpenRAM		[Git repo for OpenRAM, DO NOT work in this dir]
   ├─ OpenSTA		[Git repo for OpenSTA, DO NOT work in this dir]
```
# OpenRAM
[OpenRAM] is an award winning open-source Python framework to create the layout, netlists, timing and power models, placement and routing models, and other views necessary to use SRAMs in ASIC design. 
- Find the project on [GitHub][OpenRAMgit] with documentation to get started
- Read the [ICCAD Paper][openRAMpaper]


* * *

[OpenRAM]:              https://openram.soe.ucsc.edu/
[OpenRAMgit]:           https://github.com/VLSIDA/OpenRAM 
[OpenRAMpaper]:         https://ieeexplore.ieee.org/document/7827670/
