<template>
  <div class="content">
    <h1>Employees App</h1>
    <EmployeesListList/>
    <div class="list">
      <ul class="list_content">
       
        <li v-for="employee in employees" :key="employee.id">
          <h4>{{ employee.fullname }}</h4>
          <h4>{{ employee.dep }}</h4>
          <h4>{{ employee.birthdate }}</h4>
          <h4>{{ employee.salary }}</h4>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import EmployeesListList from './EmployeesListList.vue';

export default {
    name: 'EmployeesList',
    components: {
        EmployeesListList,
    },
  data() {
    return {
      employees: [],
      fullname: '',
      dep: '',
      birthdate: '',
      salary: '',
      id: '',
      isEditing: false,
    }
  },
  methods: {
    async getEmployee() {
      try {
        await this.$http.get(`http://127.0.0.1:8000/api/employees/`).then((response) => {
          this.employees = response.data
        })
      } catch (error) {
        console.log(error)
      }
    },
  },
  created() {
    this.getEmployee()
  },
}
</script>

// apply styling to the component

<style scoped></style>
