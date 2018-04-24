This schematic gives a very broad overview of the path that data follows throughout a real-time scan with **Pyneal**

![](images/dataflow/dataFlow.png)

* Once the scan begins, raw images are collected by **Pyneal Scanner**, and then converted and reoriented to a standardized format (see [**image orientation**](/imageOrientation.md) for more info). 
* [**Pyneal Scanner**](pynealScanner.md) exports converted 3D volumes to [**Pyneal**](pyneal.md).
* [**Pyneal**](pyneal.md) receives 3D volumes, and concatenates them into a 4D volume over time throughout the scan. With every new 3D volume that arrives, [**Pyneal**](pyneal.md) will preprocess the volume, and run any specified analyses. 
* The analysis results for each volume are stored on a separate server, which listens for requests from remote end users or devices throughout the scan (see [**requesting results**](/pyneal.md#requesting-results) for more info). 
* Anytime a request is received, the server checks to see if that volume has been processed yet. If so, it returns the results; if not, it sends a message saying that volume has not been processed yet

