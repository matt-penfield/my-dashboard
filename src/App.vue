<script setup lang="ts">
import { ref, computed } from 'vue'
import metrics from './data/metrics.json'
import MetricCard from './components/MetricCard.vue'
import ChartCard from './components/ChartCard.vue'
import AppModal from './components/AppModal.vue'

const months = ['All', ...metrics.map((m) => m.month)]
const selectedMonth = ref('All')
const modalOpen = ref(false)

const filteredData = computed(() => {
  if (selectedMonth.value === 'All') return metrics
  return metrics.filter((m) => m.month === selectedMonth.value)
})

const kpis = computed(() => {
  const data = filteredData.value
  const volume = data.reduce((sum, m) => sum + m.shipmentVolume, 0)
  const otd = +(data.reduce((sum, m) => sum + m.onTimeDelivery, 0) / data.length).toFixed(1)
  const regional = +(data.reduce((sum, m) => sum + m.regionalPerformance, 0) / data.length).toFixed(1)
  const exceptions = data[data.length - 1].openExceptions

  // Trend vs previous month
  const currentIdx = selectedMonth.value === 'All' ? metrics.length - 1 : metrics.findIndex((m) => m.month === selectedMonth.value)
  const prev = currentIdx > 0 ? metrics[currentIdx - 1] : null
  const curr = metrics[currentIdx]

  const dir = (n: number): 'up' | 'down' | 'neutral' => n > 0 ? 'up' : n < 0 ? 'down' : 'neutral'
  const dirInvert = (n: number): 'up' | 'down' | 'neutral' => n > 0 ? 'down' : n < 0 ? 'up' : 'neutral'

  return {
    volume: { value: volume.toLocaleString(), direction: dir(prev ? curr.shipmentVolume - prev.shipmentVolume : 0) },
    otd: { value: otd + '%', direction: dir(prev ? curr.onTimeDelivery - prev.onTimeDelivery : 0) },
    regional: { value: regional + '%', direction: dir(prev ? curr.regionalPerformance - prev.regionalPerformance : 0) },
    exceptions: { value: exceptions.toLocaleString(), direction: dirInvert(prev ? curr.openExceptions - prev.openExceptions : 0) },
  }
})

const chartLabels = computed(() => filteredData.value.map((m) => m.month))
const volumeData = computed(() => filteredData.value.map((m) => m.shipmentVolume))
const otdData = computed(() => filteredData.value.map((m) => m.onTimeDelivery))
const exceptionsData = computed(() => filteredData.value.map((m) => m.openExceptions))
const regionalData = computed(() => filteredData.value.map((m) => m.regionalPerformance))
</script>

<template>
  <v-app>
    <v-app-bar flat color="white" border="b" height="64">
      <v-app-bar-title class="ml-2">
        <span class="text-h6 font-weight-bold">Fast Forward Logistics</span>
      </v-app-bar-title>
      <template #append>
        <v-btn
          variant="tonal"
          color="primary"
          class="text-none font-weight-medium mr-3"
          prepend-icon="mdi-chart-line"
          @click="modalOpen = true"
        >
          Performance Analysis
        </v-btn>
        <v-select
          v-model="selectedMonth"
          :items="months"
          variant="outlined"
          density="compact"
          hide-details
          style="max-width: 140px"
        />
      </template>
    </v-app-bar>

    <v-main class="bg-grey-lighten-4">
      <v-container class="py-8 px-6">
        <!-- KPI Cards -->
        <v-row>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard label="Shipment Volume" :value="kpis.volume.value" :trend-direction="kpis.volume.direction" />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard label="On-Time Delivery" :value="kpis.otd.value" :trend-direction="kpis.otd.direction" />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard label="Regional Performance" :value="kpis.regional.value" :trend-direction="kpis.regional.direction" />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard label="Open Exceptions" :value="kpis.exceptions.value" :trend-direction="kpis.exceptions.direction" />
          </v-col>
        </v-row>

        <!-- Charts -->
        <v-row class="mt-6">
          <v-col cols="12" md="6">
            <ChartCard
              title="Monthly Shipment Volume"
              type="bar"
              :data="volumeData"
              :labels="chartLabels"
              color="#4285f4"
              :y-min="10000"
            />
          </v-col>
          <v-col cols="12" md="6">
            <ChartCard
              title="On-Time Delivery Rate"
              type="bar"
              :data="otdData"
              :labels="chartLabels"
              color="#00bcd4"
              y-suffix="%"
              :y-min="80"
            />
          </v-col>
        </v-row>

        <v-row class="mt-2">
          <v-col cols="12" md="6">
            <ChartCard
              title="Open Exceptions Trend"
              type="bar"
              :data="exceptionsData"
              :labels="chartLabels"
              color="#ef5350"
              :y-min="100"
            />
          </v-col>
          <v-col cols="12" md="6">
            <ChartCard
              title="Regional Performance"
              type="bar"
              :data="regionalData"
              :labels="chartLabels"
              color="#ffa726"
              y-suffix="%"
              y-step-integer
              :y-min="80"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <AppModal v-model="modalOpen">
      <h2 class="text-h5 font-weight-bold mb-6">Performance Analysis</h2>
      <p class="text-body-1 mb-4">
        Open exceptions have risen steadily from 142 in January to 289 in December — a 103% increase.
        This trend closely mirrors the growth in shipment volume over the same period.
      </p>
      <v-divider class="my-4" />
      <h3 class="text-subtitle-1 font-weight-bold mb-3">Likely Contributing Factors</h3>
      <v-list lines="two" class="bg-transparent">
        <v-list-item prepend-icon="mdi-truck-alert">
          <v-list-item-title class="font-weight-medium">Capacity constraints</v-list-item-title>
          <v-list-item-subtitle>Network nearing saturation as volume grew 64% without proportional fleet expansion.</v-list-item-subtitle>
        </v-list-item>
        <v-list-item prepend-icon="mdi-clock-alert-outline">
          <v-list-item-title class="font-weight-medium">Longer processing queues</v-list-item-title>
          <v-list-item-subtitle>Higher volume creates backlog at sorting hubs, increasing exception window.</v-list-item-subtitle>
        </v-list-item>
        <v-list-item prepend-icon="mdi-map-marker-alert-outline">
          <v-list-item-title class="font-weight-medium">Regional imbalances</v-list-item-title>
          <v-list-item-subtitle>Performance dips in underserved regions correlate with higher exception rates.</v-list-item-subtitle>
        </v-list-item>
        <v-list-item prepend-icon="mdi-account-group-outline">
          <v-list-item-title class="font-weight-medium">Staffing gaps</v-list-item-title>
          <v-list-item-subtitle>Seasonal hiring lag in Q3/Q4 compounds delays during peak periods.</v-list-item-subtitle>
        </v-list-item>
      </v-list>
    </AppModal>
  </v-app>
</template>
