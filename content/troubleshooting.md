# troubleshooting


## problems installing kivy

Some users have reported difficulty installing the `kivy` dependency for **Pyneal**. Kivy is used to create the Pyneal Setup and createMask GUIs, and has its own set of dependencies. If these dependencies don't exist (or they do, but are incompatible versions), using `pip` to install Kivy can fail. 

Please see the [**detailed Kivy installation instructions**](https://kivy.org/docs/installation/installation-osx.html#using-homebrew-with-pip) for help. 

Make sure to specify the development version of kivy in the 2nd step under **Using Homebrew with pip**: `pip install https://github.com/kivy/kivy/archive/master.zip`