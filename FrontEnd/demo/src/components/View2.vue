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
    var map = new mapboxgl.Map({
      container: 'map', // container ID
      style: 'mapbox://styles/mapbox/streets-v11', // style URL
      center: [144.9, -37.8], // starting position [lng, lat]
      zoom: 9 // starting zoom
    })
    map.on('click', function (e) {
      console.log('click!')
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

#main{
  width: 100%;
  height: 900px;
  margin: 0 auto;
}

</style>
