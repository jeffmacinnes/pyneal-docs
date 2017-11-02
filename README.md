# Pyneal-Docs

Documentation for Pyneal Real-time fMRI software

[Pyneal Repo](https://github.com/jeffmacinnes/pyneal)

[Pyneal-Docs website](https://jeffmacinnes.github.io/pyneal-docs/)


This repo stores the content of the pyneal documentation website, as well as the scripts to deploy the website. 

### Editing content
All content is stored in the **chapters** dir. 

*add more notes about how to arrange content in this dir, and how to update the order.txt file*

### Deploying website
The website can be created by calling the python script *createWebBook.py* that is found in the **scripts** directory. This script will take the content of the **chapters** directory, translate it to HTML, and store the output in the **docs** directory. 

Once created, commit and push the changes to the pyneal-docs remote repository on github. The repo is set up to read whatever is in the **docs** dir in the repo, and host it as a static website at:

**https://jeffmacinnes.github.io/pyneal-docs/**


---
This documentation site is modeled off of, and built stealing tools from, the wonderful [OpenFrameworks Book](https://github.com/openframeworks/ofBook)