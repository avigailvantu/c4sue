# Class 5: CARTO tutorial

Written for the Computing for SUE class @nyu, Spring 2020.
avigailvantu@nyu.edu

### 1. Create an account on CARTO:
NYU provides free access to CARTO. Everyone part of the NYU community can create an account through [this URL](https://nyu.carto.com/signup) Use your NYU email and PW to log-in. For more information about eligibility and other CARTO tutorials go [here](https://www.nyu.edu/life/information-technology/getting-started/software/carto.html)

### 2. Data: Housing Maintenance Code Violations
Today we will be working with the housing violations data, that comes from the Housing Preservation Department. This a comprehensive data of all housing violations recorded in NYC. Violations are issued either by complaint of a tenant or by an inspector conducting regular inspections in NYC’s buildings. Housing violations are labeled by the inspector with one of theses classes:
- Class A: are Non-Hazardous violations that need to be corrected within 90 days of filing the violation
- Class B: are Hazardous violations that need to be corrected within 30 days (with some exception for immediate correction required)
- Class C: for Immediately Hazardous violations. These violations are required to be taken care of by landlords within 24 hours. C class violation are usually related to hot water/heat/lead/window guards.

#### Access the data on the Open Data platform.

For this exercise we only want to work with Class C violations. To do so, we’ll go to the [open data website](https://data.cityofnewyork.us/Housing-Development/Housing-Maintenance-Code-Violations/wvxf-dwi5/data)
We’ll then apply these filters:

1. Class is : “C”
2. Brough is : “BROOKLYN”
3. Inspection date is between: 01/01/2019 and 12/31/2019
4. This should result in 61,294 results

  ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/filter1.png)
  ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/filter2.png)

5.  Export as “CSV”

### 3. Load the violations data on CARTO:    
- Go to “Dataset” —> "connect dataset" and upload the file from your computer and then finalize the upload clicking “Upload dataset”
- Give it a few minutes to “connect” as CARTO loads your data.
- Finally, when CARTO is done loading the date it will display it as a table
- CARTO should be able to identify the geometric column in the data to visualize.
- Also note that CARTO displays the columns in A-Z order.

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/carto_data.png)

- Click on “Create Map” on the bottom right to view the data on a map
- Once you do so all points should appear on your map
- Remember, we are looking into all *sever* violations in *Brooklyn*. So our map view would reflect only the sever Brooklyn violations.
- Similar to QGIS CARTO can accommodate multiple datasets and layers. In the main interface you should be able to view all layers. At the moment we only have one that would appear as the CSV name.
- To edit and symbolize double click on the layer

### 4. The components of CARTO’s interface

- You should now see four tabs on the side menu: 1. Data, 2. Analysis, 3. Style, 4. Pop-up and  5. Legend

Let’s go through them one by one before symbolizing this layer
  *  “Data” displays basic information about the data and each column. Among other information, CARTO will tell you the number of NULL values.
  * “Analysis” is a service that will do geocoding and other data wrangling and manipulations for you. Many of the tools in this tab are similar to QGIS’ tools.
  * The “Style” tab will allow us to visualize and symbolize the data (similar to the symbology tab in the QGIS’ properties). Among other uses, you can control the size and color of the points or polygon layer.
  * “Pop-up” allows you to decide which features will be visible when hovering over them on a webpage
  * Finally “Legend” will display the legend, again similar to QGIS  

Here’s how my initial map looks like:

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/initialmap.png)

#### Aggregation style 01:
  * Because there are so many points all around the borough, it is hard to draw any conclusion on trends solely by looking at the data as is.
  * To be able to view how the hazardous (C) housing violations are distributed in the city we can try different methods
  * First, aggregate the data by squares/hexbins. Doing so we see that east-north Brooklyn has much less violations than south and west Brooklyn. That is surely an interesting fact. But if we think about it totally makes sense and aligns with what we learned about standardization of the the data. These are all less populations dense areas.

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/squares_agg.png)

#### Aggregation style 02:
  * Another way to view how the data distributes is by displaying a heat-map. Heat-maps are a technique to color code the data in order to represent different values in the data. Usually it would display clusters and less concentrated data.
  * CARTO’s default displays the points size as 45 which is way too big for us, since we have so many violations! By moving the curser to the left, reduce the point size to 6 - 10. This size will enable you to see the concentration of points in space while still identifying clusters.

