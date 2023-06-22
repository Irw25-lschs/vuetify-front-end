<template>
  <div v-for="item in data" :key = "item.IP">
    <h1>VM: {{ item.VMName}}</h1>
    <h2>Status:{{ item.Status}}</h2>
    <h2>IP:{{ item.IP}}</h2>
    <h2>Host:{{ item.Hostname}}</h2>
    <h2>Hyper Visor:{{ item.HyperVisor}}</h2>
    <h2>Last check in time:{{ item.LastCheckInTime}}</h2>
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