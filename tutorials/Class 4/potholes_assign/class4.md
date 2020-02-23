## Class 4 QGIS tutorial
### Working with 311 data: Potholes
* Created by Avigail Vantu (avigailvantu@nyu.edu), for the NYU Tandon Computing for Sustainable Environment class , Spring 2020.

The goal of this tutorial is to learn how to work with 311 data and some administrative boundaries. Today, we will count the number of points per census tract.

### Datasets:   
a. 311 Service Requests from 2010 to Present: 311 data is one of NYC’s Open Data most popular datasets.
311 is a phone and online resource in which citizens can report any non-emergency issue.
Along with 511 for traffic related incidents and 911 for emergency incidents, through 311 municipalities can get informed quickly on any of the city's malfunctions in infrastructure as well as noise, parking, and damaged trees (as well as many other categories).
The data is released through the open data platform and provides a detailed documentation of each and every one of 311 complaints in NYC. Along with the category and the agency this complaints belongs to, the data also includes time of the report and the exact address where the complaint was taken.

You access 311 data below. Do not download it yet. We will filter it prior to downloading. This way we will avoid downloading a HUGE dataset.

(https://nycopendata.socrata.com/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9/data  )

b. Bureau of transportation statistics  U.S. Hydrographic features. (https://www.bts.gov/archive/publications/national_transportation_atlas_database/2015/polygon) After you download:choose the polygon data, not line.  
* Alternatively, you could display the inverse Polygons of the US State Boundaries layer.   

c. NYC Census Tract (https://data.cityofnewyork.us/City-Government/2010-Census-Tracts/fxpq-c8ku)

d. US State Boundaries (https://catalog.data.gov/dataset/tiger-line-shapefile-2017-nation-u-s-current-state-and-equivalent-national)

### Creating a map of 311 complaints:  
#### 1. Download the 311 pothole data:
* We only want to have 311 *pothole* related complaints.  
* We'll also want to filter through complaints that were made in certain dates. For the purpose of our exercise we’d want to download two files: each for one year: 2018 and 2019.
* Note that this tutorial will be a walk through for the 2018 data. In order to compare between both years, you will be replicating this process independently for 2019.
* In the NYC open data platform, search 311 Service Requests from 2010 to Present. Click on the “Filter” section.
* For the first filter condition, choose “Created Date” , “is between” : manually choose: “01/01/2018 12:00:00 AM” and “12/31/2018 12:00:00 AM”
* Now Scroll down and click on “+ add another filter condition”: choose “Descriptor” is “Pothole”. Press “Enter” for the filters to apply. Make sure the filter worked in the bottom part of the browser, you should have about 66K results that match this search.
![,](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/potholes_assign/311_filter.png)

* In the “Export” section download the data in a CSV format  

#### 2. Import the 311 pothole complaints into QGIS
![d](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/potholes_assign/add_csv.png)


* Choose the data
- In the “geometry definition” choose: “Point coordinates”: make sure the X filed is set to “Longitude” and that the Y field is set to “Latitude”.
- “Geometry CRS”: EPSG: 4326 - WGS 84

#### 3. Count number of 311 pothole complaints per census tract

* To be able to compare different areas’ number of pothole complaints we will count the number of points per census tract. To do so we will use a built-in function in QGIS that does exactly that.
* Go to Setting → Options → Processing Settings → General → Inavlid features filtering → Skip (ignore) features with invalid geometries  


* Go to Vector→ Analysis Tools → Count Points in Polygon
![s](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/potholes_assign/analysis.png)

* Choose the Census tracts layer in Polygons and 311 data in the points layer
* Click “Run”

![l](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class%204/potholes_assign/311_analysis.png)

This process will take 10-20 minutes to run. The output of this analysis is a layer named “Count”. Once done, the layer will include a column named “NUMPOINTS” which is the count of the number of pothole complaints per census tract.

#### 4. Visualize a graduated map of number potholes:

* Re order to layers so that:
- The 311 points layer is hidden
- The point per polygon layer is first
- The NYC hydro layer is second
- Then the state hydro layer
- Lastly the state boundary

* To visualize the 311 potholes, we would want to create a graduated display of every census tract relative to the number of potholes in that census tract.
* Double click on the count layer to open the layer settings:
- In the dropdown choose: Graduated
- In columns choose NUMPOINTS
- Click quantile (Equal Count)
- Then click classify to show the quantile groups
- Adjust colors and style
- For esthetic reasons we will also remove the census tract boundary:
Go to the Layer setting: Symbol → Choose “ Sample fill” -- Stroke color: Transparent Stroke →  Apply  

* To export the map as an image open a new print layout.

* Here you can add a legend, north arrow, title and a scale bar

#### The result should look similar to this:

![s](https://github.com/avigailvantu/SUE-Class/blob/master/pothole%202018.png)

#### 5. In order to get insights and complete this tutorial repeat the same process for the 2019 311 pothole data.
* Download the data from Jan 1st 2019 to Dec 31st 2019
* Filter to only have the pothole 311 complaints

* Once you generated both maps (2018 and 2019). Answer these follow-up questions:
- What are some insights you can get from comparing both maps?
- Which areas have a high level of pothole complaints?
- Which areas seem to have lower potholes complaints?
- Can you think of reasons for some of the patterns you found?  
