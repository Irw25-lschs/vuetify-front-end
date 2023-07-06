<template>
  <div class="card text-center m-3">
    <div class="card-body">
      <div class="checkbox-container">
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            id="removeOnlineCheckbox"
            v-model="removeOnline"
          />
          <label class="form-check-label" for="removeOnlineCheckbox">
            Remove Online
          </label>
        </div>

        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            id="removeOfflineCheckbox"
            v-model="removeOffline"
          />
          <label class="form-check-label" for="removeOfflineCheckbox">
            Remove Offline
          </label>
        </div>
      </div>

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
          <tr v-for="server in filteredServers" :key="server.VMName">
            <td>{{ server.VMName }}</td>
            <td>{{ server.Status }}</td>
            <td>{{ server.IP }}</td>
            <td>{{ server.LastCheckInTime }}</td>
            <td>{{ server.HyperVisor }}</td>
            <td>{{ server.Hostname }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';

var Servers = ref(null);
var removeOnline = ref(false);
var removeOffline = ref(false);

onMounted(() => {
  fetch('http://fkhan.aiscorp.local:6284/servers')
    .then(response => response.json())
    .then(data => {
      Servers.value = data;
    })
    .catch(error => {
      console.error('Error fetching data:', error);
    });
});

const filteredServers = computed(() => {
  if (!Servers.value) {
    return [];
  }
  if (removeOnline.value && removeOffline.value) {
    return [];
  }
  if (removeOnline.value) {
    return Servers.value.filter(server => server.Status === 'Offline');
  }
  if (removeOffline.value) {
    return Servers.value.filter(server => server.Status === 'Running');
  }
  return Servers.value;
});
</script>

<style scoped>
.table {
  width: 100%;
  border: 1px solid;
  background-color: #708490;
  font-family: monospace;
  color: white;
}

th {
  background-color: #ef3b32;
  color: white;
}

td {
  padding: 8px;
  text-align: left;
  border: 1px solid #000000;
  border-bottom: 1px solid #000000;
}

tr:hover {
  background-color: #9dafb9;
}

.checkbox-container {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 10px;
}

.form-check {
  margin-right: 10px;
}
</style>