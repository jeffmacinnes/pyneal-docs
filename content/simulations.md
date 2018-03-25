# Simulations

## Overview

In order to help with the initial setup, as well as test any analysis scripts and network communications later on, **Pyneal** includes a suite of simulation tools that mimic various inputs and outputs along the data flow path.

These tools allow you to simulate **Pyneal** (or **Pyneal Scanner**) in a modular fashion without having to run the entire pipeline. If you are troubleshooting issues, these tools are immensely helpful.  

Here is a diagram highlighting the various simulation tools, and where they enter the data flow pipeline. 

![](images/simulationSchematic.png)

During an actual real-time scan, data will flow through this diagram from left to right along the blue arrows. 

Simulation tools are indicated using dashed or dotted vertical lines.

* A dashed line indicates a simulation tool that **generates input**. In other words, these tools mimic real data as it exists at a particular stage of the pipeline

* A dotted line indicates a simulation tool that **receives output**. In other words, these tools allow you to simulate the *next* stage of the pipeline

Both **Pyneal Scanner** and **Pyneal** have their own set of simulation tools. 

* **Pyneal Scanner** simulation tools can be found in `pyneal/pyneal_scanner/simulation` and are shown in light blue *below* the real data pipeline in the schematic. See below for more details

* **Pyneal** simulation tools can be found in `pyneal/utils/simulation` and are shown in green *above* the real data pipeline in the schematic. See below for more details

## Pyneal Scanner Simulation Tools

The **Pyneal Scanner** simulation tools can be found in `pyneal/pyneal_scanner/simulation`

* **Scanner Simulators**: Set of simulation scripts to mimic the behavior of real scanners with real data. 
* **pynealReceiver_sim.py**: simulates the behavior of **Pyneal** (i.e. accepts incoming 3D volumes from **Pyneal Scanner**)

### Scanner Simulators
**Use Case:** Testing **Pyneal Scanner** (and *anything else* downstream) with real data.

This will simulate the appearance of raw data coming off of the scanner. This works by pointing the simulator to a folder containing real scanner data. The simulator will copy the real data to a new directory in a way that mimics the behavior of a real scan, allowing you to test **Pyneal Scanner** and anything else downstream. 

The format of the raw data will vary according to different scanner environments/manufacturs. Accordingly, there are multiple scripts that will simulate different types of data:

#### GE

usage: `python GE_sim.py inputDir [-o outputDir -t/--TR TR]`

input args:  
 
* inputDir: path to directory containing raw slice dicoms
* -o outputDir: path to directory where slices will be copied to [default: <inputDir>/s9999]
* -t/--TR TR: set the TR in ms [default: 1000]
 
In order to run this script, you must have a local directory that contains raw slice dicom files from an actual scan. 

This script will copy all of the slices from the inputDir and copy them to the outputDir at a rate that is set by the TR. 

After the script has completed, the temporary outputDir will be deleted

#### Philips

usage: 

input args:

#### Siements

usage: 

input args:


### pynealReceiver_sim.py
**Use Case:** When you want to test **Pyneal Scanner** without having to actually run **Pyneal**

This simulator will mimic the part of **Pyneal** that accepts incoming 3D volumes from **Pyneal Scanner**. This allows you to quickly test sending output with **Pyneal Scanner**, without having to fully run **Pyneal** (which entails a lot of extra overhead). 

usage: `python pynealReceiver_sim.py`

This simulator is hardcoded to be listening for incoming data on port `5556`. Make sure **Pyneal Scanner** is configured to use that same port number for `pynealSocketPort` (see [**Pyneal Scanner Setup**](/setup.md#pyneal-scanner))
 


## Pyneal Simulation Tools