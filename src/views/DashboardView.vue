<script setup lang="ts">
import { ref } from 'vue'
import AppHeader from '@/components/AppHeader.vue'
import AppModal from '@/components/AppModal.vue'
import KpiCard from '@/components/KpiCard.vue'
import ChartCard from '@/components/ChartCard.vue'

const modalOpen = ref(false)

// Monthly data matching the design
const volumeData = [12200, 13800, 14500, 15100, 16200, 16800, 17100, 17600, 18200, 18900, 19500, 19800]
const otdData = [94, 93, 93, 92, 91, 90, 89, 88, 91, 90, 87, 85]
const exceptionsData = [142, 155, 168, 172, 185, 198, 210, 232, 230, 248, 265, 285]
const regionalData = [88, 87, 89, 86, 88, 85, 87, 89, 86, 88, 86, 85]
</script>

<template>
  <AppHeader
    title="Fast Forward Logistics"
    button-label="Performance Analysis"
    @action="modalOpen = true"
  />

  <v-main>
    <v-container fluid class="pa-6">
      <!-- KPI Cards Row -->
      <v-row>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard label="Shipment Volume" value="194,250" />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard label="On-Time Delivery" value="90.2%" />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard label="Regional Performance" value="86.5%" />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard label="Open Exceptions" value="2,522" />
        </v-col>
      </v-row>

      <!-- Charts Row -->
      <v-row class="mt-4">
        <v-col cols="12" md="6">
          <ChartCard
            title="Monthly Shipment Volume"
            type="bar"
            :data="volumeData"
            color="blue"
          />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard
            title="On-Time Delivery Rate"
            type="line"
            :data="otdData"
            color="cyan"
            y-suffix="%"
          />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard
            title="Open Exceptions Trend"
            type="line"
            :data="exceptionsData"
            color="red"
            :fill="true"
          />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard
            title="Regional Performance"
            type="line"
            :data="regionalData"
            color="orange"
            y-suffix="%"
          />
        </v-col>
      </v-row>
    </v-container>
  </v-main>

  <AppModal v-model="modalOpen">
    <h2 class="text-h5 font-weight-bold mb-5">Performance Analysis</h2>
    <v-alert type="info" variant="tonal" class="mb-4">
      Shipment volume grew 62% YTD while on-time delivery declined 9pp — capacity is strained.
    </v-alert>
    <v-alert type="warning" variant="tonal" class="mb-4">
      Open exceptions doubled from 142 to 285, tracking closely with volume increases.
    </v-alert>
    <v-alert type="success" variant="tonal">
      Regional performance remains stable at ~86.5% avg despite volume pressure.
    </v-alert>
  </AppModal>
</template>
