<script setup lang="ts">
defineProps<{
  title: string
  data?: number[]
  color?: string
}>()
</script>

<template>
  <v-card variant="outlined" class="pa-1">
    <v-card-title class="text-subtitle-2 font-weight-bold pa-5 pb-0">{{ title }}</v-card-title>
    <v-card-text class="pa-5 pt-3">
      <v-sparkline
        v-if="data && data.length"
        :model-value="data"
        :color="color || 'primary'"
        :line-width="2"
        :padding="12"
        smooth
        auto-draw
        height="140"
      />
      <div v-else class="chart-placeholder">
        <slot>
          <span class="text-medium-emphasis text-body-2">Chart Placeholder</span>
        </slot>
      </div>
    </v-card-text>
  </v-card>
</template>

<style scoped>
.chart-placeholder {
  width: 100%;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgb(var(--v-theme-surface-variant));
  border-radius: 8px;
  border: 1px dashed rgba(var(--v-border-color), var(--v-border-opacity));
}
</style>
