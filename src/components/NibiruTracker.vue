<template>
  <div>
    <div class="main_banner">
      <h1 class="main_title">Nibiru</h1>
    </div>
    
    <h3 style="margin-left: 1em; margin-bottom: 0; color: white;">Choose Call Type</h3>
    <div class="main_container">
      <ul class="list">
        <li class="list_item" v-on:click="mobile ? mobile = false : mobile = true;"><a class="list_text">Mobile Authenticated</a> <a class="letter_code">M</a> </li>
        <li class="list_item" ><a class="list_text">ANI Authenticated</a> <a class="letter_code">A</a> </li>
        <li class="list_item" ><a class="list_text">ANI + VRU Authenticated</a> <a class="letter_code">B</a> </li>
        <li class="list_item" ><a class="list_text">VRU Autheticated</a> <a class="letter_code">V</a> </li>
        <li class="list_item" ><a class="list_text">Account not Authenticated</a> <a class="letter_code">I</a> </li>
        <li class="list_item" ><a class="list_text">No customer Info</a> <a class="letter_code">N</a> </li>
      </ul>
    
    
    
      <Mobile v-if="mobile"/>
    </div>

    

  </div>
</template>

<script>
import Mobile from './Mobile'
export default {
  name: 'NibiruTracker',
  components: {
    Mobile
  },
  data () {
    return {
      mobile: 0,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .main_banner {
    display: flex;
    justify-content: left;
    align-items: center;
    width: 100%;
    height: 4em;
    background: black;
  }
  .main_title {
    margin-left: 1em;
    color: white;
  }
  .main_container {
    padding-left: 1em;
    display: grid;
    grid-template-columns: 1fr 4fr 2fr;
    grid-gap: 1.5em;
  }
  .list {
    padding-top: 2em;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 2em;
    list-style: none;
  }
  .list_item {
    width: 100%;
    height: 8em;
    display: flex;
    align-items: center;
    justify-content: left;
    box-shadow: 0 10px 6px -6px #777;
    background: white;
    position: relative;
  }
  .list_item:hover { cursor: pointer; }
  .list_text {
    margin: .5em 0 0 .8em;
    padding: 0;
    font-size: 1.1em;
    color: black;
    font-weight: bold;
  }
  .letter_code {
    width: 4em;
    height: 2em;
    display: flex;
    align-items: center;
    justify-content: center;
    top: 15%;
    right: 0;
    position: absolute;
    background: steelblue;
    color: white;
  }
</style>
