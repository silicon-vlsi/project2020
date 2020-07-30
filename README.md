# Table of Contents 
- [Overview](#Overview)
    - [Cloning the Repo](#Cloning-the-Repository)
    - [Suggested Directory Structure](#Suggested-Directory-Structure)
- [NGSpice](#NGSpice)
- [OpenRAM](#OpenRAM)
- [Tasks](#Tasks)

# Overview

This is the repository for the VLSI Project 2020. This repo contains the eda tools, Labs, assignments, docs, etc. related to the project.

## Cloning the Repository
```bash
git clone https://www.github.com/silicon-vlsi/project2020
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

# NGSpice
[NGSpice] is a open source spice simulator for electric and electronic circuits. 
- [NGSpice Reference Manual][NGSpiceMan]: Comple reference manual in HTML format.

After cloning this repo, a precompiled version (compiled in 64-bit LXLE/Ubuntu) will be available in `<PATH-TO-REPO>/project2020/eda/ngspice-32`. Add the following environment variables in your `~/.bashrc`
```bash
export  SPICE_LIB_DIR=$HOME/projects/project2020/eda/ngspice-32/glnxa64/share/ngspice
export  SPICE_EXEC_DIR=$HOME/projects/project2020/eda/ngspice-32/glnxa64/bin
export  PATH=$PATH:$SPICE_EXEC_DIR
```
There is a initialization script in `$SPICE_LIB_DIR/scripts/spinit`. You can overwrite any of the initilization by adding commands to a local `~/.spiceinit` .
The directory stucture:
```bash
project2020/eda/ngspice-32
├── doc
│   └── ngspice-32-manual.pdf  (Complete Reference)
├── examples                   (Lots of Spice examples)
├── glnxa64
│   ├── bin
│   ├── include
│   └── share
│       ├── man
│       └── ngspice
│           └── scripts        (Scripts, including startup spinit)
└── models                     (Spice models)
```

### Quick Start Guide
You can open a text editor create a *netlist* of the intended circuit for example of a voltage divider as shown below (say filename `divider.sp`):
```spice
First line in ngspice is always the title line
* This is a comment line
Vbat    vin     0       DC 5
R1      vin     vout    1k
R2      vout    0       1k

.control
tran 0.1u 1u
.endc

.end
```
Then start `ngspice` and source the netlist at the ngspice command prompt:
```bash
ngspice 1 -> source divider.sp
```
It should output the node voltages at the initial transient voltages. you can plot any of the nodes eg.:
```bash
ngspice 2 -> plot v(vout)
```
If you want to edit the file without leaving ngspice, simply type edit eg.
```bash
ngspice 3 -> edit
```
And to quit simply type `quit`.

# Technology
## MOSIS Scalable CMOS ([SCMOS])
[SCMOS] is a *lambda-based* scalable design rules that can be interfaced to many CMOS fabrication process available at MOSIS. **NOTE** The scalable design rules does not interface with Fabs now because of lot unique process nuances.

- The Spice model files are located at `<PATH-TO-REPO>/project2020/eda/ngspice-32/models/scn4m_subm`
- Typical MOS parameters:
  - **NMOS**: tox=7.6nm, nch=1.7e17/cm^3, Vt0=0.49V, un(mobility)=445 cm^2/Vs
  - **PMOS**: tox=7.6nm, nch=1.7e17/cm^3, Vt0=-0.66V, up(mobility)=151 cm^2/Vs

# OpenRAM
[OpenRAM] is an award winning open-source Python framework to create the layout, netlists, timing and power models, placement and routing models, and other views necessary to use SRAMs in ASIC design.

- Find the project on [GitHub][OpenRAMgit] with documentation to get started
- Read the [ICCAD Paper][openRAMpaper]
- For this project we will use the [SCMOS] technology, a scalable 0.5u CMOS technology.

# Tasks
- [x] Install LXLE on Virtual Box
- [x] Compile ngspice-32 on LXLE and add to the repo.
- [x] Add the [SCMOS] spice models to the ngspice directory.
- [ ] Add a NGSpice section with a quickstart guide to this README
- [ ] Create a customized `Sue` schematic editor and add to repo.
- [ ] Compile [Magic] in LXLE and add to the repo.

* * *

[OpenRAM]:              https://openram.soe.ucsc.edu/
[OpenRAMgit]:           https://github.com/VLSIDA/OpenRAM 
[OpenRAMpaper]:         https://ieeexplore.ieee.org/document/7827670/
[SCMOS]:                https://www.mosis.com/files/scmos/scmos.pdf
[NGSpice]:              http://ngspice.sourceforge.net
[NGSpiceMan]:           http://ngspice.sourceforge.net/docs/ngspice-html-manual/manual.xhtml
[Magic]:                http://opencircuitdesign.com/magic/
