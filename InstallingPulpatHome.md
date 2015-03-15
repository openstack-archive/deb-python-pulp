# Installing PuLP at Home #

PuLP is a free open source software written in Python. It is used to describe optimisation problems as mathematical models. PuLP can then call any of numerous external LP solvers (GLPK, CPLEX, XPRESS etc) to solve this model and finally display the solution. Note that to install PuLP you must first have a working python installation as described in InstallingPython In your course you will solve many mathematical programmes using PuLP. These mathematical programmes will tell you such varied things as:

  * The mix of ingredients to use to provide a nutritious can of cat food whilst minimising costs
  * The price and production quantity for a surfboard shop to maximise profit
  * The number of crates of beer to ship from breweries to pubs to minimise the shipping cost

The old version of PuLP is available on the internet, but an upgraded version of PuLP can be freely obtained from [here](http://code.google.com/p/pulp-or/downloads/list), which is the version you will be using in this course.
Please note that this version of PuLP has not been tested with operating systems other than Microsoft Windows and Ubuntu linux.

## Easy install and pypi installation ##
By far the easiest way to install pulp is through the use of [EasyInstall](http://peak.telecommunity.com/DevCenter/EasyInstall)
  * Install setuptools (including EasyInstall) http://pypi.python.org/pypi/setuptools
  * In  windows
```
c:\> easy_install pulp-or
```
  * In Linux
```
$ sudo easy_install pulp-or
```
  * Then follow the instructions below to test your installation


## Windows Installation ##

  1. Install python (InstallingPythonAtHome)
  1. Extract the PuLP-1.xx.zip folder to a suitable location (such as the desktop - the folder will be no longer required after installation)
  1. Open a command prompt by clicking "Run" in the Start Menu, and type 'cmd' in the window and push enter.
  1. Navigate to the extracted PuLP-1.xx folder with the setup file in it. [this by typing 'cd foldername' at the prompt, where 'cd' stands for current directory and the 'foldername' is the name of the folder to open in the path already listed to the left of the prompt. To return back to a root drive, type 'cd C:\'](Do.md)
  1. Type 'setup.py install' at the command prompt. This will install all the PuLP functions into Python's callable modules.

The PuLP function library is now able to be imported from any python command line! Go to IDLE or PyDev and type
```
from pulp import *
```
to load in the functions. (You need to re-import the functions each time after you close the GUI) PuLP is written in a programming language called Python, and to use PuLP you must write Python code to describe your optimisation problem.

## Linux Installation ##
  1. Extract the PuLP-1.xx.zip folder to a suitable location (such as your home directory - the folder will be no longer required after installation)
  1. Open a command line navigate to the extracted PuLP-1.xx folder with the setup file in it. [this by typing 'cd foldername' at the prompt](Do.md)
  1. Type the following at the command prompt. This will install all the PuLP functions into Python's callable modules.
```
$ sudo ./setup.py install 
```
  1. install a solver for pulp to use either
    * install glpk http://www.gnu.org/software/glpk/ debain based distributions may use the following
```
$ sudo apt-get install glpk
```
  * install cplex (and pay $$)
  * or compile coinMP and pulp from source
    1. checkout pulp and coinMP from google code website
```
$ svn checkout http://pulp-or.googlecode.com/svn/trunk/ pulp-or
```
    1. build coinmp from source (please test the installation first as the included binaries may be appropriate for your system)
```
$ ./configure
$ make
$ make test
$ make install
```
    1. copy the resultant library files to into the pulp directory and install pulp
```
$ cp lib/*.so pulp-or/src/
$ ./setup.py install
```


# Testing your PuLP installation #
To test that that you pulp installation is working correctly please type the following into a python interpreter and note that the output should be similar. The output below is what you would expect if you have not installed any other solvers.

```
>>> import pulp
>>> pulp.pulpTestAll()
Solver pulp.pulp.COIN_MEM unavailable.
Solver pulp.pulp.COIN_CMD unavailable.
* Solver pulp.pulp.COINMP_DLL passed.
Solver pulp.pulp.GLPK_MEM unavailable.
Solver pulp.pulp.GLPK_CMD unavailable.
Solver pulp.pulp.XPRESS unavailable. 
```