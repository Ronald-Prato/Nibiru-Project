<template>
  <div>
    <div class="main_banner">
      <h1 class="main_title">Nibiru <span style="color: white; font-size: 15px;">(alpha v1.0)</span></h1>
      <span style="font-size: 14px; color: white; position: absolute; right: 1%;">Ronald Prato</span>
    </div>
    
    <h3 style="margin: 1em 0 0 2.5em; color: white; text-decoration: underline">Choose Call Type</h3>
    <div class="main_container">
      <ul class="list">
        <li class="list_item" v-on:click="component = 'mobile';"><a class="list_text">Mobile Authenticated</a> <a class="letter_code">M</a> </li>
        <li class="list_item" v-on:click="component = 'ani';" ><a class="list_text">ANI Authenticated</a> <a class="letter_code">A</a> </li>
        <li class="list_item" v-on:click="component = 'ani+vru';"><a class="list_text">ANI + VRU Authenticated</a> <a class="letter_code">B</a> </li>
        <li class="list_item" v-on:click="component = 'vru';"><a class="list_text">VRU Autheticated</a> <a class="letter_code">V</a> </li>
        <li class="list_item" v-on:click="component = 'ana'"><a class="list_text">Account not Authenticated</a> <a class="letter_code">I</a> </li>
        <li class="list_item" v-on:click="component = 'nci'"><a class="list_text">No customer Info</a> <a class="letter_code">N</a> </li>
      </ul>
    
    
    
      <Mobile v-if="component == 'mobile'"/>
      <ANI v-if="component == 'ani'"/>
      <ANI_VRU v-if="component == 'ani+vru'"/> 
      <VRU v-if="component == 'vru'"/>
      <ANA v-if="component == 'ana'" />
      <NoCustomerInfo v-if="component == 'nci'"/>

      <Notes v-if="component != ''"/>
    </div>

    

  </div>
</template>

<script>
import Mobile from './Mobile'
import ANI from './ANI'
import ANI_VRU from './ANI+VRU'
import VRU from './VRU'
import Notes from './Notes'
import ANA from './Account_Not_Authenticated'
import NoCustomerInfo from './No_Customer_Info'

export default {
  name: 'NibiruTracker',
  components: {
    Mobile,
    ANI,
    ANI_VRU,
    VRU, 
    ANA,
    NoCustomerInfo,
    Notes,
  },
  data: () =>  ({
    component: ""
  })
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
    background: linear-gradient(to right, #108dc7, #ef8e38);
    position: relative; 
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
