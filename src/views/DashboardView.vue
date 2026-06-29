<script setup lang="ts">
import { ref } from 'vue'
import AppHeader from '@/components/AppHeader.vue'
import AppModal from '@/components/AppModal.vue'
import KpiCard from '@/components/KpiCard.vue'
import ChartCard from '@/components/ChartCard.vue'

const modalOpen = ref(false)
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
            value="—"
            trend="Placeholder"
            trend-direction="up"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="On-Time Delivery Rate"
            value="—"
            trend="Placeholder"
            trend-direction="down"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="Regional Performance"
            value="—"
            trend="Placeholder"
            trend-direction="neutral"
          />
        </v-col>
        <v-col cols="12" sm="6" lg="3">
          <KpiCard
            label="Open Exceptions"
            value="—"
            trend="Placeholder"
            trend-direction="down"
          />
        </v-col>
      </v-row>

      <!-- Charts Row -->
      <v-row class="mt-2">
        <v-col cols="12" md="6">
          <ChartCard title="Shipment Volume (Monthly)" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="On-Time Delivery Rate (%)" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="Regional Performance Score" />
        </v-col>
        <v-col cols="12" md="6">
          <ChartCard title="Open Exceptions" />
        </v-col>
      </v-row>
    </v-container>
  </v-main>

  <AppModal v-model="modalOpen">
    <h2 class="text-h6 mb-4">Performance Analysis</h2>
    <p class="text-body-2 text-medium-emphasis">Analysis content will go here.</p>
  </AppModal>
</template>
