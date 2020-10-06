# Table of Contents 
- [Overview](#Overview)
    - [Cloning the Repo](#Cloning-the-Repository)
    - [Suggested Directory Structure](#Suggested-Directory-Structure)
- [NGSpice](#NGSpice)
    - [QuickStart Guide](#Quick-Start-Guide)
- [CppSimLite](#CppSimLite)
    - [Sue2](#Sue2)
- [Magic](#Magic)
- [Netgen](#Netgen)
- [Technology](#Technology)
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
**IMPORANT NOTE** While editing inside ngspice, if you make an error, you may lose the netlist file. This maybe a bug in ngspice.

The preferred method of running ngspice is in batch mode:
```bash
ngspice -b -r filename.raw -o filename.log input.sp
```

And to quit, simply type `quit`.

# CppSimLite
**CppSimLite** is stripped down version of **CppSim**, (http://cppsim.com) developed by Mike Perrott for mixed-signal system and circuit modeling. Although CppSim is a suite of tools for doing mixed-signal simulation, CppSimLite is only for using the schematic editor **Sue2** and it's accompanying toolboxes for Python and HSPC.

- **Directory Structure**
```bash
CppSimLite
├── CHANGES.md				;Changes made to CppSim
├── cppsim_bashrc_file_example		;example .bashrc 
├── CppSimShared
│   ├── bin
│   ├── Doc				;All documents kept here
│   ├── HspiceToolbox
│   ├── MatlabCode
│   ├── Python				;Python lib
│   ├── Sue2				;Sue2 scripts
│   └── SueLib				;All Sue2 Private Libs
├── Import_Export
├── Netlist				;Sue2 netlists resides here
├── SimRuns				;Sue2 NGSpice runs resides
├── SpiceModels				;**NOTE**NGspice models in ngspice
├── Sue2
├── SueLib				;Public Libraries
│   └── myLib
└── Todo-Bugs.md			;Keeping tracks of Bugs and Todos
```

- Setting the Environment Variables in `~/.bashrc`

```bash
export CPPSIMHOME=$HOME/project2020/eda/CppSimLite
export CPPSIMSHAREDHOME=$CPPSIMHOME/CppSimShared
export EDITOR=/usr/bin/vim
export PATH=$PATH:$CPPSIMSHAREDHOME/bin
```
## Sue2
- Once the environment variables are set, Sue2 can be started by typing
```bash
sue2
```
- The schematic editor will launch with an empty canvas and 3 library panels on the right.
- The first panel on the top is for `schematic` only and the bottom two for symbols or icons to use in the schematic.
- You can choose what library to appear in each panel by clicking the the menu bar in the panel. The menu will show a list of the available Libraries stored in `$CPPSIMSHAREDHOME/SueLib`(Private Libs) and `$CPPSIMHOME/SueLib`(Piblic Libs) and the list and the order is loaded from `$CPPSIMHOME/Sue2/sue.lib`
- To select a schematic, use the cursor to select the schematic (eg. *invX1*) and then click **Shift-LeftMouseButton**. **NOTE** There is bug in *sue2* in Linux-LXLE distro where LeftMouseButton doesn't work. If you are working in any other Linux (eg. ubuntu) just LeftMouseButton works.
- You can create a netlist by clicking *Tools -> Create a netlist (with top sub)* and give a directory to save (default: *$CPPSIMHOME/Netlist*) **NOTE** While saving for the option *File Type* choose *All ()* Another bug which creates two .sp extensions otherwise.
- Now you can can write a Spice testbench and include and instatiate the above created netlist. There is alrady a example testbench in *$CPPSIMHOME/SimRuns/myLib/invX1/TB_invX1.sp*

# Magic
[Magic] is the most popular open-source Layout tool written in the 1980's at Berkeley by John Ousterhout (now famous for writing scripting languuage Tcl) and now maintained by Tim Edwards (opencircuitdesign.com/magic).
**Setting Up the Environment Variables**
```bash
export MAGIC_HOME=/home/vlsi/tools/magic-83
export PATH=$PATH:$MAGIC_HOME/bin
```

# Netgen
[Netgen] is a tool for comparing netlists, a process known as LVS, which stands for "Layout vs. Schematic". This is an important step in the integrated circuit design flow, ensuring that the geometry that has been laid out matches the expected circuit.
Netgen is currently maintained by Tim Edwards (opencircuitdesign.com/netgen)

# Technology
## MOSIS Scalable CMOS ([SCMOS])
[SCMOS] is a *lambda-based* scalable design rules that can be interfaced to many CMOS fabrication process available at MOSIS. **NOTE** The scalable design rules does not interface with Fabs now because of lot unique process nuances.

- The Spice model files are located at `<PATH-TO-REPO>/project2020/eda/ngspice-32/models/scn4m_subm`
- Typical MOS parameters:
  - **NMOS**: tox=7.6nm, nch=1.7e17/cm^3, Vt0=0.49V, un(mobility)=445 cm^2/Vs
  - **PMOS**: tox=7.6nm, nch=1.7e17/cm^3, Vt0=-0.66V, up(mobility)=151 cm^2/Vs
  - Vdd=5V, Lmin=0.4um, Wmin=0.6um

# OpenRAM
[OpenRAM] is an award winning open-source Python framework to create the layout, netlists, timing and power models, placement and routing models, and other views necessary to use SRAMs in ASIC design.

- Find the project on [GitHub][OpenRAMgit] with documentation to get started
- Read the [ICCAD Paper][openRAMpaper]
- For this project we will use the [SCMOS] technology, a scalable 0.5u CMOS technology.

# Tasks
- [x] Install LXLE on Virtual Box
- [x] Compile ngspice-32 on LXLE and add to the repo.
- [x] Add the [SCMOS] spice models to the ngspice directory.
- [x] Add a NGSpice section with a quickstart guide to this README
- [x] Create a customized `Sue` schematic editor and add to repo.
- [x] Compile [Magic] in LXLE and add to the repo.
- [ ] File a bug report with ngspice regarding the file deleting when in edit mode.

* * *

[OpenRAM]:              https://openram.soe.ucsc.edu/
[OpenRAMgit]:           https://github.com/VLSIDA/OpenRAM 
[OpenRAMpaper]:         https://ieeexplore.ieee.org/document/7827670/
[SCMOS]:                https://www.mosis.com/files/scmos/scmos.pdf
[NGSpice]:              http://ngspice.sourceforge.net
[NGSpiceMan]:           http://ngspice.sourceforge.net/docs/ngspice-html-manual/manual.xhtml
[Magic]:                http://opencircuitdesign.com/magic/
[Netgen]:               http://opencircuitdesign.com/netgen/
