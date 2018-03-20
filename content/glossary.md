# Glossary

## Computers
The documentation refers to computers by their *functional* role:

* **Scanner computer**: The computer where reconstructed images from the scanner appear. In the case of GE scanners, for instance, new slice dicom files appear in a directory on the scanner console. Siemens scanners, on the other hand, may export new images to a directory on a shared network drive. The **scanner computer** is simply the computer that has local access to the directory where new images appear

* **Analysis computer**: The computer that will be running **Pyneal**. This is the computer on which users will setup their analysis, launch **Pyneal**, and monitor on-going scans.

Note that in some cases, the *same physical computer* can play both functional roles. For instance, when working in a Siemens environment, new images from the scanner might be exported to a shared directory that is accessible on the **analysis computer**. In this case, the same machine could be playing the role of both the **scanner computer** and the **analysis computer**.

* **End User**: Generic term for any computer/process that is making a request to **Pyneal** for results during a scan. For instance, a task presentation computer that is requesting specific feedback values to present to the participant. 

## Additional terms used

* **Series**: A complete scan representing either a single 3D anatomical image, or a 4D functional image.

* **Session**:  A collection of series collected within the same experimental session. A **session** would typically represent all of the scans collected after the subject is placed in the scanner (e.g. Anatomical, functional series1, functional series2, etc...)