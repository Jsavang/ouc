<template>
  <div id="app">
    <h2>Autocomplete Google Maps</h2>
    <GmapAutocomplete @place_changed="setPlace" />
    <button class="btn" @click="addMarker">Add</button>

    <GmapMap
      :center="center"
      :zoom="12"
      style="width: 100%; height: 400px; margin-top: 20px"
    >
      <GmapMarker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        @click="center = m.position"
      />
    </GmapMap>
    <ul id="v-for-object">
      <li v-for="place in placeList"
      :key="place.id">
        <h2>{{ place }}</h2>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      center: { lat: 45.508, lng: -73.587 },
      currentPlace: null,
      markers: [],
      placeList: [],
    };
  },
  methods: {
    setPlace(place) {
      this.currentPlace = place;
    },
    addMarker() {
      this.placeList.push(this.currentPlace.formatted_address);
      console.log(this.placeList);
      if (this.currentPlace) {
        const marker = {
          lat: this.currentPlace.geometry.location.lat(),
          lng: this.currentPlace.geometry.location.lng(),
        };
        this.markers.push({ position: marker });
        this.center = marker;
        this.currentPlace = null;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.pac-target-input {
  padding: 10px;
  width: 20%;
}

.btn {
  margin-left: 20px;
  padding: 10px 20px;
  background-color: greenyellow;
}
</style>