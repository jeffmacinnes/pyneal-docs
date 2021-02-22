# Pyneal Scanner

![](images/pynealScanner/pynealScanner.png)

First step, make sure you've followed the instructions at [**setup: Pyneal Scanner**](setup.md#pyneal-scanner) to configure **Pyneal Scanner** to your environment.

## Directory Structure

The **Pyneal Scanner** directory has the following structure:

```
├── pyneal_scanner
│   ├── README.md
│   ├── data
│   ├── getSeries.py
│   ├── listSeries.py
│   ├── pynealScanner.log
│   ├── pynealScanner.py
│   ├── requirements.txt
│   ├── scannerConfig.yaml
│   ├── simulation
│   └── utils
```

The root level of the directory contains basic commands for launching **Pyneal Scanner** (`pynealScanner.py`), and accessing information about the current scanning session (`getSeries.py`, `listSeries.py`).

**Subdirectories**:

- **`data/`**: Any data that **Pyneal Scanner** saves to disk during a scanning session. For instance, using `getSeries.py` to build a nifti-formatted image from the current session will result in that file being written to this directory.

- **`simulation/`**: Tools for simulating inputs and outputs of **Pyneal Scanner**. See [**simulations: Pyneal Scanner Simulation Tools**](simulations/#pyneal-scanner-simulation-tools)

- **`utils/`**: General and MRI manufacturer specific tools for settings up a scanning session, monitoring for incoming data during a scan, and processing/sending data to **Pyneal** throughout a scan.

## Basic Usage

To launch **Pyneal Scanner** from the **scanner computer**, open a terminal and navigate to the `pyneal_scanner` directory. From the `pyneal_scanner` directory, type:

> python pynealScanner.py

If you have set up **Pyneal Scanner** correctly, you will see a print out of your settings, info about any existing series directories within the `scannerSessionDir` path, and a message that **Pyneal Scanner** is attempting to connect to **Pyneal** over the specified `pynealSocket`:

> ===============  
> SCANNER SETTINGS:  
> pynealSocketHost: 127.0.0.1  
> pynealSocketPort: 5555  
> scannerSessionDir: /path/to/scanner/sessionDir  
> scannerMake: GE  
> ============
>
> Series Dirs:  
>  s1923 23.6 MB 5 min, 13 s ago  
>  s1925 26.2 MB 1 min, 10 s ago  
> MainThread - Connecting to pynealSocket...

Once you launch **Pyneal** on the **analysis computer**, you will see a confirmation that **Pyneal Scanner** has connected to **Pyneal**, and is now waiting for new data to arrive from the scanner:

> MainThread - pynealSocket connected  
> MainThread - Waiting for new seriesDir...

## How it works

Behind the scenes, **Pyneal Scanner** is running two separate threads. One thread is dedicated to monitoring the specifed directory for new data to appear. Whenever new data arrives, it places it in a queue. The 2nd thread is responsible for pulling data off of that queue, preprocessing it to convert to a standardized format, and then sending the reformatted data to **Pyneal** over a socket connection (defined by `pynealSocketHost` and `pynealSocketPort` in the configuration file).

Depending on which type of scanner you are using, the directory structure for where new data will appear, and the format that it will appear in, can differ drastically. **Pyneal Scanner** comes with utilities designed to handle the directory structures and formats of 3 different scanner manufacturers: **GE**, **Philips**, and **Siemens**.

## Directory structures and data formats by scanner make

**Pyneal Scanner** is designed to handle the standard data formats used across the 3 dominant scanner manufacturers, **GE**, **Philips**, and **Siemens**. This section will provide details on the directory structures and data formats across each in order to help make sure you configure **Pyneal Scanner** correctly.

### GE

- _expected data format_: dicom files, one file per slice. Each dicom file must contain the following tags:

  - `Columns`
  - `ImagesInAcquisition`
  - `ImageOrientationPatient`
  - `ImagePositionPatient`
  - `InStackPositionNumber`
  - `InstanceNumber`
  - `MRAcquisitionType`
  - `NumberOfTemporalPositions`
  - `PixelSpacing`
  - `Rows`
  - `SliceThickness`

- _expected directory structure_: new dicom files are written to a directory on the scanner console. The path to that directory can be broken apart as:

  - `[sessionDir]/[seriesDir]`, where

    - `[sessionDir]`: directory where new subdirectories appear for each series throughout a session. On GE systems, these path to the session directory may end in a pattern like `p###/e###`.
    - `[seriesDir]`: series specific directory named like `s###` where the specific `#` values are unknown in advance. Each new scan during a given exam session will be assigned a unique `s###` dir.

    To figure out the `sessionDir` and `seriesDir` for the current scan session, see the [**listSeries**](pynealScanner.md#listseries) command below.

### Philips

- _expected data format_: new PAR/REC file pairs, where each file pair represents a 3D volume.

- _expected directory structure_: Philips scanners have the option to export reconstructed PAR/REC files to a remote directory. The path to that directory can be broken apart as

  - `[scannerSessionDir]/[seriesDir]`, where

    - `[scannerSessionDir]`: path to remote directory that remains constant across all scans

    - `[seriesDir]`: series specific directory named like `0###`, where the directory name is a 4-character number (zero padded as necessary) that increases sequentially with each new series. There is a unique series directory for each scan.

### Siemens

- _expected data format_: dicom mosaic files, where each file represents all slices from a 3D volume, arranged in mosaic format. File names are expected to follow a pattern like `###_######_######.dcm`, where the 2nd field represents the series number, and the 3rd field represents the volume number.

- _expected directory structure_: Siemens scanners have the option to export reconstructed dicom mosaic files to a remote directory. The path to that directory can be refered to as

  - `[scannerSessionDir]`

  The `[scannerSessionDir]` will contain all of the volume files for _all series_ in a given scan session.

## Sending data to Pyneal

During a scan, **Pyneal Scanner** will automatically send data to **Pyneal** over a socket connection (defined by `pynealSocketHost` and `pynealSocketPort` in the configuration file).

Regardless of how the data is formatted coming off of the scanner (see [**Directory structures and data formats by scanner make**](pynealScanner.md#directory-structures-and-data-formats-by-scanner-make) above), **Pyneal Scanner** will convert everything to a standardized format before sending to **Pyneal**.

Specifically, **Pyneal Scanner** will send data as 3D volumes. Each transmission actually takes place in 2 waves:

- First, a JSON header that contains metadata about the current volume, including fields for:

  - `volIdx` - volume index (0-based) of the current volume
  - `dtype` - datatype of the volume array
  - `shape` - dimensions of the volume array
  - `affine` - affine transformation that will convert the volume array to RAS+ orientation (see [**Image Orientation**](imageOrientation.md) for more info)

- Second, the data array for the current volume.

**Pyneal** will use information in the header message to rebuild the volume array, and carry out all subsequent preprocessing and analysis steps.

## Additional commands

The `pyneal_scanner` directory also contains a couple of other commands that may be useful during a real-time session

### listSeries

- location: `pyneal_scanner/listSeries.py`
- usage: `python listSeries.py`

`listSeries.py` will print to the screen a list of all of the series for the current session. Each series will include information like the relevant paths, directory/file sizes, and creation dates. In the case of GE scanners, this will also report the `p###/e###` parent directories (i.e. the `sessionDir`) of new series directories.

### getSeries

- location: `pyneal_scanner/getSeries.py`
- usage: `python getSeries.py`

`getSeries.py` will build a nifti file from a selected series from the current session. When called, it will print a list of all series for the current session, and prompt you to select one. You will also be prompted to specify an 'output prefix' that will be used to name the output file.

You can select series that correspond to either 3D structural series or 4D functional series. The selected series will be converted to a single nifti file, and saved as:

`pyneal_scanner/data/<output prefix>_<seriesName>.nii.gz`

This tool is useful if you need to retrieve data during a session (for example, a localizer run that will be analyzed to create ROIs for the real-time runs).
