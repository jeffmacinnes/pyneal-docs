# Pyneal Docs Website
Documentation for Pyneal Real-time fMRI software

To download the software, visit: [Pyneal Repo](https://github.com/jeffmacinnes/pyneal)

To view the docs website, visit: [Pyneal-Docs website](https://jeffmacinnes.github.io/pyneal-docs/)


### Editing content
All content is stored in markdown files that are saved in the **content** dir. Edit these files to edit the documentation

Edit the **mkdocs.yml** file for updating the page order for navigation on the website

### Building Website
The static html of the site is built using mkdocs. The **mkdocs.yml** file is customized so that the built files will appear in the **docs** dir. This way, everything can be pushed to the remote github repository, which is set up to host a site based on the contents of the **docs** dir. 

To test out your edits to the site without having to build, open up a terminal session, navigate to the root dir of the repo and type:

>mkdocs serve


To build the site, type:

>mkdocs build

After you've built, commit & push the changes to github, and the site will be live shortly thereafter