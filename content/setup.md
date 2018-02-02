#

The set-up instructions are broken down by **Pyneal Scanner** and **Pyneal**. If you haven't already, follow the [installation instructions](/installation) to configure your environment, and read the section on [definitions](installation/#definitions-used), as those definitions are used throughout these instructions. 


## Pyneal Scanner

Copy the `pyneal_scanner` directory to the **scanner computer**. 

Launch **Pyneal Scanner** from the command line by navigating in to the `pyneal_scanner` directory and running `pynealScanner.py`



> cd pyneal_scanner  
> python pynealScanner.py



**Pyneal Scanner** uses a set of configuration parameters that you can modify to fit your environment. These are stored in file named `scannerConfig.yaml` in the `pyneal_scanner` directory. 

If you're running **Pyneal Scanner** for the first time, this file won't exist yet. You can either create this file manually, or wait until `pynealScanner.py` prompts you to fill in any missing configuration values from the command line. Any values you enter from the command line will be saved in a new `scannerConfig.yaml` file. 

The `scannerConfig.yaml` file allows you to customize **Pyneal Scanner** to your scanning environment. The file contains just a few parameters stored as *key:value* pairs:

```yaml
scannerBaseDir: /path/to/new/scans
scannerMake: GE
pynealSocketHost: 127.0.0.1
pynealSocketPort: '9999'
``` 

**Configuration Keys**:

* **scannerBaseDir**: The *fixed* portion of the directory path to where new reconstructed images will be appear during a scan. That is, the part that remains constant from scan to scan. Knowing what to set this value to can differ accroding to different scanner manufacturers: 

	* **GE**: During a scan, new slices dicom files are written to a directory on the scanner console. The path to that directory can be broken apart like `[scannerBaseDir]/[sessionDir]/[seriesDir]`, where
		* **[scannerBaseDir]**: path that remains constant across all scans
		* **[sessionDir]**: directories that can change from session to session, named like `p###/e###` where the specific `#` values are unknown in advance.
		* **[seriesDir]**: series specific directory named like `s###` where the specific `#` values are unknown in advance. Each new scan during a given exam session will be assigned a unique `s###` dir. 

		You only need to specify the path to the `scannerBaseDir` in the `scannerConfig.yaml` file; **Pyneal Scanner** will automaticaly find the most recently modified session and series directories and monitor for new series directories to appear. When you run `pynealScanner.py` you will see a printout in the terminal window about the names, sizes, and modification dates of all series directories in the session directory.
		

	* **Siemens**: TODO
	
	* **Philips**: Philips scanners have the option to export reconstructed PAR/REC files to a remote directory. The path to that directory can be broken apart like `[scannerBaseDir]/[seriesDir]`, where
		* **[scannerBaseDir]**: path to remote directory that remains constant across all scans
		* **[seriesDir]**: series specific directory named like `####`
	
	You only need to specify the path to the `scannerBaseDir` in the `scannerConfig.yaml` file; **Pyneal Scanner** will monitor for new series directories to appear.  

	 
* **scannerMake**: Scanner Manufacturer, must be one of `GE`, `Siemens`, or `Philips` (case sensitive)
* **pynealSocketHost**: I.P. address of the **analysis computer** running **Pyneal**.
* **pynealSocketPort**: The port number over which **Pyneal** is listening for incoming data. 




## Pyneal

Launch **Pyneal** from the command line by navigating in to the `pyneal` directory and running `pyneal.py`



> cd pyneal   
> python pyneal.py


The **Pyneal** configuration is set via GUI. When you launch `pyneal.py` a GUI will appear, allowing you to configure **Pyneal** to the current experiment

![](images/pynealSetupGUI.png)