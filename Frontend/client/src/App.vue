<template>
  <div id="nav">
    <Navbar/>
    <router-view/>
  </div>
  
</template>

<script>
import Navbar from './components/Navbar.vue'
import axios from 'axios'
export default {
  name: 'App',
  components:{
    Navbar
  },
  beforeCreate(){
    const token = this.$store.state.token
    if(token){
      axios.defaults.headers.common['Authorization'] = "Token" + token
    }else{
      axios.defaults.headers.common['Authorization'] = ""
    }
  }
}
</script>

<style lang="scss">

</style>
