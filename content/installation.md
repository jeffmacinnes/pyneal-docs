# Installation

**Pyneal is built and tested using `Python 3.6`**

Download Python from [**https://www.python.org/downloads/**](https://www.python.org/downloads/) or via a distribution like [**Anaconda**](https://www.anaconda.com/download)

Pyneal requires additional libraries beyond the standard library. Instructions below use `pip` to install these libraries. Verify that you have `pip` installed:

>which pip

If not, download and install pip from [**https://pip.pypa.io/en/stable/installing/**](https://pip.pypa.io/en/stable/installing/)


## Download Pyneal

Download the [**Pyneal repository**](https://github.com/jeffmacinnes/pyneal) from GitHub, or clone to your local machine:


>git clone https://github.com/jeffmacinnes/pyneal.git


The installation instructions are broken down by **Pyneal Scanner** and **Pyneal**. If you haven't already, read the section on [**definitions**](#definitions-used), as those definitions are used throughout these instructions.


## Pyneal-Scanner

The `pyneal_scanner` directory needs to be on the **scanner computer**. If the **scanner computer** is different from the **analysis computer** in your environment, copy the `pyneal_scanner` directory to the **scanner computer**.  

### dependencies

The **scanner computer** requires additional `python` libraries in order to run **Pyneal Scanner**.

You can attempt to install all required libraries at once by navigating into the `pyneal_scanner` directory and typing:

>pip install -r requirements.txt

If that fails for any reason, you can install manually one at a time:

>pip install numpy==1.13.1  
>pip install pydicom==1.0.2  
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
>pip install nipy==0.4.1  
>pip install pyzmq==16.0.2  
>pip install pyyaml==3.12  
>pip install kivy==1.10.dev0  
>pip install flask==0.12.2  
>pip install flask_socketio==2.9.2  
>pip install eventlet==0.21.0  

These versions reflect the primary environment in which **Pyneal** is tested. It is likely that other versions maintain compatibility, but use at your own risk.

Some users have reported problems installing the development version of kivy (under Pyneal dependencies). For assistance with this step, and other issues, see [**Troubleshooting**](/troubleshooting.md)

## Additional Tools

**Pyneal** itself does not require any additional libaries beyond what is listed above. However, there are various tools included that you may find useful during a real-time scan session. For instance, the tool [**createMask**](/createMask) can be used to transform a standard space ROI mask to the subject's functional space, which can then be used as a mask for analysis during a real-time scan.

In order to use these additional tools, make sure you have installed the following:

* [**FSL 5.0**](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki)
