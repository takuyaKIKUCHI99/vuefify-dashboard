<template>
  <v-container>
    <h1>Dashboard</h1>

    <v-row>
      <v-col v-for="sale in sales" :key="`${sale.title}`" cols="12" sm="4">
        <SalesGraph :sale="sale" />
      </v-col>
    </v-row>

    <v-row>
      <v-col v-for="statistic in statistics" :key="`${statistic.title}`" cols="12" sm="6" lg="3">
        <StatisticCard :statistic="statistic" />
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" sm="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee"/>
      </v-col>

      <v-col cols="12" sm="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>

    <v-row id="below-the-fold" v-intersect="showMoreContent">
      <v-col cols="12" sm="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee"/>
      </v-col>

      <v-col cols="12" sm="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>

    <v-row v-if="loadNewContent" id="more-content">
      <v-col>
        <v-skeleton-loader
          ref="skeleton"
          type="table"
          class="mx-auto"
        ></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-snackbar v-model="snackbar" :left="$vuetify.breakpoint.lgAndUp">
      You have selected {{ selectedEmployee.name }}, {{ selectedEmployee.title }}
      <v-btn
        color="pink"
        text
        @click="snackbar = false"
      >
        Close
      </v-btn>
    </v-snackbar>
  </v-container>
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
      // Dashboard
      loadNewContent: false,
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
    showMoreContent(entries) {
      this.loadNewContent = entries[0].isIntersecting;
    },
  },
};
</script>
