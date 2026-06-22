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

  <section class="kpi-grid">
    <KpiCard
      label="Shipment Volume (YTD)"
      value="—"
      trend="Placeholder"
      trend-direction="up"
    />
    <KpiCard
      label="On-Time Delivery Rate"
      value="—"
      trend="Placeholder"
      trend-direction="down"
    />
    <KpiCard
      label="Regional Performance"
      value="—"
      trend="Placeholder"
      trend-direction="neutral"
    />
    <KpiCard
      label="Open Exceptions"
      value="—"
      trend="Placeholder"
      trend-direction="down"
    />
  </section>

  <section class="charts-grid">
    <ChartCard title="Shipment Volume (Monthly)" />
    <ChartCard title="On-Time Delivery Rate (%)" />
    <ChartCard title="Regional Performance Score" />
    <ChartCard title="Open Exceptions" />
  </section>

  <AppModal :open="modalOpen" @close="modalOpen = false">
    <h2>Performance Analysis</h2>
    <p class="modal-placeholder">Analysis content will go here.</p>
  </AppModal>
</template>

<style scoped>
.kpi-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 28px;
}

.charts-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.modal-placeholder {
  color: var(--text-secondary);
  font-size: 0.875rem;
  padding: 16px;
  background: var(--primary-light);
  border-radius: 8px;
}

@media (max-width: 1024px) {
  .kpi-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .charts-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .kpi-grid {
    grid-template-columns: 1fr;
  }
}
</style>
