# troubleshooting

## Installation

## Network Issues
### Address already in use

You go to launch Pyneal and in the terminal you see an error that reads something like 

>zmq.error.ZMQError: Address already in use

**Cause**: Pyneal is trying to create a socket on a port that is already in use. This could occur if:  

* A) There is another application currently using the same port(s) that Pyneal is trying to use  
* B) Pyneal failed to properly close the port(s) the last time you used it

**Diagnose**

1) Confirm which ports Pyneal is trying to use. By default, Pyneal uses ports in the 5555-5558 range; To verify, check the settings that are printed to the terminal when you run Pyneal, in particular:

```
MainThread -  Setting: dashboardClientPort: 5558
MainThread -  Setting: dashboardPort: 5557
MainThread -  Setting: pynealScannerPort: 5555
MainThread -  Setting: resultsServerPort: 5556
```

2) Next, check which processes are currently using those ports. In a terminal, type:

> lsof -i :5555-5558

and you will be presented with a list Process IDs (PID column) currently using ports within that range:

```
COMMAND     PID USER   FD   TYPE            DEVICE SIZE/OFF NODE NAME
Python    21115 jeff   14u  IPv4 0xb42eb5e0931fdff      0t0  TCP localhost:personal-agent (LISTEN)
Python    21115 jeff   17u  IPv4 0xb42eb5dfde84dff      0t0  TCP *:freeciv (LISTEN)
Python    21115 jeff   24u  IPv4 0xb42eb5e0a2ca47f      0t0  TCP localhost:52786->localhost:5557 (ESTABLISHED)
Python    21115 jeff   25u  IPv4 0xb42eb5e0922647f      0t0  TCP localhost:52787->localhost:5557 (ESTABLISHED)
Python    21115 jeff   26u  IPv4 0xb42eb5e315700ff      0t0  TCP localhost:52788->localhost:5557 (ESTABLISHED)
Python    21115 jeff   30u  IPv4 0xb42eb5e095bf0ff      0t0  TCP localhost:52789->localhost:5557 (ESTABLISHED)
```
This output indicates that Python is currently running a process that is occupying port `5557`. Despite the multiple lines, note that there is just a single process ID (PID) represented. In this case, it appears as though Pyneal has failed to properly close the socket on port 5557 the last time you ran it (unless you happen to be running other unrelated Python processes simultaneously that also happen to be using those same port numbers as Pyneal). Alternatively, if you see a different application listed under `COMMAND`, it would indicate that there is another active process on your machine that is competing for ports with Pyneal.

**Fixes**

* **Option 1**: Kill the competing process. Once you have identifed which process is occupying the port you are trying to use, you can kill it by typing:

	> kill -9 PID
	
	Where `PID` is the process ID (PID) from the output above
	
* **Option 2**: Make Pyneal use a differnt Port #. If you **do not** want to stop the competing process, you can have Pyneal use different port numbers by manually editing your config file: 
	1. Open your custom config file (or use the default one at `pyneal/src/GUIs/pynealSetup/setupConfig.yaml`)
	2. change the port number entries to use new ports (note: port numbers can range from `0-65535` but numbers `0-1023` are typically reserved for priveledged system processes)
	
```
...
dashboardClientPort: 7000  
dashboardPort: 7001  
pynealScannerPort: 7002  
resultsServerPort: 7003  
```
	


## Pyneal Scanner


## Pyneal


## Creating Masks

### My output masks are misaligned

In addition to creating the desired masks, the [**createMask.py**](createMask.md) tool creates a number of additional output files that can be used to help diagnose issues. Within the `mask_transforms` directory, check the quality of the following output files for clues:

* **exampleFunc.nii.gz** - mean 3D functional image, created by collapsing the input 4D functional image over time

* **hires_brain.nii.gz** - skull stripped version of the input anatomical image. If the default skull stripping performs poorly, try to skull strip the anatomical image manually, and then re-run `createMask.py` with the newly skull stripped image (and make sure to deselect the `skull strip?` option within the `createMask.py` GUI). 

* **hires_FUNC.nii.gz** - the hi-res anatomical transformed to functional space. Problems with this image suggest the hires2func transformation matrix failed. 

* **mni_HIRES.nii.z** - the MNI standard image transformed to hi-res anatomical space. Problems with this image suggest the mni2hires tranformation matrix failed. 