<template>
  <div id="nuxt-root">
    <main>
      <h1>9box</h1>
      <div id="box-group">
	<div class="row" v-for="row in rows">
	  <div class="col" v-for="col in row">
	    {{ col }}
	  </div>
	</div>
      </div>
    </main>
  </div>
</template>

<script>
 import axios from 'axios'
 export default {
     async asyncData(context) {
	 //console.log(context)
	 return {
	     rows: [
		 [1, 2, 3],
		 [4, 5, 6],
		 [7 ,8, 9]
	     ]
	 }
     }
 }
</script>

<style>
 div#box-group {
   display: table-cell;
   vertical-align: middle;
   border: solid #CFD 10px;
   padding: 5px;
 }
 div.row {
   clear: both;
 }
 div.col {
   width: 100px;
   height: 100px;
   border: solid red 1px;
   background-color: yellow;
   float: left;
   text-align: center;
   margin: 5px;
 }
 div#nuxt-root {
 }
 main {
   border: solid blue 2px;
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

