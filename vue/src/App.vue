<template>
  <div>
    <NavBar :isClient="isClient"/>
    <router-view :isClient="isClient" @troca="trocar"/>
    <Footbar />
  </div>

</template>

<script>
import NavBar from './components/NavBar.vue'
import Footbar from './components/Footbar.vue'

export default {
  components:{
    NavBar, Footbar
  },
  data() {
    return {
      isClient: false  
    }
  },
  methods: {
    trocar(){
      this.isClient = !this.isClient
    }
  },

}
</script>

<style>
  *{font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box}
  body{
    background-color: #fff;
  }
  .main-container {
    margin: 10px;
    padding: 5px;
    min-height: 250px;
    background-color: #888;
  }
</style>
