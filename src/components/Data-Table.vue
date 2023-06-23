<script>
import demo from './example.json';
export default{
    data(){
    return{
      data: demo
    }
  }
}
</script>
<template>
<table id="firstTable">
    <thead>
      <tr>
        <th>VM Name</th>
        <th>Status</th>
        <th>IP</th>
        <th>Hyper Visor</th>
        <th>Host Name</th>
        <th>Last Checked</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in data.Servers">
        <td>{{row.VMName}}</td>
        <td>{{row.Status}}</td>
        <td>{{row.IP}}</td>
        <td>{{row.HyperVisor}}</td>
        <td>{{row.Hostname}}</td>
        <td>{{row.LastCheckInTime}}</td>
      </tr>
    </tbody>
  </table>
  </template>
<style>
table {
    font-family: 'Open Sans', sans-serif;
    width: 750px;
    border-collapse: collapse;
    border: 3px solid #44475C;
    margin: 10px 10px 0 10px;
    text-align: center;
    margin-left: auto;
    margin-right: auto;
  }
  
  table th {
    text-transform: uppercase;
    text-align: left;
    background: #44475C;
    color: #FFF;
    padding: 8px;
    min-width: 30px;
  }
  
  table td {
    text-align: left;
    padding: 8px;
    border-right: 2px solid #7D82A8;
  }
  table td:last-child {
    border-right: none;
  }
  table tbody tr:nth-child(2n) td {
    background: #D4D8F9;
  }
</style>