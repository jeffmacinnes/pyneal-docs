/Users/jeff/gDrive/jeffCloud/real-time/pyneal/src/GUIs/pynealSetup
<h1 id="pyneal">pyneal</h1>


Pyneal Real-time fMRI Acquisition and Analysis

This is the main Pyneal application, designed to be called directly from the
command line on the computer designated as your real-time analysis machine.
It expects to receive incoming slice data from the Pyneal-Scanner application,
which should be running concurrently elsewhere (e.g. on the scanner console
itself)

Once this application is called, it'll take care of opening the
GUI, loading settings, launching separate threads for monitoring and analyzing
incoming data, and hosting the Analysis output server

<h2 id="pyneal.launchPyneal">launchPyneal</h2>

```python
launchPyneal()
```

Main Pyneal Loop. This function will launch setup GUI,
retrieve settings, initialize all threads, and start processing
incoming scans

<h2 id="pyneal.createOutputDir">createOutputDir</h2>

```python
createOutputDir(parentDir)
```

Create a new output directory in the parent dir. Output directories
are named sequentially, starting with pyneal_001.

This function will find all existing pyneal_### directories in the
parentDir and name the new output directory accordingly.

returns full path to the new output directory

<h1 id="src.scanReceiver">src.scanReceiver</h1>


Class to listen for incoming data from the scanner.

This tool is designed to be run in a separate thread, where it will:
    - establish a socket connection to pynealScanner (which will be sending volume
data from the scanner)
    - listen for incoming volume data (preceded by a header)
    - format the incoming data, and assign it to the proper location in a
    4D matrix for the entire san
In additiona, it also includes various methods for accessing the progress of an
on-going scan, and returning data that has successfully arrived, etc.

--- Notes for setting up:
** Socket Connection:
This tool uses the ZeroMQ library, instead of the standard python socket library.
ZMQ takes care of a lot of the backend work, is incredibily reliable, and offers
methods for easily sending pre-formatted types of data, including JSON dicts,
and numpy arrays.

** Expectations for data formatting:
Once a scan has begun, this tool expects data to arrive over the socket
connection one volume at a time.

There should be two parts to each volume transmission:
    1. First, a JSON header containing the following dict keys:
        - volIdx: within-volume index of the volume (0-based)
        - dtype: datatype of the voxel array (e.g. int16)
        - shape: voxel array dimensions  (e.g. (64, 64, 18))
        - affine: affine matrix to transform the voxel data from vox to mm space
    2. Next, the voxel array, as a string buffer that can be converted into a
        numpy array.

Once both of those peices of data have arrived, this tool will send back a
confirmation string message.

** Volume Orientation:
Pyneal works on the assumption that incoming volumes will have the 3D
voxel array ordered like RAS+, and that the accompanying affine will provide
a transform from voxel space RAS+ to mm space RAS+. In order to any mask-based
analysis in Pyneal to work, we need to make sure that the incoming data and the
mask data are reprsented in the same way. The pyneal_scanner utilities have all
been configured to ensure that each volume that is transmitted is in RAS+ space.

Along those same lines, the affine that gets transmitted in the header for each
volume should be the same for all volumes in the series.

<h2 id="src.scanReceiver.ScanReceiver">ScanReceiver</h2>

```python
ScanReceiver(self, settings)
```

Class to listen in for incoming scan data. As new volumes
arrive, the header is decoded, and the volume is added to
the appropriate place in the 4D data matrix

Input a dictionary called 'settings' that has (at least) the following keys:
    numTimepts: number of expected timepoints in series [500]
    pynealHost: ip address for the computer running Pyneal
    pynealScannerPort: port # for scanner socket [e.g. 5555]

<h3 id="src.scanReceiver.ScanReceiver.createImageMatrix">createImageMatrix</h3>

```python
ScanReceiver.createImageMatrix(self, volHeader)
```

Once the first volume appears, this function should be called
to build the empty matrix to store incoming vol data, using
info from the vol header.

<h3 id="src.scanReceiver.ScanReceiver.get_affine">get_affine</h3>

```python
ScanReceiver.get_affine(self)
```

Return the affine for this series

<h3 id="src.scanReceiver.ScanReceiver.get_vol">get_vol</h3>

```python
ScanReceiver.get_vol(self, volIdx)
```

Return the requested vol, if it is here.
Note: volIdx is 0-based

<h3 id="src.scanReceiver.ScanReceiver.get_slice">get_slice</h3>

```python
ScanReceiver.get_slice(self, volIdx, sliceIdx)
```

Return the requested slice, if it is here.
Note: volIdx, and sliceIdx are 0-based

<h3 id="src.scanReceiver.ScanReceiver.sendToDashboard">sendToDashboard</h3>

```python
ScanReceiver.sendToDashboard(self, msg)
```

If dashboard is launched, send the msg to the dashboard. The dashboard
expects messages formatted in specific way, namely a dictionary with 2
keys: 'topic', and 'content'

Any message from the scanReceiver should set the topic as
'pynealScannerLog', and the content should be it's own dictionary with
the key 'logString'. logString should contain the log message you want
the dashboard to display

<h3 id="src.scanReceiver.ScanReceiver.saveResults">saveResults</h3>

```python
ScanReceiver.saveResults(self)
```

Save the image matrix as a Nifti file in the output directory for this
series

