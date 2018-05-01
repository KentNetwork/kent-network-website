---
layout: map
title: Coverage
menu:
    main:
        parent: network
---

<script src='https://api.tiles.mapbox.com/mapbox-gl-js/v0.44.2/mapbox-gl.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox-gl-js/v0.44.2/mapbox-gl.css' rel='stylesheet' />

<div id='map' style="height:400px"></div>
<script>
  mapboxgl.accessToken = 'pk.eyJ1Ijoia2VudG5ldHdvcmsiLCJhIjoiY2pmejB4NXUxNHdoeTMybnZpeTl6enU0aSJ9.3VhMj8SGSOKY9dDS22be1g';
  var map = new mapboxgl.Map({
      container: 'map', // container id
      style: 'mapbox://styles/kentnetwork/cjgm9og8v003s2snz9m6a4eho',
      center: [1.21501,51.275050],
      zoom: 10.1, // starting zoom,
      pitch: 45,
  });

  map.on('load', function() {
    // Insert the layer beneath any symbol layer.
    var layers = map.getStyle().layers;

    var labelLayerId;
    for (var i = 0; i < layers.length; i++) {
        if (layers[i].type === 'symbol' && layers[i].layout['text-field']) {
            labelLayerId = layers[i].id;
            break;
        }
    }

    map.addLayer({
        'id': '3d-buildings',
        'source': 'composite',
        'source-layer': 'building',
        'filter': ['==', 'extrude', 'true'],
        'type': 'fill-extrusion',
        'minzoom': 15,
        'paint': {
            'fill-extrusion-color': '#aaa',

            // use an 'interpolate' expression to add a smooth transition effect to the
            // buildings as the user zooms in
            'fill-extrusion-height': [
                "interpolate", ["linear"], ["zoom"],
                15, 0,
                15.05, ["get", "height"]
            ],
            'fill-extrusion-base': [
                "interpolate", ["linear"], ["zoom"],
                15, 0,
                15.05, ["get", "min_height"]
            ],
            'fill-extrusion-opacity': 0.6
        }
    }, labelLayerId);
});

var geojson = {
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "properties": {
                "title": "Gateway:",
                "message": "Ingram",
                "iconSize": [30, 30]
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    1.0660251975059507,
                    51.298447975523885
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "title": "Gateway:",
                "message": "Invicta House",
                "iconSize": [40, 40]
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    1.4047238230705261,
                    51.381119269497034
                ]
            }
        }
    ]
};

geojson.features.forEach(function(marker) {

  var el = document.createElement('div');
  el.className = 'marker';

  new mapboxgl.Marker(el)
  .setLngLat(marker.geometry.coordinates)
  .setPopup(new mapboxgl.Popup({ offset: 25 })
  .setHTML('<h3>' + marker.properties.title + '</h3><p>' + marker.properties.message + '</p>'))
  .addTo(map);
});

</script>

<style>
  .marker {
  background-image: url('/images/logo/marker.png');
  background-size: cover;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  cursor: pointer;
  }

  .mapboxgl-popup {
    max-width: 200px;
  }

  .mapboxgl-popup-content {
    text-align: center;
    font-family: 'Open Sans', sans-serif;
  }
</style>
