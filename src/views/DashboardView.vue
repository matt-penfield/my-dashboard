<script setup lang="ts">
import { ref } from 'vue'
import AppHeader from '@/components/AppHeader.vue'
import AppModal from '@/components/AppModal.vue'
import KpiCard from '@/components/KpiCard.vue'
import ChartCard from '@/components/ChartCard.vue'

const modalOpen = ref(false)

// Placeholder data simulating a year of logistics metrics
const volumeData = [4380, 4590, 4810, 5020, 5250, 5410, 5630, 5870, 6050, 6280, 6490, 6720]
const otdData = [95.8, 95.2, 94.6, 94.1, 93.5, 93.0, 92.6, 92.1, 91.4, 91.0, 90.3, 89.8]
const regionalData = [82, 79, 84, 77, 81, 76, 83, 78, 80, 75, 82, 77]
const exceptionsData = [38, 44, 49, 55, 60, 67, 72, 79, 84, 91, 97, 104]
</script>

<template>
  <AppHeader
    title="Logistics Dashboard"
    button-label="Performance Analysis"
    @action="modalOpen = true"
  />

  <v-main>
    <v-container fluid>
      <!-- KPI Cards Row -->
      <v-row>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="Shipment Volume (YTD)"
            value="66,500"
            trend="↑ 53.4% growth (Jan–Dec)"
            trend-direction="up"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="On-Time Delivery Rate"
            value="92.8%"
            trend="↓ 6.0pp decline (Jan–Dec)"
            trend-direction="down"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="Regional Performance"
            value="79.5/100"
            trend="~ Variable across regions"
            trend-direction="neutral"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="Open Exceptions"
            value="104"
            trend="↑ 174% increase (Jan–Dec)"
            trend-direction="down"
          />
        </v-col>
      </v-row>

      <!-- Charts Row -->
      <v-row class="mt-2">
        <v-col cols="12" md="6">
          <ChartCard title="Shipment Volume (Monthly)" :data="volumeData" color="blue" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="On-Time Delivery Rate (%)" :data="otdData" color="green" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="Regional Performance Score" :data="regionalData" color="purple" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="Open Exceptions" :data="exceptionsData" color="red" />
        </v-col>
      </v-row>
    </v-container>
  </v-main>

  <AppModal v-model="modalOpen">
    <h2 class="text-h6 mb-4">Performance Analysis</h2>
    <v-alert type="info" variant="tonal" class="mb-3">
      Shipment volume grew 53% YTD while on-time delivery declined 6pp — capacity may be strained.
    </v-alert>
    <v-alert type="warning" variant="tonal" class="mb-3">
      Open exceptions rose from 38 to 104, tracking closely with volume increases.
    </v-alert>
    <v-alert type="success" variant="tonal">
      Regional performance remains stable at ~79.5 avg despite volume pressure.
    </v-alert>
  </AppModal>
</template>
