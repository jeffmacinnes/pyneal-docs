# Pyneal

## Before a real-time scan

### Creating Masks
Pyneal requires the user to supply a mask that will specify which voxels to include during the real-time analysis. 

This mask can take any form you want, with the caveat that it *must* be in the same space (i.e. voxel size, image resolution, and orientation) as the incoming functional data throughout the real-time scan.

#### Examples:

* **Mask from functional ROI**: You could include a mask that represents voxels with significant task-induced activation from the current subject. To do so, include a quick localizer task at the beginning of your session that you can access offline (for instance, by using the `getSeries.py` tool in **Pyneal Scanner**) and analyze. Threshold and/or binarize the resulting statistical maps as appropriate, and create a funtional ROI mask file. 

* **Mask from anatomical ROI**: You can create a subject-specific anatomical ROI mask by transforming a preselected MNI space mask to the participant's functional space. **Pyneal** includes an automated tool to assist in this process. See [**Creating Masks**](/createMask.md) under *Additonal Tools* 


### Choosing Analyses


## During a real-time scan

### Pyneal Dashboard

### Requesting Results

## After a real-time scan


