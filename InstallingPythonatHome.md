# Installing Python at Home #

---

You can easily set up Python on your home computer. First navigate to the [Python Downloads Website](http://www.python.org/download/) and download the latest version (> 2.5.1) in a format suitable to you, depending on whether you use Windows or Unix. For Windows users, select the format indicated in the diagram. After selecting this version, you may need to select your processor type. For most people this will be x86. The .msi file will be around 11MB.

http://pulp-or.googlecode.com/svn/wiki/PythonDownloadAr.PNG


Once the file is downloaded it can be installed on your computer and shortcuts will be made in Start > Programs > Python 2.5. The useful installed components include:


  * IDLE - The most simple Python GUI (Graphic User Interface). Python files can be written in this GUI and as you type, the text is higlighted automatically in different colours for improved readability.
  * Python (Command Line) - The command line for Python. Can be useful to test small segments of code.
  * Python Manuals - Extensive Python Documentation including a Beginners Guide to Programming Tutorial. There are many good guides to programming in Python which will be linked to in the next section on [Basic Python Coding](http://130.216.209.237/engsci392/pulp/BasicPythonCoding).

http://pulp-or.googlecode.com/svn/wiki/StartBarPython.PNG

For your coding in this course, you will not actually need an advanced Python Graphic User Interface, however the recommended development environment for your Python code is Eclipse (www.eclipse.org). This is primarily used for Java programming but with the PyDev Plug-in, it can be used very effectively for Python.

It is your choice in this course whether to use IDLE (comes with Python) or Eclipse with PyDev for creating your .py (Python Extension) files. As a Development Environement, IDLE is similar in layout to MATLAB and Eclipse is similar in layout to Visual Studio.


## Using IDLE ##

---

The Python Shell can be opened through the Start Menu. In the Python Shell, there is a command line which can be used for testing code. "File > New Window" will open a new empty Python code file where you can write your code and save it as a .py extension to be recognised. Writing .py is very important (as shown below).

http://pulp-or.googlecode.com/svn/wiki/IDLEShell.PNG http://pulp-or.googlecode.com/svn/wiki/SavingIDLE.PNG


## Using Eclipse with PyDev ##

---

This must be downloaded from the [Eclipse Website](http://www.eclipse.org/downloads/). Download the latest version of Eclipse Classic (we will use 3.3.1.1) from any of the mirror sites listed after following the link. Once downloaded, it can be easily extracted and installed onto your computer.

PyDev can be downloaded from [here](http://sourceforge.net/project/showfiles.php?group_id=85796). Information about the PyDev plug-in can be found on [The PyDev Site](http://pydev.sourceforge.net/).

http://pulp-or.googlecode.com/svn/wiki/EclipseDL.PNG http://pulp-or.googlecode.com/svn/wiki/PyDevDL.PNG

After installing the PyDev plug-in succesfully, the Eclipse IDE should look like:

http://pulp-or.googlecode.com/svn/wiki/PyDev.PNG

A new PyDev project can be created with "File>New>Project" and new files can similarly be created with "File>New>File". It is important to save the files with the .py extension.

Finally, before the code will run, Eclipse needs to be given the link to the Python Interpreter. In the taskbar, follow "Window>Preferences>PyDev>Interpreter-Python" and locate and add Python.exe into the Interpreter box