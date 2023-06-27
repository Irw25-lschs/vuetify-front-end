<template>
  <div>
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
export default {
  data() {
    return {
      data: [],
      sortKey: '',
      sortDir: 'asc',
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
    this.fetchData();
  },
 /* computed: {
    sortedData() {
      return this.data.sort((a, b) => {
        const modifier = this.sortDir === 'asc' ? 1 : -1;
        if (a[this.sortKey] < b[this.sortKey]) return -1 * modifier;
        if (a[this.sortKey] > b[this.sortKey]) return 1 * modifier;
        return 0;
      });
    }
  }, */
  methods: {
    fetchData() {
      fetch('http://jwerts.aiscorp.local:3000/servers')
        .then(response => response.json())
        .then(data => {
          this.data = data;
        })
        .catch(error => {
          console.error('Error:', error);
        });
    }
   // sortData(key) {
     // if (this.sortKey === key) {
       // this.sortDir = this.sortDir === 'asc' ? 'desc' : 'asc';
     // } else {
      //  this.sortKey = key;
      //  this.sortDir = 'asc';
     // }
    //}
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
