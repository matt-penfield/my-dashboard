<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  label: string
  value: string
  trend?: number
  suffix?: string
  invert?: boolean
}>()

const trendColor = computed(() => {
  if (!props.trend || props.trend === 0) return 'grey'
  const positive = props.invert ? props.trend < 0 : props.trend > 0
  return positive ? 'success' : 'error'
})

const trendIcon = computed(() => {
  if (!props.trend || props.trend === 0) return 'mdi-minus'
  return props.trend > 0 ? 'mdi-arrow-up' : 'mdi-arrow-down'
})

const trendText = computed(() => {
  if (!props.trend) return ''
  const abs = Math.abs(props.trend)
  return props.suffix ? `${abs}${props.suffix}` : abs.toLocaleString()
})
</script>

<template>
  <v-card elevation="1" class="rounded-lg">
    <div class="pa-6">
      <div class="text-overline font-weight-bold text-medium-emphasis mb-3" style="letter-spacing: 0.08em;">
        {{ label }}
      </div>
      <div class="d-flex align-center">
        <span class="text-h4 font-weight-black">{{ value }}</span>
        <v-chip
          v-if="trend !== undefined && trend !== 0"
          :color="trendColor"
          variant="tonal"
          size="small"
          class="ml-3"
          :prepend-icon="trendIcon"
        >
          {{ trendText }}
        </v-chip>
      </div>
    </div>
  </v-card>
</template>
