<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  label: string
  value: string
  trendDirection?: 'up' | 'down' | 'neutral'
}>()

const trendColor = computed(() => {
  if (props.trendDirection === 'up') return 'success'
  if (props.trendDirection === 'down') return 'error'
  return 'grey'
})

const trendIcon = computed(() => {
  if (props.trendDirection === 'up') return 'mdi-arrow-up'
  if (props.trendDirection === 'down') return 'mdi-arrow-down'
  return 'mdi-minus'
})
</script>

<template>
  <v-card elevation="1" class="rounded-lg">
    <div class="pa-6">
      <div class="text-overline font-weight-bold text-medium-emphasis mb-3" style="letter-spacing: 0.08em">
        {{ label }}
      </div>
      <div class="d-flex align-center">
        <span class="text-h4 font-weight-black">{{ value }}</span>
        <v-icon
          v-if="trendDirection && trendDirection !== 'neutral'"
          :icon="trendIcon"
          :color="trendColor"
          size="20"
          class="ml-2"
        />
      </div>
    </div>
  </v-card>
</template>
