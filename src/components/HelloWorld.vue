<template>
  <div class="hello">
  </div>
  <div v-for="item in data" :key = "item.IP">
    <label for ="name"></label>
    <h1 name = "name">{{ item.VMName}}</h1>
    <label for="price"></label>
    <h2 name="price">{{ item.Status}}</h2>
  </div>
</template>

<script>
import demo from './Demo-Output.json';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      data: demo
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>