<template>
  <div id="nuxt-root">
    <main>
      <h1>Header</h1>
      <div v-for="value,key,index in values">
	index:{{index}} key:{{ key }} value:{{ value }}
      </div>
    </main>
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
 div#nuxt-root {
 }
 main {
   border: solid black 1px;
   background-color: #CCC;
 }
 h1 {
   border: solid black 1px;
   border-radius: 80px;
   padding: 0 0 0 20px;
   font-family:
     'HelveticaNeueUltraLight',
     'HelveticaNeue-Ultra-Light',
     'Helvetica Neue Ultra Light',
     'HelveticaNeue',
     'Helvetica Neue';
   font-weight: 300;
   color: #00F;
   border: solid black 1px;
   background-color: #FCF;
 }
</style>

