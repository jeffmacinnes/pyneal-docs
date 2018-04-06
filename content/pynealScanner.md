# Pyneal Scanner (detailed)

This section will provided a more detailed overview of **Pyneal Scanner**, what is happening behind the scenes, and how to customize it for different imaging environments. 

Before beginning, make sure you've followed the instructions at [**setup: Pyneal Scanner**](/setup.md#pyneal-scanner) to configure **Pyneal Scanner** to your environment. 



## 

* Make sure you have followed the [**installation**](/installation.md) and [**setup**](/setup.md) instructions. 

* Figure out the IP address of the machine that is going to be the **analysis computer** running **Pyneal**. You'll need this address in order to configure **Pyneal Scanner**, as well as to request any results during the scan itself. This IP address must be accessible from the same network as the **scanner computer** (and any **end user** computer that will be making requests to **Pyneal** for results during the scan)

* Determine the port numbers to use for commmuncation. Pyneal will need to have one available port number dedicated for communication with **Pyneal Scanner**, and an additional port number dedicated for communication with remote end users or devices. 
	* If you don't know which port numbers to use, try choosing ones in the range of 1024-49151. If you happen to choose a port number that is already in use, **Pyneal** will return an error message. In that event, try a different number. 

* Once you have determined the IP address and port numbers to use with **Pyneal** on the **analysis computer**

## 