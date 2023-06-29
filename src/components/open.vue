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
          <th v-for="column in columns" :key="column.key" @click="sortData(column.key)">
            {{ column.label }}
            <span v-if="sortKey === column.key">
              {{ sortDir === 'asc' ? '▲' : '▼' }}
            </span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in sortedData" :key="item.id">
          <td v-for="column in columns" :key="column.key">
            {{ item[column.key] }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import { fetchData } from '@/api';

export default {
  data() {
    return {
      data: [],
      showOnlineServers: true, 
      showOfflineServers: true,
      jsonData: null,
      columns: [
        { key: 'VMName', label: 'VM Name' },
        { key: 'Status', label: 'Status' },
        { key: 'IP', label: 'IP' },
        { key: 'Hostname', label: 'Host Name' },
        { key: 'HyperVisor', label: 'Hyper Visor' },
        { key: 'LastCheckInTime', label: 'Last Check In' },
        // Add more columns as needed
      ]
    };
  },


  mounted() {
    this.fetchDataFromServer();
  },
  computed: {
    filteredServers() {
      // Filter the servers based on checkbox states
      return this.data.filter((data) => {
        if (this.showOnlineServers && data.Status === 'online') {
          return true;
        }
        if (this.showOfflineServers && data.Status === 'offline') {
          return true;
        }
        return false;
      });
    },
  },
  methods: {
    async fetchDataFromServer() {
      try {
        const url = 'http://jwerts.aiscorp.local:3000/servers';
        const data = await fetchData(url);
        this.jsonData = data;
      } catch (error) {
        console.error('Error:', error);
      }
    }
  }
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
