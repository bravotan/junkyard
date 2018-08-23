<template>
  <div>
    <h1>Header</h1>
    <nuxt-link to="/gallery/">gallery</nuxt-link>
    <div v-for="value,key,index in values">
      index:{{index}} key:{{ key }} value:{{ value }}
    </div>
  </div>
</template>

<script>
 import axios from 'axios'
 export default {
     async asyncData({ query }) {
	 const { data } = await axios.get('http://localhost:8080/webdesign/range5.json')
	 return { values: data }
     }
 }
</script>

<style>
</style>

