<template>
  <v-app>
    <v-content>
      <NibiruTracker/>
    </v-content>
  </v-app>
</template>

<script>
import NibiruTracker from './components/NibiruTracker'

export default {
  name: 'App',
  components: {
    NibiruTracker
  },
  data () {
    return {
      //
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto');
* {
  margin: 0;
  padding: 0;
  background: linear-gradient(to right, #355c7d, #6c5b7b, #c06c84);;
}
body {
  margin: 0;
  padding: 0;
  
  
}

#app {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}
</style>
