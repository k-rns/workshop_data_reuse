---
title: "Set up "
teaching: 10
exercises: 0
questions:
- "How to install Python Anaconda"
- "Create an environment called "erddap"
- "Install the following libraries in your conda environment: pandas erddapy urllib3 "
---

{% include links.md %}

# Python - Anaconda

Anaconda is a Python distribution platform. It comes with the most popular data science libraries and their dependencies pre-installed, and a package manager to assist with installing additional libraries that weren’t pre-installed.

## Installing Anaconda

#### Windows

1. Open https://www.anaconda.com/products/individual#download-section with your web browser.
2. Download the Anaconda for Windows installer with Python 3. (If you are not sure which version to choose, you probably want the  64-bit Graphical Installer *Anaconda3-...-Windows-x86_64.exe*)
3. Install Python 3 by running the Anaconda Installer, using all of the defaults for installation *except* make sure to check **Add Anaconda to my PATH environment variable**.

#### MacOS3

1. Open https://www.anaconda.com/products/individual#download-section with your web browser.
2. Download the Anaconda Installer with Python 3 for macOS (you can either use the Graphical or the Command Line Installer).
3. Install Python 3 by running the Anaconda Installer using all of the defaults for installation.

## Conda Environment and Packages

**Install method 1: Make a new environment and launch jupyter notebooks using the new environment.**

This method is more fail-safe than method 2.   As shown in the  steps below you have to use a command line (Anaconda Prompt(win)  Terminal(Mac/Linux) to launch jupyter notebook, not the graphical  Anaconda Navigator.

**Steps**

1. Open Anaconda Prompt (Windows) or Terminal(Mac/Linux)

2. Enter the following command to create a new environment called "pyaos-lesson"

   ```
   conda create -n pyaos-lesson -c conda-forge jupyter xarray netCDF4 cartopy cmocean cmdline_provenance plotnine
   ```

3. You will be asked if you would like to install the packages after they are found.  Press Yes (y).

   You should see messages for Preparing, Verifying, and Executing the "transaction" and end with a line that says "done"

4. Enter the new environment you created.  After this command you should see "(pyaos-lesson)" at the start of your line.

   ```
   conda activate pyaos-lesson
   ```

5. Launch the jupyter notebook with the following command. A new browser window should pop up with jupyter notebook in it.

   ```
   jupyter notebook
   ```

6. Test your installs worked. See "Testing Your Installs" section Below.

**Install Method 2: Using the base environment**

This method may be quite slow for some people and you may encounter more issues than method 1. But if you have completed your installs with this method and your test works then you are all set for the worksohp  (See "Testing Your Installs" section Below).

**Steps**

1. Enter `conda activate base` and press enter to  execute. This makes sure you are in your base environment. It won't hurt anything if you already are in base and run it anyway.  You should see  "(base)" at the beginning of your line.	 		

2. Run the following commands one at a time.  It may take a few  minutes to respond during this process.  You will be asked if you would  like to install the packages after they are found.  Press Yes (y).		

   `conda install jupyter xarray netCDF4 cartopy`

   `conda install -c conda-forge cmocean cmdline_provenance plotnine`

   You should see messages for Preparing, Verifying, and Executing the "transaction" and end with a line that says "done"

3. Launch the jupyter nootebook using either Anaconda Navigator or  command line using Anaconda Prompt(Windows) or Terminal(Mac/Linux).

4. Test your installs worked. See "Testing Your Installs" section Below.

## Testing the installs

#### Jupyter Notebook

*if you have just followed the instructions to install packages and  test them, you already have launched jupyter notebook and can use that.  You can follow these instructions if you don't already have a notebook  running.

**Steps**

1.  Open an Anaconda Prompt(Win) or Terminal(Mac/Linux). 

2. Enter the environment wish to use.  After this command you should  see the environment name "(pyaos-lesson)"  or "base" at the start of  your line.

   If you installed your packages using method 1:

   ```
   conda activate pyaos-lesson
   ```

   If you installed your packages using method 2:

   ```
   conda activate base
   ```

3. Launch the jupyter notebook with the following command. A new browser window should pop up right into your notebook.

   ```
   jupyter notebook
   ```

   A browser window will open with your notebook in it. If you close  the page and need to get back to it, you can copy and paste the link  shown in your Anaconda Prompt/Terminal.  Or you can try the default  address	http://localhost:8888/. 		

For a brief introduction to Jupyter Notebooks, please consult our [Introduction to Jupyter Notebooks](https://datacarpentry.org/python-ecology-lesson/jupyter_notebooks/) page. If you installed your required packages using [method 2](https://k-rns.github.io/2020-10-26-WHOI-Data/#install-method-2), you can also launch jupyter notebook using the Anaconda Navigator (instead of command line) as shown in that lesson.		 







install anaconda



installing packages in environment

* create environment erddap install python 3.9



Opening Jupyter Notebook in the environment you just installed. 

libraries:

 * urllib.request: ```conda install -c anaconda urllib3```
 * pandas: ```conda install -c anaconda pandas```
 * erddapy: ```conda install -c conda-forge erddapy  ```

```conda install 
conda install -c anaconda urllib3
```

``` conda install 
conda install -c conda-forge pandas erddapy
```

![image-20211019053913314](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211019053913314.png)

![image-20211019054305817](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211019054305817.png)

# Open Jupyter notebook 

Make sure that you open Jupyter notebook at the same location you want your data to reside.



STEP 1. Start Jupyter Notebook

Anaconda prompt -> Direct to location -> Start Jupyter Notebook 

![image-20211008061129812](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211008061129812.png)



STEP 2: Open new notebook in the location

![image-20211008061300970](C:\Users\ksoenen\AppData\Roaming\Typora\typora-user-images\image-20211008061300970.png)

Reminder [Python Notebook Basics](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

### Edit mode

Edit mode is indicated by a green cell border and a prompt showing in the editor area:

![Jupyter cell with green border](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/images/edit_mode.png)

When a cell is in edit mode, you can type into the cell, like a normal text editor.

Enter edit mode by pressing `Enter` or using the mouse to click on a cell's editor area.

### Command mode

Command mode is indicated by a grey cell border with a blue left margin:

![Jupyter cell with blue & grey border](https://nbviewer.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/images/command_mode.png)

The most important keyboard shortcuts are `Enter`, which enters edit mode, and `Esc`, which enters command mode.

In edit mode, most of the keyboard is dedicated to typing into the  cell's editor. Thus, in edit mode there are relatively few shortcuts.   In command mode, the entire keyboard is available for shortcuts, so  there are many more.  The `Help`->`Keyboard Shortcuts` dialog lists the available shortcuts.

We recommend learning the command mode shortcuts in the following rough order:

1. Basic navigation: `enter`, `shift-enter`, `up/k`, `down/j`
2. Saving the notebook: `s`
3. Change Cell types: `y`, `m`, `1-6`, `t`
4. Cell creation: `a`, `b`
5. Cell editing: `x`, `c`, `v`, `d`, `z`
6. Kernel operations: `i`, `0` (press twice)

