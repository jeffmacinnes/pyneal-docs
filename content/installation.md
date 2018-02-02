#

Pyneal is built and tested using `Python 3.6`. Download from [https://www.python.org/downloads/](https://www.python.org/downloads/) or via a distribution like [Anaconda](https://www.anaconda.com/download)

Pyneal requires additional libraries beyond the standard library. Instructions below use `pip` to install these libraries. Verify that you have `pip` installed:

>which pip

If not, download and install pip from [https://pip.pypa.io/en/stable/installing/](https://pip.pypa.io/en/stable/installing/)

## Overview

The software tool is broken into two separate components: **Pyneal Scanner** and **Pyneal**. When first downloaded, **Pyneal Scanner** is contained in a separate directory within the **Pyneal** directory

* **Pyneal Scanner**: Accesses incoming data, modifies it to match a standardized format, and then sends the data out, one 3D volume at a time, to **Pyneal**

* **Pyneal**: Listens for incoming 3D volumes from **Pyneal Scanner**, runs whatever analyses
you have specified, and hosts the results on a server, which other downstream components (e.g. an experimental task) can make requests to

This design allows the software to easily accommodate the various directory structures and  data formats that are found on different scanner models at different institutions around the world.

However, this feature also means that the specific installation instructions can vary by computing environments.


### Definitions Used

For the purposes of these instructions, we'll refer to computers by their *functional* role:

* **Scanner computer**: The computer where reconstructed images from the scanner appear. In the case of GE scanners, for instance, new slice dicom files appear in a directory on the scanner console. Siemens scanners, on the other hand, may export new images to a directory on a shared network drive. The **scanner computer** is simply the computer that has local access to the directory where new images appear

* **Analysis computer**: The computer that will be running **Pyneal**. This is the computer on which users will setup their analysis, launch **Pyneal**, and monitor on-going scans.

Note that in some cases, the *same physical computer* can play both functional roles. For instance, when working in a Siemens environment, new images from the scanner might be exported to a shared directory that is accessible on the **analysis computer**. In this case, the same machine could be playing the role of both the **scanner computer** and the **analysis computer**.


## Download Pyneal

Download the [Pyneal repository](https://github.com/jeffmacinnes/pyneal) from GitHub, or clone to your local machine:


>git clone https://github.com/jeffmacinnes/pyneal.git


## Pyneal-Scanner

The `pyneal_scanner` directory needs to be on the **scanner computer**. If the **scanner computer** is different from the **analysis computer** in your environment, copy the `pyneal_scanner` directory to the **scanner computer**.  

### dependencies

The **scanner computer** requires additional `python` libraries in order to run **Pyneal Scanner**.

You can attempt to install all required libraries at once by navigating into the `pyneal_scanner` directory and typing:

>pip install -r requirements.txt

If that fails for any reason, you can install manually one at a time:

>pip install numpy==1.13.1  
>pip install pydicom==0.9.9  
>pip install nibabel==2.1.0  
>pip install pyzmq==16.0.2  
>pip install pyyaml==3.12

These versions reflect the primary environment in which **Pyneal** is tested. It is likely that other versions maintain compatibility, but use at your own risk.


## Pyneal

The `pyneal` directory needs to be on the **analysis computer**.

### dependencies

The **analysis computer** requires additional `python` libraries in order to run **Pyneal**.

You can attempt to install all required libraries at once by navigating into the `pyneal` directory and typing:

>pip install -r requirements.txt

If that fails for any reason, you can install manually one at a time:

>pip install numpy==1.13.1  
>pip install nibabel==2.1.0  
>pip install pyzmq==16.0.2  
>pip install pyyaml==3.12  
>pip install kivy==1.10.dev0  
>pip install flask==0.12.2  
>pip install flask_socketio==2.9.2  
>pip install eventlet==0.21.0  

These versions reflect the primary environment in which **Pyneal** is tested. It is likely that other versions maintain compatibility, but use at your own risk.

### Misc Utilities

**Pyneal** itself does not require any additional libaries beyond what is listed above. However, there are various tools included that you may find useful during a real-time scan session. For instance, the tool **createMask** can be used to transform a standard space ROI mask to the subject's functional space, which can then be used as a mask for analysis during a real-time scan. 

In order to use these additional tools, make sure you have installed the following:

* [FSL 5.0](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki)