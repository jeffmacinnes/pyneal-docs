# Creating Masks

**Pyneal** requires that you input a mask for use during real-time analysis. This mask must have the same voxel dimensions and image orientation as the incoming functional data. 

The `createMask.py` tool will assist you in quickly creating these masks during a real-time session. 

**createMask** provides you with two mask creation options:

* **Whole Brain Mask**: This option will create a whole brain mask from the functional data you supply. 

* **Transform mask from MNI space**: This option will take a mask defined in MNI space and transform it to the dimensions and orientation of the functional data you supply.

*Note:* Behind the scenes, createMask.py relies on various functions from FSL. Make sure you have installed [FSL 5.0](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki)

## Launching createMask
The createMask tool is found in `pyneal/utils/createMask.py`

You can launch the createMask GUI by navigating to the `utils` directory via the terminal and running `createMask.py` with Python

> cd utils  
> python createMask.py


![](images/createMaskGUI.png)

## Specifying a reference 4D functional file

In order to create masks, we need to know the voxel size, 3D volume dimensions, and image orientation of the functional data for the current session. The easiest way to get this data is to include a brief (30sec or less) functional scan near the beginning of your session. Use the exact same slice prescriptions and image settings as you plan to use during your real-time scans. 

After the scan has finished, use the `getSeries.py` tool from **Pyneal Scanner** to convert the images to a 4D nifti file. Note that `getSeries.py` will automatically reorient the output data to RAS+ orientation. Thus, by using this data as our reference functional data we will create a mask that is also in RAS+. This is good since, during a real-time run, **Pyneal** will be receiving data in RAS+ orientation (see [image orientation](/imageOrientation) for more info) 


## Deciding on a mask type

### Whole Brain Mask
If you check **Create whole-brain FUNC mask**, a 3D whole-brain mask will be created using the 4D FUNC file as a reference. Every brain voxel will be labeled **1** and every non-brain voxel will be labeled **0**.

The output file will be found in `mask_transforms/FUNC_masks/wholeBrain_FUNC_mask.nii.gz`

A whole-brain mask is useful in situations where you are using a custom analysis during real-time runs and want access to the entire 3D brain volume (e.g. calculating grand volume mean as a reference value for other steps in your analysis). 

### Transform MNI space mask


## Output

The output from `createMask.py` will be saved to the same directory that contains your reference 4D file. Within that directory, you will find a new directory named `mask_transforms` that holds all of the output mask files and transformation matrices from `createMask.py`
