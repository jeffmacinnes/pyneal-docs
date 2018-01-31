# Pyneal Docs Website
Documentation for Pyneal Real-time fMRI software

To download the software, visit: [Pyneal Repo](https://github.com/jeffmacinnes/pyneal)

To view the docs website, visit: [Pyneal-Docs website](https://jeffmacinnes.github.io/pyneal-docs/)


### Editing content
All content is stored in markdown files that are saved in the **content** dir. Edit these files to edit the documentation

The table of contents for the documentation is set within `mkdocs.yml` file in the root directory. Edit the section called `pages:` to change the page order and page nesting.


### Building Website
The static html of the site is built using [mkdocs](http://www.mkdocs.org/). In order to see how your changes will appear in html, you need to install the mkdocs tool, as well as the theme files:

>pip install mkdocs

>pip install mkdocs-windmill


To test out your edits to the site without having to build, open up a terminal session, navigate to the root dir of the repo and type:

>mkdocs serve

This will start a local webserver and render your page. The URL will be provided in the output (probably `127.0.0.1:8000`)

Once you're happy with the changes, build the complete site by typing:

>mkdocs build

 The **mkdocs.yml** file is customized so that the built files will appear in the **docs** dir. This way, everything can be pushed to the remote github repository, which is set up to host a site based on the contents of the **docs** dir.


Once the site is build, next commit & push the changes to github, and the site will be live within a few minutes afterward
