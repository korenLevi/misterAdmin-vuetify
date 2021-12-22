<template>
  <v-card>
    <v-card-title>
      Leads
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table :headers="headers" :items="dataTable" :search="search">
      <template v-slot:item.inboundDate="{ item }">
        {{ formatDate(item.inboundDate) }}
      </template>
      <template v-slot:item.caller="{ item }">
        <v-select v-model="item.caller" :items="item.employees">
          {{ item.employees }}</v-select
        >
      </template>

      <template v-slot:item.wasCalled="{ item }">
        <v-container class="px-0" fluid>
          <v-checkbox v-model="item.wasCalled"></v-checkbox>
        </v-container>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
import Json from "../../data/admin.json";
import moment from "moment";
import { adminService } from "../services/admin.service.js";
// new Date(item.inboundDate).toLocaleString()
// const moment = require('moment')
export default {
  data() {
    return {
      search: "",
      headers: [
        {
          text: "Incoming date",
          align: "start",
          filterable: false,
          value: "inboundDate",
          dataType: "Date",
        },
        { text: "Name", value: "fname" },
        { text: "Last Name", value: "lname" },
        { text: "Email", value: "email" },
        { text: "Phone", value: "phone" },
        { text: "Message", value: "words" },
        { text: "Lead Source", value: "src" },
        { text: "Was Called", value: "wasCalled" },
        { text: "Caller", value: "caller" },
      ],
      dataTable: Json,
    };
  },

  methods: {
    formatDate(value) {
      return moment(value).subtract(10, "days").calendar();
    },
    printj(item) {
      console.log(item);
    },
  },
  watch: {
    dataTable: {
      handler(newValue) {
        console.log("value", newValue);
        adminService.saveJson(this.dataTable);
        // save(value);
      },
      deep: true,
    },
  },
  components: {
    // moment
  },
};
</script>

<style>
</style>