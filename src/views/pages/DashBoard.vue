<template>
  <!-- ---------------------------------------------- -->
  <!---First Row -->
  <!-- ---------------------------------------------- -->
  <v-row class="flex-0" dense>
    <v-col cols="12" xl="4">
      <!-- Sales Card -->
      <v-card class="card-shadow" height="460">
        <sales-card></sales-card>
      </v-card>
    </v-col>
    <v-col cols="12" md="6" xl="4">
      <!-- Activity Card -->
      <v-card class="card-shadow" height="460">
        <activity-card></activity-card>
      </v-card>
    </v-col>
    <v-col cols="12" md="6" xl="4">
      <!-- Trafiic Card-->
      <v-card class="card-shadow h-full" height="460">
        <sources-card></sources-card>
      </v-card>
    </v-col>
  </v-row>
  <!-- ---------------------------------------------- -->
  <!---Second Row -->
  <!-- ---------------------------------------------- -->
  <v-row class="card-shadow flex-grow-0" dense>
    <v-col cols="12" xl="6">
      <!-- Table Card-->
      <v-card class="card-shadow" height="460">
        <table-card></table-card>
      </v-card>
    </v-col>
    <v-col cols="12" xl="6">
      <!-- Task Card-->
      <v-card class="card-shadow" height="460">
        <task-card></task-card>
      </v-card>
    </v-col>
  </v-row>
  <!-- ---------------------------------------------- -->
  <!---Third Row -->
  <!-- ---------------------------------------------- -->
  <v-row class="card-shadow flex-grow-0" dense>
    <v-col cols="12" xl="6">
      <!-- Target Card-->
      <v-card class="card-shadow" height="460"><todo-card></todo-card></v-card>
    </v-col>
    <v-col cols="12" xl="6">
      <v-card class="card-shadow" height="460"
        ><tickets-card></tickets-card>
      </v-card>
    </v-col>
  </v-row>
</template>

<script setup lang="ts">
import { ref } from "@vue/reactivity";
import SalesCard from "@/components/dashboard/SalesCard.vue";
import SourcesCard from "@/components/dashboard/SourcesCard.vue";
import ActivityCard from "@/components/dashboard/ActivityCard.vue";
import TableCard from "@/components/dashboard/TableCard.vue";
import TicketsCard from "@/components/dashboard/TicketsCard.vue";
import TrackCard from "@/components/dashboard/TrackCard.vue";
import TodoCard from "@/components/dashboard/TodoCard.vue";
import TaskCard from "@/components/dashboard/TaskCard.vue";

import router, { constantRoutes, dynamicRoutes } from "@/router";
console.log(router);
console.log(constantRoutes);

const order = ref(1);
</script>

<style lang="scss" scoped>
.card-shadow {
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px !important;
}
</style>
