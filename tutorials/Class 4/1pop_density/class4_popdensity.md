## Class 4 C4SUE: NYC's Population Density
As we learned, normalizing the data can be crucial when presenting spatial data. This helps us present the data in a more accurate way, while accounting for area/number of housing units/number of people depending on the data and our unit of analysis. In this tutorial we will learn how to display population in geographical data. We did so for your homework last week, so the beginning will be more a refresher. We will display population counts for each zip codes in NYC (not by NTA's like we did for the homework). Then, we will apply what we learned in class and standardize the data to account for the area of each zip code. Eventually we will have the population density rather than pure population count.

Not that the zip code data (from NYC Open Data) comes with the exact population counts. However, these counts are a little outdated (and most importantly do not really come with a data dictionary). We will be merging the zip code level data with American Community Service (ACS) population estimates from 2017. I downloaded the data from the Census FactFinder.

Note about this tutorials and the next ones: this time I will try to provide less instructions on how to do certain things. That will be based on previous assignments or in class work. This is to slowly give you the confidence and know-how of working on you projects and figuring out some things on QGIS. In cases where you asked to conduct a certain analysis but don't see the detailed instructions on how to do so you will need to come up with it yourself. If you can't remember how to do so, you can go back to previous class materials, homework, or look it up online.

## I. Load data
### Zip Code Polygons
### 1. Data prep and acquisition:
We will need a .shp file of all Zip Codes in NYC. The Data is from NYC Open Data platform. The data can be accessed here: [alt text](https://data.cityofnewyork.us/Business/Zip-Code-Boundaries/i8iw-xf4u))

### 2. Load the data to qgis. Note this is a shapefile.

You should now have all Zip Codes for NYC displayed on your map.

### Population data from the ACS

### 3. Load the CSV with NY state (can be accessed on NYU Classes)
This is a CSV file without geographic attributes. We do have the 5-digit zip codes in the zipcode column. Similar to our first assignment we can join tables to have the ACS population count in a geographical format.

* To do so, let's load to QGIS as a delimited text layer.

* Before we join tables, we'd want to change the population column into an integer. We'll use the toreal() function again.

* create a new column in the ACS CSV data and name it: population_new
First, we'd like to display the populations as absolute numbers.




* We can now join both layers. To do so, go to the zipcode boundaries layer and join the ACS CSV table.

* Right click the layer and make sure the merge looks fine.

4. Visualize population

Similar to assignment 1, we will create a choropleth map of the number of people per zip code.


* In the top dropdown: choose: Graduated
* In the column name: choose <your merged population column>
* Click: Classify
* In mode: choose quantiles (5 groups)

Choose a color ramp of your choice. I recommend choosing the same color ramp for both this map and the population density one. That would enable us to compare between both more easily.  

Note about quantiles: this methods divided the data into a frequency distribution which results into equal groups. We can set the number of groups (doesn't have to be 4). We'll use a 5 groups quantile.


* Review map: ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/1pop_density/population_new.png)


## II. Population Density in NYC, by Zip Code

As mentioned above, we want to look into displaying the data in a more *meaningful* way. Meaning, not solely display population, but *also* accounting for the area of each zipcode. As Zip Codes are shapes that differ a lot in size, it is common to standardize data displayed in this unit. The same goes for neighborhoods and other units too. As we learned in class there are many ways to do so. Today we will standardize using the *area* of the zip code. This makes sense when attempting to understand population densities, which is the number of people per unit area.

In a more broad note, population densities enable comparing between areas. The number tells us how many people live within the unit (mile/kilometer  etc). According to the census, NYC on average, has 28K people per sq mile, which is a little more than 3 times the population density of LA. Keep in mind that these numbers are very tricky to compare between large areas (e.g. cities, states). This is because these areas are likely to vary within themselves. For these reasons we'd usually want to have small area calculation of population densities.     

1. Duplicate the zip code layer:
* Right click the layer--Duplicate layer
* Rename the new layer. right click--rename layer--'population_density'
* make sure to reset the classification. This will make things less confusion for us along the way. To reset, go to the layer symbology and change the style to "single symbol".  
2. Now that we have a new layer for the population density we can hide the population layer for the time being. This will let us focus in the new map.
3. Examine the new layer (population density) and make sure it's displayed.
4. Open the layer attribute table and click on the field calculator icon in the right side of the menu bar
5. In the field calculator, create a new column that would calculate the population density and create a new column with the info.
We'll need to take the ACS population column and divide it by the "area" column that is a given in the boundaries data.
* What do we mean when we say we're going to calculate Population Density? That's the formula we will apply:
 - Population Density(for zip code i) = (population(i)/area(i))
Because the area units are large, we will multiply the result by 100000, so that our final population density formula will look like that: Population Density(for zip code i) = (population(i)/area(i))* 100000. Note that we do so only for the ease of understanding and visualizing the data.

Your field calculator should look something like this:

* ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/1pop_density/field_calc.png)

Click OK to generate this new column.
6. We now have a new column named: pop_dens. We want to symbolize this column, similar to how we did for the population layer in the first section. This will allow us to compare between both population and population density.
* Follow step 3 in section I, but use the population density column instead of the population column.
* To submit this task, export these two maps: one for population and one for population density.
How does the population density map compares to the population map? As a NYC resident: which one of the maps aligns better with your perception of the city?
Write one paragraph about your findings and your conclusion from this exercise.
