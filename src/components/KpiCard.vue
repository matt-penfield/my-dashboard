<script setup lang="ts">
defineProps<{
  label: string
  value: string
  trend?: string
  trendDirection?: 'up' | 'down' | 'neutral'
}>()
</script>

<template>
  <v-card variant="outlined">
    <v-card-text>
      <div class="text-overline text-medium-emphasis">{{ label }}</div>
      <div class="text-h4 font-weight-bold mt-1">{{ value }}</div>
      <div
        v-if="trend"
        class="text-caption mt-1"
        :class="{
          'text-success': trendDirection === 'up',
          'text-error': trendDirection === 'down',
          'text-warning': trendDirection === 'neutral',
        }"
      >
        {{ trend }}
      </div>
    </v-card-text>
  </v-card>
</template>
