<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <div class="chart-card">
    <h3>{{ title }}</h3>
    <div class="chart-placeholder">
      <slot>
        <span class="placeholder-text">Chart Placeholder</span>
      </slot>
    </div>
  </div>
</template>

<style scoped>
.chart-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px;
  box-shadow: var(--shadow);
}

.chart-card h3 {
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 16px;
  color: var(--text);
}

.chart-placeholder {
  width: 100%;
  height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg);
  border-radius: 8px;
  border: 1px dashed var(--border);
}

.placeholder-text {
  color: var(--text-secondary);
  font-size: 0.875rem;
}
</style>
