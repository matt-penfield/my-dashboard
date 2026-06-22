<script setup lang="ts">
defineProps<{
  label: string
  value: string
  trend?: string
  trendDirection?: 'up' | 'down' | 'neutral'
}>()
</script>

<template>
  <div class="kpi-card">
    <div class="label">{{ label }}</div>
    <div class="value">{{ value }}</div>
    <div v-if="trend" class="trend" :class="trendDirection">{{ trend }}</div>
  </div>
</template>

<style scoped>
.kpi-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px;
  box-shadow: var(--shadow);
}

.label {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  margin-bottom: 6px;
}

.value {
  font-size: 1.75rem;
  font-weight: 700;
}

.trend {
  font-size: 0.8rem;
  margin-top: 4px;
}

.trend.up {
  color: var(--success);
}
.trend.down {
  color: var(--danger);
}
.trend.neutral {
  color: var(--warning);
}
</style>
