<template>
  <div>
    <h1>Dashboard</h1>
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
    <v-snackbar v-model="snackbar">
      You have selected {{ currentEmployee }}
      <template v-slot:action="{ attrs }">
        <v-btn
          color="pink"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
import employees from "@/data/employees.json";

export default {
  name: "Dashboard",
  data() {
    return {
      snackbar: false,
      currentEmployee: "",
      headers: [
        { text: "ID", value: "id" },
        { text: "Name", value: "name" },
        { text: "Title", value: "title" },
        { text: "Salary", value: "salary" },
      ],
      employees: employees,
    };
  },
  methods: {
    selectRow(event) {
      this.snackbar = true;
      this.currentEmployee = event.name;
    },
  },
};
</script>
