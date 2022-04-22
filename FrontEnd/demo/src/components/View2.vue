<template>
  <div id='map' style='width: 100%; height: 900px;'></div>
</template>

<script>
import mapboxgl from 'mapbox-gl'

export default {
  name: 'View2',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    mapboxgl.accessToken = 'pk.eyJ1Ijoid2VuanVudyIsImEiOiJjbDI5czM2MGIwbTVtM250MzVnZXJ4MTd1In0.8e5pzkNEMkUEe37MkLXT0g'
    const map = new mapboxgl.Map({
      container: 'map', // container ID
      style: 'mapbox://styles/mapbox/light-v10', // style URL
      center: [144.9695, -37.8227], // starting position [lng, lat]
      zoom: 12 // starting zoom
    })
    let geoJson = {
      'type': 'geojson',
      'data': {
        'type': 'FeatureCollection',
        'features': [
          {
            'type': 'Feature',
            'properties': {
              'description':
                '<strong>abc</strong><img src="https://pbs.twimg.com/media/EYeX7akWsAIP1_1.jpg" width="200px">'
            },
            'geometry': {
              'type': 'Point',
              'coordinates': [144.93038, -37.801567]
            }
          },
          {
            'type': 'Feature',
            'properties': {
              'description':
                '<strong>Mad Men Season Five Finale Watch Party</strong>'
            },
            'geometry': {
              'type': 'Point',
              'coordinates': [144.94803, -37.811527]
            }
          },
          {
            'type': 'Feature',
            'properties': {
              'description':
                '<strong>Big Backyard Beach Bash and Wine Fest</strong>'
            },
            'geometry': {
              'type': 'Point',
              'coordinates': [144.9687, -37.821567]
            }
          },
          {
            'type': 'Feature',
            'properties': {
              'description':
                '<strong>Ballston Arts & Crafts Market</strong>'
            },
            'geometry': {
              'type': 'Point',
              'coordinates': [144.9409, -37.831567]
            }
          },
          {
            'type': 'Feature',
            'properties': {
              'description':
                '<strong>Seersucker Bike Ride and Social</strong>'
            },
            'geometry': {
              'type': 'Point',
              'coordinates': [144.9229, -37.78507]
            }
          }
        ]
      }
    }
    map.on('load', () => {
      // Add a layer showing the places.
      map.addSource('places', geoJson)
      map.addLayer({
        'id': 'places',
        'type': 'circle',
        'source': 'places',
        'paint': {
          'circle-color': '#4264fb',
          'circle-radius': 6,
          'circle-stroke-width': 2,
          'circle-stroke-color': '#ffffff'
        }
      })
      // Create a popup, but don't add it to the map yet.
      const popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false
      })
      map.on('mouseenter', 'places', (e) => {
        // Change the cursor style as a UI indicator.
        map.getCanvas().style.cursor = 'pointer'
        // Copy coordinates array.
        const coordinates = e.features[0].geometry.coordinates.slice()
        const description = e.features[0].properties.description
        // Ensure that if the map is zoomed out such that multiple
        // copies of the feature are visible, the popup appears
        // over the copy being pointed to.
        while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
          coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360
        }
        // Populate the popup and set its coordinates
        // based on the feature found.
        popup.setLngLat(coordinates).setHTML(description).addTo(map)
      })
      map.on('mouseleave', 'places', () => {
        map.getCanvas().style.cursor = ''
        popup.remove()
      })
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

</style>
