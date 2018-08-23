<template>
  <div id="nuxt-root">
    <main>
      <h1>Gallery</h1>
      <div class="pager">
	<nuxt-link :to="`${first_page}`">|&lt;</nuxt-link>
	&nbsp;
	<nuxt-link :to="`${prev}`">&lt;</nuxt-link>
	&nbsp;
	{{ current_page }} of {{ last_page }}
	&nbsp;
	<nuxt-link :to="`${next}`">&gt;</nuxt-link>
	&nbsp;
	<nuxt-link :to="`${last_page}`">&gt;|</nuxt-link>
      </div>
      <transition-group name="list" tag="ul">
	<li v-for="(file, index) in files" :key="index">
	  <a v-bind:href="file" target=":blank">
	    <img v-lazy="file" width="200" />
	    <!--img :src="file" width="200" /-->
	  </a>
	</li>
      </transition-group>
      <div class="pager">
	<nuxt-link :to="`${first_page}`">|&lt;</nuxt-link>
	&nbsp;
	<nuxt-link :to="`${prev}`">&lt;</nuxt-link>
	&nbsp;
	{{ current_page }} of {{ last_page }}
	&nbsp;
	<nuxt-link :to="`${next}`">&gt;</nuxt-link>
	&nbsp;
	<nuxt-link :to="`${last_page}`">&gt;|</nuxt-link>
      </div>
    </main>
  </div>
</template>

<script>
 import axios from 'axios'
 import jsonQuery from 'json-query'
 import Vue from 'vue'
 import VueLazyload from 'vue-lazyload'
 Vue.use(VueLazyload)

 const server = "http://127.0.0.1:8081"

 const urls = {
     root: "/",
     itemlist_url: "/",
 }

 export default {
     data () {
	 return {
	     current_page: 1,
	     files: [],
	 }	 
     },
     validate ({ params }) {
	 return /^\d+$/.test(params.page)
     },
     async asyncData({ query, params }) {
	 const path = urls.itemlist_url
	 const page = params.page
	 const {data} = await axios.get(`${server}${path}?page=${page}`)
	 let files = []
	 for (let file of jsonQuery('files', {data: data}).value){
	     files.push(`${server}/${file}`)
	 }
	 return {
	     first_page: jsonQuery('first', {data: data}).value,
	     last_page: jsonQuery('last', {data: data}).value,
	     prev: jsonQuery('prev', {data: data}).value,
	     next: jsonQuery('next', {data: data}).value,
	     current_page: jsonQuery('current', {data: data}).value,
	     files: files,
	 }
     }
 }
</script>

<style>
 div#nuxt-root {
 }
 body {
   margin: 0;
   background-color: #CCC;
 }
 img {
   margin: 3px;
 }
 h1 {
   border: solid black 1px;
   border-radius: 10px;
   padding: 0 0 0 20px;
   font-family:
   'HelveticaNeueUltraLight',
   'HelveticaNeue-Ultra-Light',
   'Helvetica Neue Ultra Light',
   'HelveticaNeue',
   'Helvetica Neue';
   font-weight: 300;
   color: #009;
   border: solid black 1px;
   background-color: #FFF;
 }
 div.pager {
   text-align: center;
 }
 img[lazy=loading] {
   opacity: 0;
 }
 img[lazy=loaded] {
   transition: all 1s;
   opacity: 1;
 }
 ul li {
   display: inline-block;
   font-family: Helvetica, Arial, sans-serif;
   /*background: white;*/
   /*border: 1px #ddd solid;*/
   overflow: hidden;
   /*opacity: 0;*/
 }
 .list-enter-active, .list-leave-active {
   transition: all 1s;
 }
 .list-enter, .list-leave-to {
   opacity: 0;
 }
</style>
