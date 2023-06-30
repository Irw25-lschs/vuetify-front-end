<template>
  <div class="card text-center m-3">
    <h5 class="card-header">Simple GET Request</h5>
    <div class="card-body">
      <table class="table">
        <thead>
          <tr>
            <th>VM Name</th>
            <th>Status</th>
            <th>IP</th>
            <th>Last Check-In Time</th>
            <th>HyperVisor</th>
            <th>Hostname</th>
          </tr>
        </thead>
        <tbody>
          <tr  v-for="item in products" :key = "item.IP">
            <td>{{ item.Servers.VMName.value }}</td>
            <td>{{ item.Servers.Status }}</td>
            <td>{{ item.Servers.IP }}</td>
            <td>{{ item.Servers.LastCheckInTime }}</td>      
            <td>{{ item.Servers.HyperVIsor }}</td>
            <td>{{ item.Servers.Hostname }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

var products = ref(null);

onMounted(() => {
  fetch('http://jwerts.aiscorp.local:3000/servers') 
    .then(response => response.json())
    .then(data => {
      products.value = data;
    })
    .catch(error => {
      console.error('Error fetching data:', error);
    });
});


</script>


<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th span {
  font-size: 10px;
  margin-left: 4px;
}
</style>
