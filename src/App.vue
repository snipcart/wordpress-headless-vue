<template>
  <div id="app">
    <h1>A WordPress Headless + Vue.js Demo</h1>
    <div class="badge-container">
      <div v-for="badge in markers" :key="badge.name">
        <Badge :name="badge.name" :image="badge.image" />
      </div>
    </div>

    <Map v-if="markers.length > 0" :markers="markers" />
    
  </div>
</template>

<script>
import Badge from './components/Badge.vue'
import Map from './components/Map.vue'

export default {
  name: 'app',
  data(){
    return {
      markers: []
    }
  },
  components: {
    Badge,
    Map
  },
  mounted(){
    fetch('https://wordpress-vue.herokuapp.com/index.php/wp-json/markers/v1/post')
      .then((r) => r.json())
      .then((res) => this.markers = res.map(x => x.acf));
  }
}
</script>

<style>
.badge-container {
  padding-top: 60px;
  display: flex;
  justify-content: space-between;
}

html, body {
    margin: 0;
    height: 100%;
    background-color: #FAFAFA;
    font-family: 'Roboto', sans-serif;
}

body {
  margin-left: 15%;
  margin-right: 15%;
}

#app > h1 {
  text-align: center;
  color: 212121;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#footer{
  text-align: center;
  text-decoration: none;
  color: 212121;
}


</style>
