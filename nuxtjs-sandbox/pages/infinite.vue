<template>
  <main id="nuxt-root">
    <ul>
      <li class="box" v-for="(item, index) in list">
	{{ index+1 }}
      </li>
      <infinite-loading @infinite="infiniteHandler"></infinite-loading>
    </ul>
  </main>
</template>

<script>
 import InfiniteLoading from 'vue-infinite-loading'
 import strftime from 'strftime'

 // It's like a python range().
 const range = n => Array.from(Array(n).keys())
 const CHUNKSIZE = 12;

 export default {
     components: {
	 InfiniteLoading,
     },
     async asyncData(context) {
	 return {
	     list: [],
	 }
     },
     methods: {
	 infiniteHandler($state) {
	     setTimeout(()=>{
		 let temp = []
		 for (var i of range(CHUNKSIZE)){
		     let now = strftime('%Y/%m/%d %H:%M:%S')
		     temp.push(now)
		 }
		 this.list = this.list.concat(temp)
		 $state.loaded()
	     }, 100)
	 }
     },
 }
</script>

<style>
 html {
   background-color: #333;
 }
 .box {
   width: 320px;
   height: 180px;
   border: solid black 1px;
   margin: 2px;
   padding: 5px;
   display: inline-block;
   background-color: #666;
   transition: all 0.5s;
   opacity: 1;
   font-size: 50pt;
   text-align: right;
   color: #0F0;
   padding-right: 30px;
 }
 .box:hover {
   transition: all 0.5s;
   opacity: 1;
   background-color: #CCC;
   color: #0C0;
 }
 .appear {
   visibility: visible;
 }
</style>

