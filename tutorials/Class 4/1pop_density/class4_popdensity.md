## Class 4 C4SUE: NYC's Population Density
As we learned, normalizing the data can be crucial when presenting spatial data. This helps us present the data in a more accurate way, while accounting for area/number of housing units/number of people depending on the data and our unit of analysis. In this tutorial we will learn how to display population in geographical data. We did so for your homework last week, so the beginning will be more a refresher. We will display population counts for each zip codes in NYC (not by NTA's like we did for the homework). Then, we will apply what we learned in class and standardize the data to account for the area of each zip code. Eventually we will have the population density rather than pure population count.

Luckily, the zip code data (from NYC Open Data) already comes with the exact population counts. That means that we do not need to join tables and attributes in order to create this map!

Note about this and next tutorials: with time I will try to give less direct instructions on how to do certain things that we did in previous assignments or in class. This is to slowly give you the confidence and know-how. In cases are you asked to conduct a certain analysis but don't see the detailed instructions for it you will need to come up with it yourself. If you can't remember how to do so, you can go back to class materials, homework or look online.

## I. Population in NYC, by Zip Code

### 1. Data prep and acquisition:
We will need a .shp file of all Zip Codes in NYC. The Data is from NYC Open Data platform. The data can be accessed here: [alt text](https://data.cityofnewyork.us/Business/Zip-Code-Boundaries/i8iw-xf4u))

### 2. Load the data to qgis. Note this is a shapefile.

You should now have all Zip Codes for NYC displayed on your map

### 3. Display population Count for NYC's Zip Codes
First, we'd like to display the populations as absolute numbers. Similar to assignment 1, we will create a choropleth map of the number of people per zip code.

First, let's open the attribute table and view the data.
Now go to the layer symbology menu. Right click the layer to do so.

* In the top dropdown: choose: Graduated
* In the column name: choose POPULATION
* Click: Classify
* In mode: choose Natural Breaks

Choose a color ramp of your choice. I recommend choosing the same color ramp for both this map and the population density one. That would enable us to compare between both.  

Note about natural breaks on QGIS: this mode is an algorithm that looks for natural groups in the data which classifies according to the chosen column. It displays the data according to classes when the goal is to find the maximum variance b/w all groups.

4. Review map: ![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/population_map.png)


## II. Population Density in NYC, by Zip Code

As mentioned above, we want to look into displaying the data in a more meaningful way. Meaning, not solely display population, but accounting for area. As Zip Codes are shapes that differ a lot in size, it is common to standardize it. As we learned in class there are many ways to do so. Today we will standardize using the area of the zip code. This makes sense when attempting to understand population densities, which is the number of people per unit area.

In a more broad note, population densities enable us to compare between areas'. The number tells us how many people live within the unit (mile/kilometer). According to the census, NYC on average, has 28K people per sq mile, which is a little more than 3 times the population density of LA. Keep in mind that these numbers are very tricky to compare between large areas (e.g. cities, states) because these areas are likely to vary within themselves. For these reasons we'd usually want to have small area calculation of population densities.     

1. Duplicate the zip code layer:
* Right click the layer--Duplicate layer
* Rename the new layer. right click--rename layer--'population_density'
2. Now that we have a new layer for the population density we can hide the population layer for the time being. This will let us focus in the new map.
3. Now go examine the new layer and make sure it's displayed.
4. Open the layer attribute table and click on the field calculator icon in the right side of the menu bar
5. In the field calculator, create a new column that would calculate the population density and create a new column with the info.
As the data comes with both the population count and the area for each Zip Code we will need the new column to be a calculation of both columns, so that for every zip code:
* What do I mean when I say we're going to calculate Population Density? That's the formula we will apply:
 - Population Density(for zip code i) = (population(i)/area(i))
Because the area units are large, we will multiply the result by 1000, so that our final population density formula will look like that: Population Density(for zip code i) = (population(i)/area(i))* 1000

Your field calculator should look something like this:

* ![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/field_calc.png)

 Check out the column name: pop_dens (you can choose your own). Click OK to generate this new column.
6. We now have a new column named: pop_dens. We want to symbolize this column, similar to how we did it for the population layer in the first section so we can compare between both.
* Follow step 3 in section I, but use the population density column instead of the population.
* To submit this task, export these two maps: one for population and one for population density.
How does both maps look to you? How does the population density map compares to the first map? As a NYC resident: which one of the maps aligns better with your perception of the city?
Write one paragraph about your findings and your conclusion from this exercise.
