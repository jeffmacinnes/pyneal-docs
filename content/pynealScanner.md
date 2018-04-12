# Pyneal Scanner

![](images/pynealScanner/pynealScanner.png)

First step, make sure you've followed the instructions at [**setup: Pyneal Scanner**](setup.md#pyneal-scanner) to configure **Pyneal Scanner** to your environment. 


## Basic Usage 

To launch **Pyneal Scanner** from the **scanner computer**, open the command line and navigate to the `pyneal_scanner` directory. From the `pyneal_scanner` directory, type:

> python pynealScanner.py

If you have set up **Pyneal Scanner** correctly, you will see a print out of your settings, info about any existing series directories in the `scannerBaseDir` path, and a message that **Pyneal Scanner** is attempting to connect to **Pyneal** over the specified `pynealSocket`:

> ===============  
> SCANNER SETTINGS:  
> pynealSocketHost: 127.0.0.1  
> pynealSocketPort: 5555  
> scannerBaseDir: /path/to/scanner/baseDir  
> scannerMake: GE    
> ============     
> Session Dir:  
> /path/to/scanner/baseDir/p1/e666  
> Series Dirs:  
> 		s1923	 23.6 MB	5 min, 13 s ago  
> 		s1925	 26.2 MB	1 min, 10 s ago    
> MainThread -  Connecting to pynealSocket...  

Once you launch **Pyneal** on the **analysis computer**, you will see a confirmation that **Pyneal Scanner** has connected to **Pyneal**, and is now waiting for new data to arrive from the scanner:

> MainThread -  pynealSocket connected  
> MainThread -  Waiting for new seriesDir...

## How it works

Behind the scenes, **Pyneal Scanner** is running two separate threads. One thread is dedicated to monitoring the specifed directory for new data to appear. Whenever new data arrives, it places it in a queue. The 2nd thread is responsible for pulling data off of that queue, preprocessing it to convert to a standardized format, and then sending the reformatted data to **Pyneal** over a socket connection (defined by `pynealSocketHost` and `pynealSocketPort` in the configuration file). 

Depending on which type of scanner you are using, the directory structure for where new data will appear, and the format that it will appear in, can differ drastically. **Pyneal Scanner** comes with utilities designed to handle the directory structures and formats of 3 different scanner manufacturers: **GE**, **Philips**, and **Siemens**. 

## Directory structures and data formats by scanner make

**Pyneal Scanner** is designed to handle the standard data formats used across the 3 dominant scanner manufacturers, **GE**, **Philips**, and **Siemens**. This section will provide details on the directory structures and data formats across each in order to help make sure you configure **Pyneal Scanner** correctly. 

### GE

* *expected data format*: dicom files, one file per slice. Each dicom file must contain the following tags:
	* `Columns`
	* `ImagesInAcquisition`
	* `ImageOrientationPatient`
	* `ImagePositionPatient` 
	* `InStackPositionNumber`
	* `InstanceNumber`
	* `MRAcquisitionType`
	* `NumberOfTemporalPositions`
	* `PixelSpacing`
	* `Rows`
	* `SliceThickness`

* *expected directory structure*: new dicom files are written to a directory on the scanner console. The path to that directory can be broken apart as:

	* `[scannerBaseDir]/[sessionDir]/[seriesDir]`, where
		* `[scannerBaseDir]`: path that remains constant across all scans
		* `[sessionDir]`: directories that can change from session to session, named like `p###/e###` where the specific `#` values are unknown in advance.
		* `[seriesDir]`: series specific directory named like `s###` where the specific `#` values are unknown in advance. Each new scan during a given exam session will be assigned a unique `s###` dir.

		To figure out the `sessionDir` and `seriesDir` for the current scan session, see the [**listSeries**](pynealScanner.md#listSeries) command below.


### Philips

* *expected data format*: new PAR/REC file pairs, where each file pair represents a 3D volume. 

* *expected directory structure*: Philips scanners have the option to export reconstructed PAR/REC files to a remote directory. The path to that directory can be broken apart as

	* `[scannerBaseDir]/[seriesDir]`, where  
		
		* `[scannerBaseDir]`: path to remote directory that remains constant across all scans
	
		* `[seriesDir]`: series specific directory named like `0###`, where the directory name is a 4-character number (zero padded as necessary) that increases sequentially with each new series. There is a unique series directory for each scan. 


### Siemens

* *expected data format*: dicom mosaic files, where each file represents all slices from a 3D volume, arranged in mosaic format. File names are expected to follow a pattern like `###_######_######.dcm`, where the 2nd field represents the series number, and the 3rd field represents the volume number. 

* *expected directory structure*:  Siemens scanners have the option to export reconstructed dicom mosaic files to a remote directory. The path to that directory can be refered to as

	* `[scannerBaseDir]`
	
	The `[scannerBaseDir]` will contain all of the volume files for  *all series* in a given scan session. 


## Sending data to Pyneal

During a scan, **Pyneal Scanner** will automatically send data to **Pyneal** over a socket connection (defined by `pynealSocketHost` and `pynealSocketPort` in the configuration file). 

Regardless of how the data is formatted coming off of the scanner (see [**Directory structures and data formats by scanner make**](pynealScanner.md#directory-structures-and-data-formats-by-scanner-make) above), **Pyneal Scanner** will convert everything to a standardized format before sending to **Pyneal**. 

Specifically, **Pyneal Scanner** will send data as 3D volumes. Each transmission actually takes place in 2 waves:  

* First, a JSON header that contains metadata about the current volume, including fields for:
	* `volIdx` - volume index (0-based) of the current volume
	* `dtype` - datatype of the volume array
	* `shape` - dimensions of the volume array
	* `affine` - affine transformation that will convert the volume array to RAS+ orientation (see [**Image Orientation**](imageOrientation.md) for more info)

* Second, the data array for the current volume. 

**Pyneal** will use information in the header message to rebuild the volume array, and carry out all subsequent preprocessing and analysis steps. 


## Additional commands

The `pyneal_scanner` directory also contains a couple of other commands that may be useful during a real-time session

### listSeries

* location: `pyneal_scanner/listSeries.py`
* usage: `python listSeries.py`

`listSeries.py` will print to the screen a list of all of the series for the current session. Each series will include information like the relevant paths, directory/file sizes, and creation dates. In the case of GE scanners, this will also report the `p###/e###` parent directories (i.e. the `sessionDir`) of new series directories. 

### getSeries

* location: `pyneal_scanner/getSeries.py`
* usage: `python getSeries.py`

`getSeries.py` will build a nifti file from a selected series from the current session. When called, it will print a list of all series for the current session, and prompt you to select one. You will also be prompted to specify an 'output prefix' that will be used to name the output file.  

You can select series that correspond to either 3D structural series or 4D functional series. The selected series will be converted to a single nifti file, and saved as:
 
`pyneal_scanner/data/<output prefix>_<seriesName>.nii.gz`

This tool is useful if you need to retrieve data during a session (for example, a localizer run that will be analyzed to create ROIs for the real-time runs).