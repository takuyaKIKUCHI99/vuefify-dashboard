<template>
  <v-data-table
    :headers="headers"
    :items="employees"
    :items-per-page="5"
    :sort-by="['id', 'name', 'title', 'salary']"
    :sort-desc="[false, false, false, true]"
    multi-sort
    class="elevation-1"
    @click:row="selectRow"
  ></v-data-table>
</template>

<script>
export default {
  name: "EmployeesTable",
  props: {
    employees: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      headers: [
        { text: "ID", value: "id" },
        { text: "Name", value: "name" },
        { text: "Title", value: "title" },
        { text: "Salary", value: "salary" },
      ],
    };
  },
  methods: {
    selectRow(event) {
      const employee = {
        name: event.name,
        title: event.title,
      };

      this.$emit("select-employee", employee);
    },
  },
};
</script>