### 5. SQL for CARTO:
- CARTO allows manipulation of the data using programming like SQL. By writing very basic codes we can filter and merge and choose exactly what is it that we want to display.  
- Let’s say we only want to display one specific area in terms of housing violations. We can filter through the NTA column using a simple SQL code
- As you will soon see, SQL is a pretty simple language. It is also a very important skill to have to work in the data science field.
- To filter NTA’s, we will first use the SELECT and FROM commands.
- SELECT specifies which columns we will work with when * means we query all columns in the data.
- FROM specifies the dataset we will be working with.


#### Display only certain violations using conditions
1. In the DATA tab: switch from "values" to "SQL" mode. This will open a SQL script page where we will be able to write our commands. We will see the changes implemented right away on the map.
3. First we will choose all data and specify we want to query the housing violations data:

```sql
 SELECT * FROM <YOUR_USER_NAME>.housing_maintenance_code_violations
```


This command on its own is not going to change our data display because we already had the entire 			data displayed
4. Now let’s choose only Flatbush, we’ll use the WHERE command for that:

``` sql
WHERE NTA = 'Flatbush'
```
5. to add more neighborhoods we will use the “OR” command and add:

```SQL
OR NTA = 'Crown Heights South'
```
to our code

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/wintertime.png)

6. Because we are looking into the hazardous housing violations it would be interesting to display the violations that were recorded in the winter months. For the propose of this exercise we will assume that January through end of March are these months that are the most dangerous in term of lack in heat or hot water. To only view the winter months violations we can filter using the Inspections date column:

```SQL
 AND InspectionDate  BETWEEN  '01/01/2019' and '04/01/2019' . Add this command to your SQL script: AND InspectionDate  BETWEEN  '01/01/2019' and '04/01/2019'
 ```

7. NOTE: to apply this filter to all chosen neighborhoods be sure to include the NTA commands inside parenthesis.
8. We see that the most class C violations do actually happen during the coldest winter months.

![alt text](/https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/wintertime.png)

** notice the difference b/w both query results.

### 6. Style your SQL query results. You are free to use the method and colors that work best, in your opinion.

  - I used the squares aggregation method in style, with pink color-graduated palette
  -  I also zoomed-in into these two areas so they appear at the center of the map (when publishing this map the zoom level we set will be maintained).
  - I also changed the map basemap. If you want to do so too, go to the main menu, where all layers are displayed. the basemap will be one of the layers. My default map is Voyager.
  - I changed it to “Positron” to have a gray backdrop to my map.
  - I also added a legend
![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/mapfinal.png)

### 7.Publish your map:
  1. CARTO is different than QGIS since it is an interactive map tool that allows us to publish maps, on top of downloading them as an image. This means, we can easily embed a map on a web interface, or just share a URL of it to stack-holders.
  2. To publish this map we need to go to the layers view
  3. Then click on “Publish” on the bottom right side of the map.

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/publish.png)

  4. After clicking on publish, you will be directed to a webpage where you will need to choose between "share with colleagues" and "publish".
  5. Before finalizing this, you will need to make the map public (NYU default maps are private).
  6. Go back to the layers page and click on the orange private on the top left
  7. when the dropdown opens, change from Private to Public

  ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/CARTO/private_public.png)

  6. Finally we can publish!
  7. Click on publish again. This time when you go to the Publish tab you can access two options for publishing your map: embed or get a link.
  8. copy the address in the "Get a link" section to your browser.



[That's my final map!]( https://nyu.carto.com/u/avigailvantu/builder/b9a5d8cf-70c3-40bd-8fff-a6974964c089/embed?state=%7B%22map%22%3A%7B%22ne%22%3A%5B40.591665655665636%2C-74.07051086425783%5D%2C%22sw%22%3A%5B40.69235321394895%2C-73.83567810058595%5D%2C%22center%22%3A%5B40.642028420083335%2C-73.95309448242189%5D%2C%22zoom%22%3A13%7D%7D)

How's yours looking like?

### 8. Deliverable:
Please submit your CARTO map as URL on NYU Classes.
