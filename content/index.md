
![](images/pynealLogo.png)


# Introduction

[<img src="images/githubLogo.png" style="width:75px">](https://github.com/jeffmacinnes/pyneal)
[**Pyneal GitHub repository**](https://github.com/jeffmacinnes/pyneal)

## What is it?
**Pyneal** is an open source software package to support real-time functional magnetic resonance imaging (fMRI). It is entirely Python-based and depends exclusively on free, open source neuroimaging libraries.

It allows users to:

* access functional MRI data in real-time
* compute on-going analyses throughout a scan
* monitor data quality
* share analysis results with remote devices (e.g. send results to an experimental task presenting neurofeedback to participants)

It currently supports data formats used across 3 major MRI manufacturers: **GE**, **Siemens**, **Philips**.

In addition to allowing users to compute basic, ROI-based analyses during a scan, **Pyneal** also provides a simple framework for designing and writing customized analyses that can be computed across the whole brain volume at each timepoint.


## Design/Structure

The software is broken into two separate components: **Pyneal Scanner** and **Pyneal**. When first downloaded, **Pyneal Scanner** is contained in a separate directory within the **Pyneal** directory

* **Pyneal Scanner**: Accesses incoming data, modifies it to match a standardized format, and then sends the data out, one 3D volume at a time, to **Pyneal**

* **Pyneal**: Listens for incoming 3D volumes from **Pyneal Scanner**, runs whatever analyses
you have specified, and hosts the results on a server, which other downstream components (e.g. an experimental task) can make requests to

This design allows the software to easily accommodate the various directory structures and data formats that are found on different scanner models at different institutions around the world. (However, it also means that the steps to install, and setup **Pyneal** can vary from environment to environment):

* [**Installation guide**](installation.md)
* [**Setup guide**](setup.md)


## Terms/Definitions

Throughout the documentation specific terms are used to describe the different components of the software, the underlying architecture, and the various processes involved. Despite sincere efforts to keep these terms intuitive, they're probably not in all cases. Please check the [**glossary**](/glossary.md) for any unfamiliar terms you come across. (You can also find it under `Reference` in the lefthand menu.