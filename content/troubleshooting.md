# troubleshooting

## Installation

### problems installing kivy

If you have followed the instructions under [**Installation**: Pyneal](/installation.md#pyneal) but are still having trouble getting Kivy to work, there are a couple of other options you may want to try. 

First off, check out [**detailed Kivy installation instructions**](https://kivy.org/docs/installation/installation-osx.html#using-homebrew-with-pip) to see if there are any tips. 

Second, you can try to manually compile Kivy following these steps

* clone the Kivy repo from github:

> git clone https://github.com/kivy/kivy

* Navigate into the cloned `kivy` directory and set environmental variables:

> cd kivy  
> export USE_SDL2=1  
> export USE_GSTREAMER=1  

In order for this to work, make sure you have installed the SDL2 and GSTREAMER libraries for Kivy listed under [**Kivy Libraries**](/installation.md#[Option-1]-Using-Homebrew)

* run `make` to compile the package

> make

If this proceeded without error, test by running **Pyneal** to see if the GUI appears:

> python pyneal.py  


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