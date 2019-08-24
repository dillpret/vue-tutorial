<template>
  <div id="employee-table">
    <b-table-simple>
      <b-thead>
        <b-tr>
          <b-th>Employee name</b-th>
          <b-th>Employee email</b-th>
        </b-tr>
      </b-thead>
      <b-tbody>
        <b-tr v-for="employee in employees" :key="employee.id">
          <b-td>{{ employee.name }}</b-td>
          <b-td>{{ employee.email }}</b-td>
        </b-tr>
      </b-tbody>
    </b-table-simple>
  </div>
</template>

<script>
  export default {
    name: 'employee-table',
    props: {
      employees: Array
    }
  }
</script>

<style scoped></style>