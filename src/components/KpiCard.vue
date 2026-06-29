<script setup lang="ts">
defineProps<{
  label: string
  value: string
}>()
</script>

<template>
  <v-card variant="outlined" class="pa-1">
    <v-card-text class="pa-5">
      <div class="text-overline font-weight-bold text-medium-emphasis mb-2">{{ label }}</div>
      <div class="text-h4 font-weight-black">{{ value }}</div>
    </v-card-text>
  </v-card>
</template>
