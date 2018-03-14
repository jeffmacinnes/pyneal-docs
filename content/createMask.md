# Creating Masks

**Pyneal** requires that you input a mask for use during real-time analysis. This mask must have the same voxel dimensions and image orientation as the incoming functional data. 

The `createMask.py` tool will assist you in quickly creating these masks during a real-time session. 

*Note:* Behind the scenes, createMask.py relies on various functions from FSL. Make sure you have installed [FSL 5.0](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki)

## Launching createMask
The createMask tool is found in `pyneal/utils/createMask.py`

You can launch the createMask GUI by navigating to the `utils` directory via the terminal and running `createMask.py` with Python

> cd utils  
> python createMask.py


![](images/createMaskGUI.png)

