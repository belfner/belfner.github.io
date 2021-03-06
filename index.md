<!DOCTYPE html>
<html>
  <head>
    <title>Data Layer: Simple</title>
    <meta name="viewport" content="initial-scale=1.0">
    <meta charset="utf-8">
    <style>
      
      /* Always set the map height explicitly to define the size of the div
       * element that contains the map. */
      #map {
        height: 100%;
      }
      /* Optional: Makes the sample page fill the window. */
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
      #info-box {
        background-color: white;
        border: 1px solid black;
        bottom: 30px;
        height: 20px;
        padding: 10px;
        position: absolute;
        left: 30px;
      }
    
    </style>
  </head>
  <body>
    <div id="map"></div>
	<div id="info-box"></div>
    <script>

      var map;
      function initMap() {
        map = new google.maps.Map(document.getElementById('map'), {
          zoom: 4,
          center: {lat: 37.0902, lng: -95.7129}
        });

        // NOTE: This uses cross-domain XHR, and may not work on older browsers.
        map.data.loadGeoJson(
            'http://benelfner.com/states.geojson');
			
		map.data.setStyle({
		  fillColor: 'green',
		  strokeWeight: 1
		});
			
		map.data.addListener('mouseover', function(event) {
		  document.getElementById('info-box').textContent =
			  event.feature.getProperty('unit_name');
		});
		
		var infowindow = new google.maps.InfoWindow();
		
		map.data.addListener('click', function(event) {
		  // in the geojson feature that was clicked, get the "place" and "mag" attributes
		  let place = event.feature.getProperty("unit_name");
		  let magnitude = event.feature.getProperty("unit_type");
		  let html = place + ' name, ' + magnitude + ' type'; // combine place and magnitude, inserting additional text between them
		  infowindow.setContent(html); // show the html variable in the infowindow
		  infowindow.setPosition(event.latLng); // anchor the infowindow at the marker
		  infowindow.setOptions({pixelOffset: new google.maps.Size(0,-30)}); // move the infowindow up slightly to the top of the marker icon
		  infowindow.open(map);
		});
		
      }
    </script>
    <script async defer
    src="https://maps.googleapis.com/maps/api/js?key=AIzaSyCZ-JHIZGqY3S0dHD0oQzDFVlsaG_OSGcs&callback=initMap">
    </script>
  </body>
</html>

