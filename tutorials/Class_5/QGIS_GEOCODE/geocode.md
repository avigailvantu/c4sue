### Class 5: Geocoding Data on QGIS Using Google API

### Tutorial goal:

This tutorial aims to cover how to attribute geographical features to non geographic data. In many cases when we obtain data without geographical attributes we can easily join tables with a shapefile that contains the same geographical entity. For example, if we obtain a CSV file of data that is Zip Code level information on NYC. We can probably obtain a shapfile or geojson of all Zip Codes in NYC. Then we can join tables to have the CSV attributes merged with the shapfile.

In this tutorial we will learn how to transform non geographical data that can not be easily associated with geographical data into geographical data.

### 1. Geocoding:

Geocoding means that we will assign (X,Y) coordinates to a CSV file with some geographically related name (e.g. city, state, exact address). There are different ways to geocode. Today we will learn how to use Google API through QGIS to goecode data. This process can take a little bit of time. We will be working with a relatively small data so we can compute the API quite fast (< than 10 minutes hopefully). If you use the same methods for bigger data (>1000 rows), then keep in mind this process can take a few minutes or more.  

### 2. Getting started:

Before we go into QGIS and actually get to geocode data. We'll need to each get an API Key from Google.

The Key can be accessed for free from Google (however you may be required to setup your account billing info which may ask for credit card info).

[Click here to get your Google API Key](https://developers.google.com/maps/gmp-get-started?authuser=2)

  Once you get your API Key, make sure to copy it somewhere safe. We will be using it soon.


### 3. Get data:

We will be working with the list of cities that have Open Data platforms worldwide. This data was obtained from the DATA.GOV website. Along with the city name, the file also includes the URL for the Open Data platform (you might want to have a closer look at this list as we approach our final projects).


You can download the data from [here.](https://developers.google.com/maps/gmp-get-started?authuser=2)https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/opendatasites91819.csv)

### 4. Get ready to GEOCODE!

Now that we have both the API Key and the data we want geocoded, we are (almost)ready to go!

* In order to geocode we will need to download an plugin to our QGIS.
* The plugin name is MMQGIS. MMQGIS is a bundle of Python plugins that enables different analyses and data manipulations like animation, geometry conversion and geocoding.  
* To get the MMQGIS plugin go to: Plugins: Manage and Install Plugins. ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_1.png)

* Search for MMQGIS--click on install plugin

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_2.png)

* Once Qgis is done, you will see the plugin name appearing on the upper menu bar.

### 5. Load data:

Let's load the world map so we have a geographical framework. We will also use the world map to visualize our final map.

* Go to the bottom bar on the map section of QGIS--click on the "Coordinate" window--type: "world" and Enter.

 * You should see the world map displayed.

 ![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_3.png)

### 6. Geocode cities who have Open Data platforms:

For our exercise we have the city name for each city that has a data platform. Therefore we will need Google to use city name in order to geocode the data into points. The Google  geocoding algorithm is pretty good. However, it is not always 100% perfect as we will see soon. Therefore, in many occasions when running the algorithm we will not have 100% match. QGIS saves a file of all successful address conversions as well as those that it failed to geocode along the way.

* Go to the MMQGIS plugin and follow the below steps:

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_4.png)

* once the geocoded window opens insert all these details:
-  Input CSV: choose the opendatasites csv.
-  Make sure the column "City" appears in the City dropdown.
-  In web services choose: Google
-  Insert your API key
-  Rename the output file name to :opendatacities.shp
-  Rename the not found output list to: not_found.CSV

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_5.png)

* Click-- Apply and wait for the geocoding to be ready (should take aprox 5-10 min).
* When the plugin is done, you will see a pop up saying how many successful/unsuccessful geocodes you got. I had 310 successful, and 3 unsuccessful geocodes).

* Note that the output file will be visualized on your map once the algorithm is done.

* Now change the dots colors and style
* Also change the style of the map.
* Finally go to the print layout window for final touches and to download the map.

![alt text](https://github.com/avigailvantu/c4sue/blob/master/tutorials/Class_5/QGIS_GEOCODE/class5_6.png)

* What are your observations when looking at this map? Which areas of the world have more open data programs? Which areas are starting to catch up and which areas not at all?

* To submit this map, export the final map and write one paragraph discussing the above questions.
