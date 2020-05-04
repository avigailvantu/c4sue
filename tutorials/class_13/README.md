# Data Workflow With Jupyter

As we approach the end of the class I imagine you are working hard on your final projects. Working in groups is hopefully productive for your group as you can divide workload between team members.


Having said that, if not done right, working on a data project with other people can lead to messy work and create additional time consumed on figuring out each others work. There is no magic solutions to keep your workflow organized, but there are a few tools and advices that can help make the best out of your collaborative work.

This repo is an *example* for how you can divide work and keep track of each other's work. The structure I recommend consists of both horizontal and vertical work. These approaches can be used for group or individual projects and can be generalized to fit many subjects.

Note that some projects can be managed using only one big notebook. However, in many cases when the analysis scales up one script can be messy and require running all cells to only compute a simple thing. If you have multiple analyses this method will most likely not work for you.

## Creating a data workflow using Jupyter Notebook for designated purposes.
![alt text][https://github.com/avigailvantu/c4sue/blob/master/tutorials/class_13/workflow_jupyter.jpg]

### Project readme

It is a best practice to create a new project repo generating a readme file. In data projects this file can specify dependencies, data sources and a general description of the project. In addition, you can add any visual aid and explanation to help your future self and your team members understand the workflow.

### Horizontal:
Most projects involve multiple datasets, each needs different initial exploration and cleaning (e.g. remove columns, rename, remove nans and outliers). Having one jupyter for each data source makes it easy to change things, update data, and test on smaller section of the data, if needed.

## Vertical:
This aspect acknowledges that the different steps of the project are intertwined. Cleaning data is done for the purpose of visualizing it etc. That is why most projects can be worked using a funnel structure. Usually, each step will require less notebooks than the previous step.

## How to divide work between team members:

Remember all these are recommendations. You *do not have* to follow each and every one of these steps (or any!). If you do choose to use this structure I recommend dividing work between team members either horizontally OR vertically.

1. Approach 1: In this sense, if you decide to divide work horizontally, each member could be responsible of acquiring, importing, reading cleaning, and understanding the structure and format of one dataset. Then, going into the next step of data merging, analysis and data viz there could be a collaboration between multiple members.

2. Approach 2: you could also divide the work vertically. In this case you will each work on one step of the project. One person will be acquiring and cleaning, another person will merge, visualize etc..

By all means, there is no perfect method. No matter which one you end up choosing you will need to be strict about keeping the readme.md up-to-date with as much info as possible. For best results, the readme is a file should have all team members working on. My advice is: no matter which approach you decide to go with make sure to be coherent, as organized as possible and a good communicator.

This repo includes *example* notebooks for a methods involving 3 steps:

1. cleaning_exploration(1_1).ipynb
2. merging_descriptive(2_1).ipynb
3. viz 3_1.ipynb

These represent the vertical structure. In reality each step can have more than one notebook.
