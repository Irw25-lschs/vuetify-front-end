<template>
  <div>
    <label>
      <input type="checkbox" v-model="showOnlineServers" />
    </label>
    <label>
      <input type="checkbox" v-model="showOfflineServers" /> 
    </label>
    <table>
      <thead>
        <tr>
          <th>Column 1</th>
          <th>Column 2</th>
          <th>Column 3</th>
          <th>Column 4</th>
          <th>Column 5</th>
          <th>Column 6</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in tableData" :key="item.id">
          <td>{{ item.Status }}</td>
          <td>{{ item.IP }}</td>
          <td>{{ item.LastCheckInTime }}</td>
          <td>{{ item.VMName }}</td>
          <td>{{ item.HyperVisor }}</td>
          <td>{{ item.LastCheckInTime }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import { fetchData } from '../fetchData';

export default {
  data() {
    return {
      tableData: [],
    };
  },
  async mounted() {
    try {
      const url = 'http://jwerts.aiscorp.local:3000/servers'; // Replace with your server link
      this.tableData = await fetchData(url);
    } catch (error) {
      // Handle error
    }
  },
};
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
