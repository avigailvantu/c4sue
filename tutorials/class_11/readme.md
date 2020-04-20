Because some of you had issues working with geopandas, here is some info which I'm hopping could be helpful with running geopandas and all other packages for this class.

A. First of all, if you haven't already, go to the GeoPandas Istallation page: https://geopandas.org/install.html
B. For windows users: you may be facing some additional issues. This URL should be helpful in walking you through some ways to overcome these issues: https://geoffboeing.com/2014/09/using-geopandas-windows/  
C. Another way to be able to run Geopandas in case you are still facing issues you could run your Jupyter notebooks from a virtual environment. In a nutshell, a virtual environment is an isolated location on your computer. In the case of working with Python, virtual environments can run your script on s separate Python. Because issues with GeoPandas often are related to dependencies (one package requires having other packages and exact versions of them) working on a virtual environment solves this problem.
* Note: For many of you who are already able to run GeoPandas on your local machine (laptop)--you do not need to set up your venv. This is only for those who weren't able to run last week's class.

## Here are the steps for setting-up your virtual environment:
1. First go to your command line, in mach this is the "Terminal" app, which pretty much is a black (or white) window in which you can communicate with the computer directly. Note that my instructions are inly for mac and Linux computers. For windows the commands should be a little different.

2. Once you are in the Terminal, you will need to navigate into the folder where you want to crate the virtual environment. For example:

 `cd Documents/c4sue/class_11`

 Tab is very helpful in completing the names. For example: if you type Doc and then type Tab, it should complete it to Documents (assuming a folder named that way is inside the folder you are in).  
 You will know you are in the folder you want to be if the command line name changes. For me it looks like this:

 `Avigails-MBP:class_11 avigailvantu$`

 So I know I'm inside the class 11 folder

 Important: plz make sure the requirments.txt file I posted on Github is there!


3. We are finally ready to create a virtual environment. Basically, all you need to so is to specify you want a Python virtual environment, and the name you want to name it (in my example the name of that environment is : c4sue_venv )


`python3 -m venv c4sue_venv`

Now your environment exists on your computer!

Your command line should reflect it, mine starts like this:

`(c4sue_venv) (base) Avigails-MBP:class_11 avigailvantu$``

* Note that this is not a conda environment so you will need to write `pip install <package_name>` in case you want to download something (and not conda install). Let's not worry about that for now.
4. You can now activate your newly created virtual environment. Type this into your command line:  

```
. c4sue_venv/bin/activate


```
5. Make sure the requirments.txt file is in the folder (not inside the environment, just inside the parent folder).

Now install the requirments.txt file. This will make sure that your virtual environment has the same packages and versions as me, so you can ensure runing the notebooks.

Run the following command:

`pip install -r requirements.txt`

* give your computer a few minutes to run-- it will be downloading a bunch of packages to your computer so: be patient.  

6. that's it! now you can open Jupyter notebook by runing this command:

`ipython notebook`
7. In case you want to deactivate your environment you can always do so typing: `deactivate`

8. Now that you set up your environment, future use is easy: every time you want to run your Jupyter Notebook you will need to:
a.  navigate to the folder (step 2)
b. activate your virtual environment (step 4)
