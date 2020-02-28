### Geocoding Data on QGIS Using Google API

### Goal:

This tutorial aims to cover how to attribute geographical features to non geographical data. In many cases when we obtain data without geographical attributes we can easily join tables with a shapfile that  contains the same geographical entity. For example, if we obtain a CSV of data that is Zip Code level information on NYC. We can probably obtain a shapfile or geojson of all Zip Codes in NYC. Then we can join tables to have the CSV attributes merged with the shapfile.

In this tutorial we will learn how to transform non geographical data which that can not be easily associated with geographical data.

### Geocoding:

The process of geocoding is means that we will assign (X,Y) coordinates to a CSV file with some geographical name (e.g. city, state, exact address). There are different ways to geocode. Today we will learn how to use Google API through QGIS to goecode data. This process can take a little bit of time. We will be working with a relatively small data so we can compute the API quite fast (> than 10 minutes hopefully). If you use the same methods for bigger data (< 1000 rows), keep in mind that this can take a few minutes or more.  

### Getting started:

Before we go into QGIS and actually get to geocode data. We'll need to each get an API Key from Google.

The Key can be accessed for free from Google (however you may be required to setup your account billing info).

	[Click here to get your Google API Key](https://developers.google.com/maps/gmp-get-started?authuser=2)

  Once you get your API Key, make sure to copy it somewhere safe. We will be using it soon.


### Get data:

We will be working with the list of cities that have Open Data platforms worldwide. This data was obtained from the DATA.GOV website. Along with the city name, the file also includes the URL for the Open Data platform (some of you may want to have a closer look at this list as we approach our final projects).


You can download the data from [here.](https://developers.google.com/maps/gmp-get-started?authuser=2)https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/opendatasites91819.csv)

### Get ready to GEOCODE!

Now that we have both the API Key and the date we want to geocode, we are (almost)ready to go!
* Open QGIS
* In order to geocode we will need to download an plugin to our QGIS.
* The plugin name is MMQGIS. MMQGIS is a bundle of Python plugins that enables different analyses and data manipulations like animation, geometry conversion and geocoding.  
* To get the MMQGIS plugin go to: Plugins: Manage and Install Plugins. ![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_1.png)

* Search for MMQGIS--click on install plugin

![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_2.png)

* Once Qgis is done, you will see the plugin name appearing on the upper menu bar.

### Load data:

Let's load the world map so we have a geographical framework. We will also use the world map to visualize our final map.

* Go to the bottom bar on the map section of QGIS--click on the "Coordinate" window--type: "world" and Enter.

 * You should see the world map displayed.

 ![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_3.png)

### Geocode cities with Open Data platforms:

For our exercise we have the city of each data platform. Therefore we will need Google to use city name in order to geocode the data into points. The Google  geocoding algorithm is pretty good. However, it not always 100% perfect as we will see soon. Therefore, in some occasions when running the algorithm. That is why QGIS saves a file of all successful address conversions as well as those that fail to geocode for some reason.

* Go to MMQGIS plugin and follow the below steps:

![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_4.png)

* once the geocode window opened insert all these details:
1. Input CSV: choose the opendatasites csv.
2. Make sure the column "City" appears in the City dropdown.
3. in web services choose: Google
4. insert your API key
5. Rename the output file name to :opendatacities.shp
6. Rename the not found output list to: not_found.CSV

![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_5.png)

* Click-- Apply and wait for the geocoding to be ready (should take aprox 5-10 min).
* When the plugin is done, you will see a pop up saying how many successful/unsuccessful geocodes you got. I had 310 successful (which means 3 were unsuccessful).

* Note that the output file will be visualized on your map once the algorithm is done.

* Now change the dots colors and style
* Also change the style of the map.
* Finally go to the print layout window for final touches and to download the map.

![alt text](https://github.com/avigailvantu/SUE-Class/blob/master/Class_5/class5_6.png)

* What are your observations when looking at this map? Which areas of the world have more open data programs? Which areas are have some and which areas not at all?

* To submit this map, export the final map and write one paragraph discussing the above questions.
