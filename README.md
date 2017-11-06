# Pyneal-Docs

Documentation for Pyneal Real-time fMRI software

[Pyneal Repo](https://github.com/jeffmacinnes/pyneal)

[Pyneal-Docs website](https://jeffmacinnes.github.io/pyneal-docs/)


This repo stores the content of the pyneal documentation website, as well as the scripts to deploy the website. 

## Editing content
Visiting the website, you'll see the documentation broken up into topic sections. Each topic section is made up of one or more chapters. 

#### Editing Sections
The topic sections are defined within a single text file that you can find in **chapters/order.txt** and is formatted like:

	Section 1
		S1_chapter_1
		S1_chapter_2
	Section 2
		S2_chapter_1
		S2_chapter_2
	...
	
and so on. The "Section #" labels will set the section headings in the navigation bar on the website. The indented chapter titles 
		

All content is stored in the **chapters** dir. Within the **chapters** dir, there are subdirs for each chapter. Each subdir contains a markdown file called **chapter.md** and, (if needed) a directory called **images** to hold any images that the chapter may reference. 

### Adjusting the order of sections
Within the **chapters** dir, there is also a file named **order.txt**. You can adjust the order 




## Deploying website
The website can be created by calling the python script *createWebBook.py* that is found in the **scripts** directory. This script will take the content of the **chapters** directory, translate it to HTML, and store the output in the **docs** directory. 

Once created, commit and push the changes to the pyneal-docs remote repository on github. The repo is set up to read whatever is in the **docs** dir in the repo, and host it as a static website at:

**https://jeffmacinnes.github.io/pyneal-docs/**


---
This documentation site is modeled off of, and built stealing tools from, the wonderful [OpenFrameworks Book](https://github.com/openframeworks/ofBook)