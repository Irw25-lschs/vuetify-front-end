<template>
  <v-app>
    <v-main>
      <img src="https://th.bing.com/th/id/OIP.jh9o0I5pyWbtqgxha1My0wG2CO?w=328&h=113&c=7&r=0&o=5&pid=1.7">
      <HelloWorld />
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
  import HelloWorld from '@/components/HelloWorld.vue'
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    }
</style>
