# Frequently Asked Questions

## Which port numbers should I use when configuring Pyneal Scanner/Pyneal?

**Pyneal** communicates with other components in the pipeline, like **Pyneal Scanner** and and **End User**, via TCP/IP sockets. These are network communication portals very similar to how an internet browser communicates with websites hosted on remote servers. 

For this type of commnunication, it's useful to think of one end as the *server*, listening for and responding to requests from remote *clients*. Clients connect to the server by specifying the server's IP address and a specific port number. 

In our case, **Pyneal** (running on the **analysis computer**) is always playing the role of the *server*. The IP address you use for **Pyneal** will depend on how the rest of your environment is set up:

* If all components are running on the same machine, you can use the generic loopback IP address `127.0.0.1`. Put another way, you can use this address if and only if **Pyneal Scanner** and **Pyneal** and any **End User** that requests data are all running from the same physical machine. This might be the case, for instance, if you are testing/debugging certain steps of your analysis (see [**simulations**](simulations.md)

* In all other cases, you have to figure out the IP address assigned to the **analysis computer** running **Pyneal**. 

**Pyneal** will use one available port number for communication with **Pyneal Scanner**, and an additional port number dedicated for communication with remote end users or devices. You can manually specify the port number to use when setting up **Pyneal** 

If you don't know which port numbers to use, check with a network administrator, or simply try choosing ones in the range of 1024-49151. If you happen to choose a port number that is unavailable, **Pyneal** will return an error message. In that event, try a different number. 


