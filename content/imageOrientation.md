# Image Orientation

Throughout the **Pyneal** pipeline, from the *output* stage of **Pyneal Scanner** onward, we use the convention of orienting the images to **RAS+**. This means:

* The **1st** axis (x) is oriented *from* **left** *to* **right**
* The **2nd** axis (y) is oriented *from* **posterior** *to* **anterior**
* The **3rd** axis (z) is oriented *from* **inferior** *to* **superior**

Visually, the **RAS+** coordinate system is arranged like: 

![](images/imageOrientation/RAS_orientation.png)

There are a number of stages throughout the pipeline where this is important to keep in mind:

## Output from Pyneal Scanner

**Pyneal Scanner** is designed to accept a variety of inputs from various scanner manufactures and imaging environments. One of **Pyneal Scanner's** important functions is to take the input data, in whatever form it appears, and convert it to a standardized format before passing each volume along to **Pyneal**. 

![](images/pynealScanner/pynealScanner.png)

**Pyneal** expects each volume to arrive from **Pyneal Scanner** in **RAS+** orientation. 


## Creating masks for Pyneal




