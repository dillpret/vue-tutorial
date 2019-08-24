<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">
      No employees
    </p>
    <b-table-simple>
      <b-thead>
        <b-tr>
          <b-th>Employee name</b-th>
          <b-th>Employee email</b-th>
          <b-th>Actions</b-th>
        </b-tr>
      </b-thead>
      <b-tbody>
        <b-tr v-for="employee in employees" :key="employee.id">
          <b-td v-if="editing === employee.id">
            <b-input type="text" v-model="employee.name"/>
          </b-td>
          <b-td v-else>{{ employee.name }}</b-td>

          <b-td v-if="editing === employee.id">
            <b-input type="email" v-model="employee.email"/>
          </b-td>
          <b-td v-else>{{ employee.email }}</b-td>

          <b-td v-if="editing === employee.id">
            <b-button pill variant="success" @click="editEmployee(employee)">
              Save
            </b-button>
            <b-button pill @click="cancelEdit(employee)">
              Cancel
            </b-button>
          </b-td>
          <b-td v-else>
            <b-button pill @click="editMode(employee)">
              Edit
            </b-button>
            <b-button pill variant="danger" @click="$emit('delete:employee', employee.id)">
              Delete
            </b-button>
          </b-td>

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
    },
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editMode(employee) {
        this.cachedEmployee = Object.assign({}, employee)
        this.editing = employee.id
      },

      cancelEdit(employee) {
        Object.assign(employee, this.cachedEmployee)
      },

      editEmployee(employee) {
        if (employee.name === '' || employee.email === ''){
          return
        }
        this.$emit('edit:employee', employee.id, employee)
        this.editing = null
      }
    },
  }
</script>

<style scoped></style>