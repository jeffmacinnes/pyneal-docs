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

## Pyneal Simulation Tools