<template>
  <main>
    <h1>{{ title }}</h1>
    <ul>
      <li>key: {{ key }}</li>
      <li>key2: {{ key2 }}</li>
      <li>count: {{ count }}</li>
    </ul>
    <button @click="countup">countup</button>
    <form action="." @submit.prevent="onSubmit">
      <input type="text" cols="30" @keydown="keyArrow" />
      <button>button</button>
      <button type="submit">SUBMIT!</button>
    </form>
  </main>
</template>

<script>
 import axios from 'axios'
 
 export default {
     async asyncData(ctx) {
	 return {
	     title: 'Events',
	     key: null,
	     key2: "...",
	     count: 0,
	 }
     },
     methods: {
	 countup(event) { this.count++ },
	 onSubmit(event) {console.log(event)},
	 keyArrow(event) {console.log(event)},
	 keyDownEvent(event) {
	     this.count++
	     this.key = event.key
	 },
     },
     mounted () {
	 console.log('mounted')
	 //console.log(this)
     },
     beforeMount () {
	 console.log('beforeMount')
	 window.addEventListener('keydown', this.keyDownEvent)
	 //window.addEventListener('keyup', this.keyUpEvent)
     },
     destroyed () {
	 console.log('destroyed')
	 window.removeEventListener('keydown', this.keyDownEvent)
	 //window.removeEventListener('keyup', this.keyUpEvent)
     }
 }
</script>

<style>
 main {
   border: solid black 1px;
 }
</style>

