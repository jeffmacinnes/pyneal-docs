
![](images/pynealLogo.png)


# Introduction

[Pyneal GitHub repository](https://github.com/jeffmacinnes/pyneal)

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


modular, customizable, fit the needs of diverse research groups...

The software is broken into two separate components: **Pyneal Scanner** and **Pyneal**. When first downloaded, **Pyneal Scanner** is contained in a separate directory within the **Pyneal** directory

* **Pyneal Scanner**: Accesses incoming data, modifies it to match a standardized format, and then sends the data out, one 3D volume at a time, to **Pyneal**

* **Pyneal**: Listens for incoming 3D volumes from **Pyneal Scanner**, runs whatever analyses
you have specified, and hosts the results on a server, which other downstream components (e.g. an experimental task) can make requests to

This design allows the software to easily accommodate the various directory structures and data formats that are found on different scanner models at different institutions around the world. (However, it also means that the steps to install, and run **Pyneal** can vary from environment to environment).


## Definitions Used

### Computers
Throughout the documentation, we'll refer to computers by their *functional* role:

* **Scanner computer**: The computer where reconstructed images from the scanner appear. In the case of GE scanners, for instance, new slice dicom files appear in a directory on the scanner console. Siemens scanners, on the other hand, may export new images to a directory on a shared network drive. The **scanner computer** is simply the computer that has local access to the directory where new images appear

* **Analysis computer**: The computer that will be running **Pyneal**. This is the computer on which users will setup their analysis, launch **Pyneal**, and monitor on-going scans.

Note that in some cases, the *same physical computer* can play both functional roles. For instance, when working in a Siemens environment, new images from the scanner might be exported to a shared directory that is accessible on the **analysis computer**. In this case, the same machine could be playing the role of both the **scanner computer** and the **analysis computer**.

### Additional terms used

* **Series**: A complete scan representing either a single 3D anatomical image, or a 4D functional image.

* **Session**:  A collection of series collected within the same experimental session. A **session** would typically represent all of the scans collected after the subject is placed in the scanner (e.g. Anatomical, functional series1, functional series2, etc...)
