# Overview

Download the [Pyneal repository](https://github.com/jeffmacinnes/pyneal) from GitHub, or clone to your local machine:

>git clone https://github.com/jeffmacinnes/pyneal.git

The software tool is broken into two separate components: **Pyneal Scanner** and **Pyneal**.
**Pyneal Scanner** is contained entirely in the `pyneal_scanner` directory of this repository.

* **Pyneal Scanner**: Accesses incoming data, modifies it to match a standardized format, and then sends the data out, one 3D volume at a time, to **Pyneal**

* **Pyneal**: Listens for incoming 3D volumes from **Pyneal Scanner**, runs whatever analyses
you have specied, and hosts the results on a server, which other downstream components (e.g. an experimental task) can make requests to

This design allows the software to easily accommodate the various directory structures and  data formats that are found on different scanner models at different institutions around the world.

However, this feature also means that the specific installation instructions can vary by computing environments.


#### Definitions Used

For the purposes of these instructions, we'll refer to computers by their *functional* role:

* **Scanner computer**: The computer where reconstructed images from the scanner appear. In the case of GE scanners, for instance, new slice dicom files appear in a directory on the scanner console. Siemens scanners, on the other hand, may export new images to a directory on a shared network drive. The **scanner computer** is simply the computer that has local access to the directory where new images appear

* **Analysis computer**: The computer that will be running **Pyneal**. This is the computer on which users will setup their analysis, launch **Pyneal**, and monitor on-going scans.

Note that in some cases, the *same* physical computer can play both functional roles. For instance, when working in a Siemens environment, new images from the scanner might be exported to a shared network drive. In this case, the same machine could be playing the role of both the **scanner computer** and the **analysis computer**.

## Pyneal-Scanner

The `pyneal_scanner` directory needs to be placed  


### Pyneal

### Misc Utilities
