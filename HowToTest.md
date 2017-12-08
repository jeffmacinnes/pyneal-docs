# Various forms of testing
You can think about data being passed through the Pyneal pipeline in various stages:

1. **Scanner**: Raw data from the scanner, which gets passed to
2. **Pyneal_Scanner**: Receives raw data and reformats, then passes to
3. **Pyneal**: Analyzes reformatted data, output gets passed to
4. **[???]**: makes use of the analyzed output somehow

In order to faciliate debugging and testing, there are various simulation tools written to simulate the output from each of these steps. For instance, if you want to test **Pyneal**, you can run the *Pyneal_Scanner simulator*, instead of having to run an actual scan (or even simulate an actual scan and have the data be passed through **Pyneal_Scanner** proper). This can make debugging a whole lot easier. 

**Steps for how to simulate each of these steps are found below:**

## simulate the *Scanner*
**What's Simulated:**  
This will simulate the appearance of raw data coming off of the scanner. The format of the raw data will vary according to different scanner environments/manufacturs. Accordingly, there are multiple scripts that will simulate different types of data 

**Use Case:**  
Use this when you want to test out anything further downstream in the pipeline. 

**Steps:** 
Scanner simulation scripts can be found in:

`[pynealDir]/pyneal_scanner/simulation`

### GE:  
script: `GE_sim.py inputDir [-o outputDir -t/--TR TR]`

input args:  
 
* inputDir: path to directory containing raw slice dicoms
* -o outputDir: path to directory where slices will be copied to [default: <inputDir>/s9999]
* -t/--TR TR: set the TR in ms [default: 1000]
 
In order to run this script, you must have a local directory that contains raw slice dicom files from an actual scan. 

This script will copy all of the slices from the inputDir and copy them to the outputDir at a rate that is set by the TR


## simulate *Pyneal_Scanner*
**What's Simulated:**  
This will mimic the output that Pyneal_Scanner produces during an actual run. Specifically, this will generate fake data that is formatted according to the Pyneal standard, and send it out over a socket connection. You can change parameters about the data (e.g. image dimensions, TR) or the socket connection (e.g. host, port number) by editing values near the top of the script. 

**Use Case:**  
Use this when you want to test out *Pyneal* without having to run (or simulate) an actual scan. 

**Steps:** 
The Pyneal_Scanner simulation script can be found in:
`[pynealDir]/simulation`


### Usage:
script: `pynealScanner_sim.py`
