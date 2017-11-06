# Pyneal-Docs

Documentation for Pyneal Real-time fMRI software

[Pyneal Repo](https://github.com/jeffmacinnes/pyneal)

[Pyneal-Docs website](https://jeffmacinnes.github.io/pyneal-docs/)


This repo stores the content of the pyneal documentation website, as well as the scripts to deploy the website. 

## Editing content
Visiting the website, you'll see the documentation broken up into Chapters. You can switch between chapters using the navigation bar on the left 

#### Editing Chapters
The chapter orders in the navigation bar are defined within a single text file that you can find in **chapters/order.txt** and is formatted like:

	First chapter
		first_chapter
	Second chapter
		second_chapter
	...
	
and so on. The top level names (e.g. "First chapter") will determine how the chapter names are displayed in the navigation bar. The indented level (e.g. "first_chapter") is the name of the subdirectory (within the **chapters** dir of this repository) that contains the chapter information for this chapter. The subdirs names will not be displayed anywhere, so do yourself a favor and avoid any whitespace.

Make sure each chapter has a subdir in **chapters**, and within each subdir make sure there is a markdown file named **chapter.md**. Edit this file to change the content of any chapter. 

A couple of things to note about editing the **chapter.md** files:

* H1 and H2 headings (i.e. # and ##, respectively) will appear as nested links in the navigation bar whenever this chapter is active. The H2 heading links in the nav bar will even automatically update as the user scrolls down the page.
* You can place images inline, just make sure that a copy of the image gets placed in an **images** subdirectory, within the chapter subdirectory. In other words, if your markdown file references an image called "myImage.jpg", structure the directories like:  

```
/chapters/
	chapter_1/
		chapter.md
		images/
			myImage.jpg
```	


## Deploying website
The website can be created by calling the python script *buildWebsite.py* that is found in the **scripts** directory. This script will take the content of the **chapters** directory, translate it to HTML, and store the output in the **docs** directory. 

Once created, commit and push the changes to the pyneal-docs remote repository on github. The repo is set up to read whatever is in the **docs** dir in the repo, and host it as a static website at:

**https://jeffmacinnes.github.io/pyneal-docs/**


---
This documentation site is modeled off of, and built stealing tools from, the wonderful [OpenFrameworks Book](https://github.com/openframeworks/ofBook)