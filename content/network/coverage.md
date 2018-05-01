---
layout: single
title: Coverage
menu:
    main:
        parent: network
---
<script src='https://api.tiles.mapbox.com/mapbox-gl-js/v0.44.2/mapbox-gl.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox-gl-js/v0.44.2/mapbox-gl.css' rel='stylesheet' />
<style>
    #map { position:absolute; top:0; bottom:0; width:50%; }
</style>

<div id='map'></div>

<script>
  mapboxgl.accessToken = 'pk.eyJ1Ijoia2VudG5ldHdvcmsiLCJhIjoiY2pmejB4NXUxNHdoeTMybnZpeTl6enU0aSJ9.3VhMj8SGSOKY9dDS22be1g';
  var map = new mapboxgl.Map({
      container: 'map', // container id
      style: 'mapbox://styles/kentnetwork/cjgm9og8v003s2snz9m6a4eho', // stylesheet location
      center: [1.0789,51.2802], // starting position [lng, lat]
      zoom: 10.1 // starting zoom
  });
</script>
