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

## Additional commands

### listSeries
### getSeries

## Directory structures and data formats by scanner make

**Pyneal Scanner** is designed to handle the standard data formats used across the 3 dominant scanner manufacturers, **GE**, **Philips**, and **Siemens**. This section will provide details on the directory structures and data formats across each in order to help make sure you configure **Pyneal Scanner** correctly. 

### GE

### Philips

### Siemens

