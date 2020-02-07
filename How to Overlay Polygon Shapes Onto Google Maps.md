## How to Overlay Polygon Shapes Onto Google Maps ##

In this tutorial, I'll teach you how to overlay polygon shapes onto Google Maps and embed it into a website. The example we will use will be to overlay the US census' states data. Data processing will be done with mapshaper.org which you can learn more about [here](https://simplemaps.com/resources/guide-to-mapshaper).

#### 1. Use the Google Maps JavaScript API to embed a basic map of the US
The first step is to add a Google Maps JavaScript application in your website. To do this you must first create a Google Cloud Platform Project which you can read about [here](GoogleCloudProjectSetup). (Important) When adding the API use the Maps JavaScript API instead of the Maps embed API.



#### 2. Add application to website

Once this setup is done you can start adding code to your website. The code required is very simple.

Insert these lines where ever you want your map to be located on your website

    <div id="map">
		<script>
			var map;

			function initMap() {
				map = new google.maps.Map(document.getElementById('map'), {
					zoom: 3,
					center: {
						lat: 39.8283,
						lng: -98.5795
					}
				});
			}
		</script>
	</div>

Insert this line with the rest of your scripts or if you have none, place it at the bottom of your html section. Replace "YOUR_KEY_HERE" with the key from your project

    <script async defer src="https://maps.googleapis.com/maps/api/js?key=YOUR_KEY_HERE&callback=initMap" type="text/javascript"></script>

#### 2. Get data
Once you have Google Maps embedded into your website, you can add geographic data to it.

For, this tutorial we'll be getting our U.S. state data from the  [US Census Bureau](https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html "census.gov"). A cleaned version has already been preformatted for you to click on and download [here](C:\Users\benel\Documents\GitHub\belfner.github.io\index_files\states.zip "states.zip").

You'll need to unzip the folder of data before moving forward.


#### 3. Convert to GEOJSON
To use this data with Google Maps it will need to be converted from the Shapefile format to the GeoJSON format. To do this you will first need to upload it to [mapshaper.org](https://mapshaper.org/). This gives us an easy method to convert between different geographic data formats. 

1. Go to [mapshaper.org](https://mapshaper.org/)
2. Open the unziped folder with the states data
3. Select and drag all of the files from your computer and drop them within the mapshaper.org browser window
4. Click Import
5. If you did things properly, you should see the map appear. Click on the information icon and hover over a state to make sure that MapShaper has imported the associated data for each state.

![](images/import.png)


######*Optional:*######
*If you want to manipulate the data of the polygons, you can view the "Editing Shapefiles with MapShaper" section on our [guide to MapShaper](https://simplemaps.com/resources/guide-to-mapshaper).*

Finaly, to export the data:

1. Click on the Export button in the top right corner of the webite
2. Select GeoJSON as the File format on the window that popped up
3. Click Export

This will download the data in the GeoJSON format.


#### 4. Add GEOJSON Google Maps

To add the data to the embedded map:

1. Move the downloaded file to your websites folder
2. Add this line of code to initMap() and replace "PATH" with the path to the geojson file

	`map.data.loadGeoJson('PATH');`

	a example of this could be

	`map.data.loadGeoJson('http://example.com/parks.geojson');`

	your code should end up like this
	
	    <div id="map">
			<script>
				var map;
		
				function initMap() {
					map = new google.maps.Map(document.getElementById('map'), {
						zoom: 3,
						center: {
							lat: 39.8283,
							lng: -98.5795
						}
					});
		`			
					map.data.loadGeoJson('http://example.com/parks.geojson');
				}
			</script>
		</div>

	Test this code and you should see the shapes on the map

#### 5. Adjust the color of the shapes

#### 6. Make shapes clickable