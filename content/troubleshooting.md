# troubleshooting

## Installation

### problems installing kivy

Some users have reported difficulty installing the `kivy` dependency for **Pyneal**. Kivy is used to create the Pyneal Setup and createMask GUIs, and has its own set of dependencies. If these dependencies don't exist (or they do, but are incompatible versions), using `pip` to install Kivy can fail. 

Please see the [**detailed Kivy installation instructions**](https://kivy.org/docs/installation/installation-osx.html#using-homebrew-with-pip) for help. 

Make sure to specify the development version of kivy in the 2nd step under **Using Homebrew with pip**: `pip install https://github.com/kivy/kivy/archive/master.zip`

## Pyneal Scanner

### Pyneal scanner issue 1

## Pyneal

### Pyneal issue 1

## Creating Masks

### My output masks are misaligned

In addition to creating the desired masks, the [**createMask.py**](createMask.md) tool creates a number of additional output files that can be used to help diagnose issues. Within the `mask_transforms` directory, check the quality of the following output files for clues:

* **exampleFunc.nii.gz** - mean 3D functional image, created by collapsing the input 4D functional image over time

* **hires_brain.nii.gz** - skull stripped version of the input anatomical image. If the default skull stripping performs poorly, try to skull strip the anatomical image manually, and then re-run `createMask.py` with the newly skull stripped image (and make sure to deselect the `skull strip?` option within the `createMask.py` GUI). 

* **hires_FUNC.nii.gz** - the hi-res anatomical transformed to functional space. Problems with this image suggest the hires2func transformation matrix failed. 

* **mni_HIRES.nii.z** - the MNI standard image transformed to hi-res anatomical space. Problems with this image suggest the mni2hires tranformation matrix failed. 