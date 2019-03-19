<template>
  <div>
      <div id='map' class='map'> </div>
  </div>
</template>

<script>

export default {
  name: 'Map',
  mounted(){
          
    window.mapboxgl.accessToken = "pk.eyJ1Ijoic25pcGNhcnQiLCJhIjoiY2p0OTB5d2l5MDQzbjQzbzhxeTJvbGcxZyJ9.R0dhrDX81Ufn31cZkRDC6Q";	
    
    var map = new window.mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/dark-v9',
        center: [-81.4608, 48.4758], 
        zoom: 4
    });

    map.on('load', (() => {

        this.markers.forEach(function(marker) {
            var el = document.createElement('div');
            el.className = 'marker';

            new window.mapboxgl.Marker(el)
                .setLngLat([parseFloat(marker.latitude), parseFloat(marker.longitude)])
                .addTo(map);
        });
        
        this.markers.forEach((x) => {
            document.getElementById(x.name)
                .addEventListener('click', () => {
                    map.flyTo({
                        center: [parseFloat(x.latitude), parseFloat(x.longitude)],
                        zoom: 9
                    })
                ;}
            )
        })
           
    }).bind(this));
  },
  props: {
    markers: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.marker {
  background-image: url('./../assets/mapbox-icon.png');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.map { 
    height: 500px;
    border: #f6e767 3px solid;
    border-radius: 7px;
}
</style>
