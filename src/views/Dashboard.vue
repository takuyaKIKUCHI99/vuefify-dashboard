<template>
  <div>
    <h1>Dashboard</h1>

    <SalesGraph v-for="sale in sales" :key="`${sale.title}`" :sale="sale" />

    <StatisticCard
      v-for="statistic in statistics"
      :key="`${statistic.title}`"
      :statistic="statistic"
    />

    <EmployeesTable :employees="employees" @select-employee="setEmployee"/>

    <EventTimeline :timeline="timeline" />

    <v-snackbar v-model="snackbar">
      You have selected {{ selectedEmployee.name }}, {{ selectedEmployee.title }}
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
// Components
import EmployeesTable from "@/components/EmployeesTable.vue";
import EventTimeline from "@/components/EventTimeline.vue";
import SalesGraph from "@/components/SalesGraph.vue";
import StatisticCard from "@/components/StatisticCard.vue";

// Data
import employeesData from "@/data/employees.json";
import timelineData from "@/data/timeline.json";
import salesData from "@/data/sales.json";
import statisticsData from "@/data/statistics.json";

export default {
  name: "Dashboard",
  components: {
    EmployeesTable,
    EventTimeline,
    SalesGraph,
    StatisticCard,
  },
  data() {
    return {
      // Employees table
      employees: employeesData,
      selectedEmployee: {
        name: "",
        title: "",
      },
      headers: [
        { text: "ID", value: "id" },
        { text: "Name", value: "name" },
        { text: "Title", value: "title" },
        { text: "Salary", value: "salary" },
      ],
      snackbar: false,

      // Event timeline
      timeline: timelineData,

      // Sales graph
      sales: salesData,

      // Statistic card
      statistics: statisticsData,
    };
  },
  methods: {
    setEmployee(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.name;
    },
  },
};
</script>
