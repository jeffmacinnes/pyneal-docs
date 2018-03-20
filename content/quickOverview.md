# Quick Overview
This section will provide a quick overview of running a scan with Pyneal. The aim is to  familiarize you with the interface and commands you would use during a scan session, without getting lost in the details about what is happening underneath the hood. 

For a more in-depth discussion of the main components, see [**Pyneal Scanner**](/pynealScanner.md) and [**Pyneal**](/pyneal.md).

## Main Components
Throughout this overview, we'll refer to 3 main components of a typical real-time session:

1. **Pyneal Scanner**: The component that has access to raw data direct from the scanner. This component runs on the **scanner computer**. 

## Prior to the scan...

* Make sure you have followed the [**installation**](/installation.md) and [**setup**](/setup.md) instructions. 

* Figure out the IP address of the machine that is going to be the **analysis computer** running **Pyneal**. You'll need this address in order to configure **Pyneal Scanner**, as well as to request any results during the scan itself. This IP address must be accessible from the same network as the **scanner computer** (and any **end user** computer that will be making requests to **Pyneal** for results during the scan)

* Determine the port numbers that you would like to use for  
