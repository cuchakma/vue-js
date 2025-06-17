<template>
  <HeadingMessage v-if="showNotice" :text='text'/>
  <!-- <h1>{{ count }}</h1>
  <button @click="click">Click Me To Increment</button>
  <ul>
    <li v-for="(data, index) in datas" v-bind:key="index">{{ data }}</li>
  </ul>
  <a v-bind:href="link" v-bind:data-attr="cupid">Click To Enter Google</a> -->
  <button @click="noticeEvent">Show/Hide</button>
</template>

<script>
import HeadingMessage from './components/HeadingMessage.vue'
  export default {
    components:{
      HeadingMessage
    },
    data() {
      return {
        count:0,
        datas:['cupid', 'rhine', 'guddu'],
        link:'www.google.com',
        showNotice:true,
        text:'Hello Niggs'
      }
    },
    methods: {
      click() {
        this.count++;
      },
      noticeEvent() {
        this.showNotice = !this.showNotice;
      }
    },
  }
</script>