# leaflet-data-apis
Leaflet map with multiple API data feeds from USGS, Socrata, Esri ArcGIS Online. View [demo](https://handsondataviz.github.io/leaflet-data-apis/index.html).

![Screenshot](images/screenshot.png)

If you plan to query Socrata heavily, it is recommended you sign up for an API token at https://dev.socrata.com/.

### Example of data fetch from Socrata

Assuming you have your `map` initialized and layers control created, load data from a GeoJSON endpoint in Socrata, translate each feature into a layer (circleMarker), bind a popup to the marker,and add it to the map like shown below.

```javascript
$.getJSON("https://data.ct.gov/resource/v4tt-nt9n.geojson?&$$app_token=QVVY3I72SVPbxBYlTM8fA7eet", function(data) {
  
  var geoJsonLayer = L.geoJson(data, {
    pointToLayer: function(feature, latlng) {
      return L.circleMarker(latlng, {
        radius: 6,
        fillColor: 'blue',
        color: 'blue',
        weight: 2,
        opacity: 1,
        fillOpacity: 0.7
      }).bindPopup(feature.properties.name + '<br>' + feature.properties.district_name);
    }
  }).addTo(map);

  controlLayers.addOverlay(geoJsonLayer, 'Public Schools (CT Open Data-Socrata)');

});
```

### Example of data load using esri-leaflet plugin

Esri-leaflet plugin allows you to load the data without using jQuery's `getJSON` function.

```javascript
var bikeRoutes = L.esri.featureLayer({
  url: 'https://gis1.hartford.gov/arcgis/rest/services/OpenData_Community/MapServer/9',
  style: function(feature) {
    if (feature.properties.TYPE === 'Bike Lane') {
      return {color: 'green', weight: 3 };
    } else {
      return { color: 'blue', weight: 3 };
    }
  }
}).addTo(map);

controlLayers.addOverlay(bikeRoutes, 'Bike Routes (Hartford Open Data-ArcGIS Online)');
```

## Learn more

- [Pull Open Data into Leaflet Map with APIs Tutorial](https://handsondataviz.org/leaflet-maps-open-apis.html) in *Hands-On Data Visualization* book (http://HandsOnDataViz.org)
- Leaflet-esri example (http://github.com/jackdougherty/leaflet-esri) by Jack Dougherty
- Tim Stallmann, Mapping external GeoJSON data, http://savaslabs.com/2015/05/18/mapping-geojson.html

## Credits
* Leaflet ([see license](https://github.com/Leaflet/Leaflet/blob/master/LICENSE))
* Esri Leaflet plugin (Apache 2.0)
* jQuery (MIT)
