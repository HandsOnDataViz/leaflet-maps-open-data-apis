# leaflet-data-apis
Leaflet map with multiple API data feeds Socrata and Esri ArcGIS Online. View [demo](https://handsondataviz.github.io/leaflet-maps-open-data-apis/index.html).

![Screenshot](images/screenshot.png)

If you plan to query Socrata heavily, it is recommended you sign up for an API token. See more details at https://dev.socrata.com/.

### Example of data fetch from Socrata

Assuming you have your `map` initialized and layers control created, load data from a GeoJSON endpoint in Socrata
and add it to the map as shown below.

```javascript
$.getJSON('https://data.ct.gov/api/geospatial/evyv-fqzg?method=export&format=GeoJSON', function(data) {

  var towns = L.geoJson(data, {
    fillOpacity: 0,
    weight: 0.5,
    color: 'silver',
  }).addTo(map)

  // Add town boundaries as a checkbox to the legend
  legend.addOverlay(towns, 'Town boundaries')

  // Re-center the map view
  map.fitBounds( towns.getBounds() )

})
```

### Example of data load using esri-leaflet plugin

Esri-leaflet plugin allows you to load the data without using jQuery's `getJSON()` function.

```javascript
var ems = L.esri.featureLayer({
  url: 'https://services1.arcgis.com/Hp6G80Pky0om7QvQ/arcgis/rest/services/EMS_Stations/FeatureServer/0',
  where: "STATE = 'CT'",
  pointToLayer: function(feature, latlng) {
    return L.circleMarker(latlng, {
      radius: 4,
      fillColor: 'blue',
      color: 'blue',
      weight: 0.1,
      opacity: 1,
      fillOpacity: 0.5,
      pane: 'markerPane'
    }).bindTooltip(feature.properties.NAME)
  }
}).addTo(map)

legend.addOverlay(ems, 'EMS Stations')
```

## Learn more

- [Pull Open Data into Leaflet Map with APIs Tutorial](https://handsondataviz.org/leaflet-maps-open-apis.html) in *Hands-On Data Visualization* book (https://HandsOnDataViz.org)
- Leaflet-esri example (https://github.com/jackdougherty/leaflet-esri) by Jack Dougherty
- Tim Stallmann, Mapping external GeoJSON data, https://www.savaslabs.com/blog/mapping-external-geojson-data

## Credits
* Leaflet ([see license](https://github.com/Leaflet/Leaflet/blob/master/LICENSE))
* Esri Leaflet plugin (Apache 2.0)
* jQuery (MIT)
