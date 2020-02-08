# NYC NTA Population Count

In this assignment we will visualize NYC's NTA's. NTA stands for Neighborhood Tabulation Areas and are a geographical entity for neighborhoods used mainly by the [NYC Dept. of City Planning](https://www1.nyc.gov/site/planning/data-maps/open-data/dwn-nynta.page).

NTA's represent neighborhoods in NYC and they are drawn so that their size is minimum 15K people per NTA. Therefore, in some cases a few neighborhoods were merged together to form one NTA. For example, NTA BK38 represents DUMBO, Vinegar Hill, Downtown Brooklyn and Boerum Hill which organically would count as 4 different neighborhoods.


### Datasets:
1. Shapefile of NYC NTA. The data comes as polygons and can be downloaded from [NYC Open Data](https://data.cityofnewyork.us/City-Government/NTA-map/d3qk-pfyz) or from this assignment Github repo.
2. CSV file with population per NTA from [NYC Open Data](https://data.cityofnewyork.us/City-Government/New-York-City-Population-By-Neighborhood-Tabulatio/swpk-hqdp/data) is a 2010 census population count per NTA (or from this assignment Github repo).

### Load data:

Download both (1) and (2) and load them both into a new QGIS project:

* For (1): Layer --> Add Layer --> Add vector layer
* For (2): Layer --> Add Layer --> Add Delimited Text Layer--> Choose "no geometry attribute"

Both the NTA Shapefile and the population per NTA should be on your layers qgis panel.


### Joining tables:

As you may have noticed dataset (1) is provided in a spatial and easy to read format (for Qgis in any case). The population data on the other hand, is a CSV file without any immediately mappable geographical attribute. We learned that CSVs are very easy to work with. Which is usually true! Our problem here is that the data is not geographically represented. Meaning, we don't have (X,Y) coordinates in the data.

Luckily, the NTA data comes as Shapefile which is about to make our lives pretty easy. *All* we need to do is to find a column that is a unique identifier and is identical between both datasets. Then, we can merge both tables and have the population data in a geographic form. QGIS allows us to do so quit easily.


### Understanding the NTA code:
NTA's each have a unique identifier: two letters and two integers. The letters represent the borough where the NTA is located, and the 2-digits represent a serial number within each given borough. For example, QN25 is the NTA code for Corona in Queens and SI25 is the NTA code for Oakwood-Oakwood Beach. Meaning, integers and letters can be repeated. However, the combination of letters and integers is always unique and is only used to represent one NTA.

Now that we have both data loaded into QGIS, check out both layers attribute tables and confirm you can find the NTA code in ![both layers.](https://github.com/avigailvantu/SUE-Class/blob/master/homework_assignment/NTAcode.png)

#### There are a few things we need to do before we actually join both tables:

### Change data formats:

We want to display the population data in a way that would account for the quantity of people in each NTA and let us compare. To do so we'd need to transform the population data to numerical values.

You can learn the datatype going to the layers properties and scrolling down in the "information" page. In the "Fields" section you can see the datatypes for each and every column.

If you look at the CSV population data, you should be able to see that all columns are of type "String".

QGIS will let us join tables between strings so the NTA code doesn't need to be changed. However, we need to find a way to get the population count in integers and NOT string. This is because the "graduated" symbol only treats numerical data.

One good way to do so is to use the "field calculator" to create a new column.

1. Open the population data attribute table (right click on the layer)
2. Navigate to the field calculator icon and click it ![both layers.](https://github.com/avigailvantu/SUE-Class/blob/master/homework_assignment/field_attr.png)
3. A window will open. Make sure the "create a new field" box is checked.
4. Name the new column: "pop_new"
5. In the input window type: toreal( "Population"). toreal() argument takes the existing population column and creates another column that will have the same values but will be in integer format.

![both layers.](https://github.com/avigailvantu/SUE-Class/blob/master/homework_assignment/calculator.png)

5. Click OK

6. Open the population data attribute table again. You should see a new column named "new_pop", it'll have the exact same values as the Population one (only eyeballing the data would not show the format).

### We are finally ready to join tables!

Now that our data formats align we want to merge both data.
To join tables we'd need to merge the CSV table to the Shapefile.

1. Go to the Shapefile and rename it: NTA
2. Go to the layer's properties and navigate to the "Joins" tab
3. Here you will need to click the + sign to add a new data
4. Choose the population layer in the Join Layer dropdown
5. Join Field and Target Field should both be the unique identifier (NTA code)
6. Click ok

Now both data should be joined. Open the NTA layer attribute table and confirm that the "new_pop" data is there.


### Visualize population by NTA

We're all set to visualize population by NTA. Open the layer properties and navigate to the "symbology" tab. Then you'll need to change the from "single symbol" to "graduated" that would allow us to display the population data as choropleth.

![.](https://github.com/avigailvantu/SUE-Class/blob/master/homework_assignment/symbology.png)

For column: choose the "new_pop" column. Note that the column name will have the joined table name before (starting with "New_York_City_Population"...).

There are a few different ways to slice the data in order to visualize it. For example: pretty breaks, equal interval, quantile, SD.. As we discussed in class we will want to display the data in a meaningful way that would allow us to compare neighborhoods. You can control them through the "Mode" dropdown.

Try out a few of these symbologies. After each choice click "classify" for the categories to be displayed in the main window. Choose one that looks the most suitable for the data, in your opinion.

### Delivery:
Browse the map you created of NYC NTAs by population. Which areas are the most populated per NTA? Which ones are the least populated? Could you think of any issues or biases that we may experience? Export the maps using QGIS Print Layout and submit 1-2 paragraphs with your answer to NYU classes.
