<script setup lang="ts">
defineProps<{
  title: string
  buttonLabel?: string
}>()

defineEmits<{
  action: []
}>()
</script>

<template>
  <v-app-bar flat color="white" border="b" height="64" class="px-4">
    <v-app-bar-title>
      <span class="text-h6 font-weight-bold">{{ title }}</span>
    </v-app-bar-title>
    <template #append>
      <v-btn
        v-if="buttonLabel"
        color="primary"
        variant="tonal"
        class="text-none font-weight-bold mr-3"
        prepend-icon="mdi-chart-line"
        @click="$emit('action')"
      >
        {{ buttonLabel }}
      </v-btn>
      <v-btn variant="outlined" append-icon="mdi-menu-down" class="text-none">
        All Months
      </v-btn>
    </template>
  </v-app-bar>
</template>
